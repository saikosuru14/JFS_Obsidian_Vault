---
title: Spring Cheat Sheet
aliases:
  - Spring Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 2
tags:
  - revision
  - spring
---

# Spring Cheat Sheet

> Interview-ready revision for [[Spring]] (4–5 YOE). Concepts, code, tables, and Q&A with answers.

---

## 1. Core / IoC & DI
The container creates beans, resolves dependencies, and manages lifecycle. Prefer **constructor injection** — enforces immutability, makes dependencies explicit, supports `final`, fails fast on missing/circular deps, and needs no Spring to unit-test.

```java
@Service
class OrderService {
    private final OrderRepository repo;      // final = required
    OrderService(OrderRepository repo) { this.repo = repo; }  // no @Autowired needed (single ctor)
}
```

- `@Component`/`@Service`/`@Repository`/`@Controller` = classpath-scanned beans. `@Bean` in a `@Configuration` = programmatic/third-party beans.
- `@Repository` also translates persistence exceptions to `DataAccessException`.
- Resolve ambiguity: `@Primary`, `@Qualifier("name")`. Inject config with `@Value("${...}")`.

### Proxies (root of many gotchas)
Spring wraps beans in proxies to add behavior (`@Transactional`, `@Async`, `@Cacheable`, security). Interface → **JDK dynamic proxy**; class → **CGLIB** subclass.
- `@Configuration` classes are CGLIB-enhanced ("full" mode), so calling one `@Bean` method from another returns the **singleton**, not a new object.
- **Self-invocation** (calling an annotated method from within the same bean) bypasses the proxy → the aspect (transaction/cache/async) does **not** apply.

---

## 2. Bean Lifecycle & Scopes
```
instantiate → populate deps → *Aware callbacks → BeanPostProcessor.before
→ @PostConstruct / InitializingBean / init-method → BeanPostProcessor.after
→ [bean in use] → @PreDestroy / DisposableBean / destroy-method
```

| Scope | Meaning | Note |
|-------|---------|------|
| singleton | one per container (default) | must be **stateless**/thread-safe |
| prototype | new each injection/lookup | container does **not** call destroy |
| request / session | one per HTTP request/session | web only |

- Injecting a **prototype into a singleton** freezes one instance — use `ObjectProvider<T>`, `@Lookup`, or a scoped proxy to get a fresh one.
- Singletons are shared across threads → keep them stateless (no mutable instance fields).

---

## 3. Spring Boot
`@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`.

**Auto-configuration:** Boot loads candidate config classes listed in `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` (Boot 2.7+/3.x; older used `spring.factories`) and applies them conditionally via `@ConditionalOnClass`, `@ConditionalOnMissingBean`, `@ConditionalOnProperty`. So defining your own `DataSource` bean disables the auto one.

**Config precedence (high → low):** CLI args → `SPRING_APPLICATION_JSON` → OS env vars → `application-{profile}.yml` → `application.yml` → `@PropertySource` → defaults. Relaxed binding maps `MY_VAR` ↔ `my.var`.

```java
@ConfigurationProperties(prefix = "app.mail")   // type-safe, relaxed binding, @Validated
record MailProps(String host, int port, @DefaultValue("false") boolean tls) {}
```
- `@Value` for one-off; `@ConfigurationProperties` for grouped/typed config.
- **HikariCP** is the default pool — size `maximum-pool-size` to DB capacity (often small, e.g. 10–20), not to app thread count.
- Actuator: `/actuator/health` (liveness/readiness groups for k8s), `/metrics` via **Micrometer** → Prometheus.

---

## 4. Spring MVC
```
DispatcherServlet → HandlerMapping → HandlerAdapter → (HandlerInterceptor.pre)
→ Controller → HttpMessageConverter (@ResponseBody) / ViewResolver → (post)
```
```java
@RestController
@RequestMapping("/api/orders")
class OrderController {
    @GetMapping("/{id}")
    ResponseEntity<OrderDto> get(@PathVariable long id) { ... }

    @PostMapping
    ResponseEntity<Void> create(@Valid @RequestBody CreateOrder req) { ... }
}

@RestControllerAdvice
class ApiErrors {
    @ExceptionHandler(MethodArgumentNotValidException.class)
    ResponseEntity<ErrorBody> onInvalid(...) { return ResponseEntity.badRequest().body(...); }
}
```
- **Filter vs Interceptor:** filters are servlet-level (before dispatch, e.g. auth, CORS, logging); interceptors are Spring-level (have handler/`ModelAndView` context).
- Return consistent error bodies (code, message, traceId) — never leak stack traces. Use WebFlux only for full reactive stacks (don't block inside it).

---

## 5. Transactions (`@Transactional`)
Proxy-based AOP: the proxy opens a transaction, delegates, then commits/rolls back.

```java
@Transactional(propagation = Propagation.REQUIRED, isolation = Isolation.READ_COMMITTED,
               timeout = 5, rollbackFor = BusinessException.class)
public void placeOrder(...) { ... }
```

| Propagation | Behavior |
|-------------|----------|
| REQUIRED (default) | join existing, else create |
| REQUIRES_NEW | suspend current, always new |
| NESTED | savepoint within current |
| MANDATORY / NEVER | require / forbid an existing tx |

**Pitfalls (very common interview trap):**
- **Self-invocation** bypasses the proxy → no transaction.
- Only **unchecked** (`RuntimeException`/`Error`) roll back by default → use `rollbackFor` for checked.
- `private`/`final` methods and non-Spring-managed objects → ignored.
- Keep transactions short; no remote/HTTP calls inside. Use `@Transactional(readOnly = true)` for reads.

---

## 6. Data JPA / Hibernate
Persistence context = **L1 cache** + dirty checking; changes flush at commit (or before a query). Entity states: transient → persistent → detached → removed.

- **N+1 problem:** lazy association loaded per row. Fix with `JOIN FETCH`, `@EntityGraph`, or `@BatchSize`.
```java
@EntityGraph(attributePaths = "items")
List<Order> findByStatus(Status s);      // one query, items eagerly fetched
```
- `LazyInitializationException`: lazy access after the session closes → fetch within the transaction or use a graph. Disable open-session-in-view (`spring.jpa.open-in-view=false`).
- Fetch: prefer `LAZY` for `@ManyToOne`/`@OneToMany`; fetch explicitly where needed.
- Locking: **optimistic** `@Version` (low contention, retry on `OptimisticLockException`) vs **pessimistic** `SELECT … FOR UPDATE` (hot rows). Pagination: keyset over large `OFFSET`.
- Caches: L1 = session (always); L2 = shared, opt-in (Ehcache/Hazelcast) for read-mostly reference data.

---

## 7. Spring Security (6.x)
```java
@Bean
SecurityFilterChain chain(HttpSecurity http) throws Exception {
    return http
        .authorizeHttpRequests(a -> a.requestMatchers("/api/admin/**").hasRole("ADMIN")
                                     .anyRequest().authenticated())
        .oauth2ResourceServer(o -> o.jwt(Customizer.withDefaults()))
        .csrf(c -> c.disable())          // ok for stateless bearer-token APIs
        .sessionManagement(s -> s.sessionCreationPolicy(STATELESS))
        .build();
}
```
- A chain of servlet filters → `AuthenticationManager` → `UserDetailsService` + `PasswordEncoder` (BCrypt/Argon2).
- **Authentication** (who) vs **authorization** (`@PreAuthorize("hasRole('ADMIN')")`, allowed).
- Stateless APIs: **JWT** (validate signature + expiry; short-lived access + refresh). Delegated login: **OAuth2/OIDC**. **CSRF** matters for cookie/session apps, not stateless bearer tokens. Configure **CORS** for browser clients.

---

## 8. Testing
| Annotation | Loads | Use for |
|------------|-------|---------|
| `@SpringBootTest` | full context | integration |
| `@WebMvcTest` | web slice (controllers) | MVC + `MockMvc` |
| `@DataJpaTest` | JPA slice + in-mem/Testcontainers DB | repositories |
| `@MockBean` | replaces a bean with a mock | isolate collaborators |

Use **Testcontainers** for real Postgres/Kafka in integration tests.

---

## 9. Interview Q&A (with answers)

**Q: Why does `@Transactional` sometimes not work?**
A: It's proxy-based, so it's skipped for self-invocation (calling the method from within the same bean), `private`/`final` methods, or non-managed objects. Also, only unchecked exceptions trigger rollback by default — checked ones need `rollbackFor`.

**Q: Constructor vs field injection?**
A: Constructor injection makes dependencies explicit and `final`, enables easy unit testing without Spring, and fails fast (including on circular deps). Field injection hides dependencies and needs reflection to test. Prefer constructor.

**Q: How does Boot auto-configuration work?**
A: `@EnableAutoConfiguration` loads candidate configs from `AutoConfiguration.imports`; each is guarded by `@Conditional*` annotations, so a config applies only if the relevant classes/properties are present and you haven't defined your own bean (`@ConditionalOnMissingBean`).

**Q: Singleton bean depending on a prototype — what happens?**
A: The prototype is injected once at singleton creation and effectively becomes a singleton. To get a fresh instance per use, inject `ObjectProvider<T>`, use `@Lookup`, or a scoped proxy.

**Q: How do you detect and fix N+1?**
A: Spot repeated identical queries in logs/`hibernate.show_sql`. Fix with `JOIN FETCH`, `@EntityGraph`, or `@BatchSize`. Avoid eager fetching everything.

**Q: Are singleton beans thread-safe?**
A: The container guarantees a single instance, not thread safety. Keep singletons stateless (no mutable instance fields) or synchronize/use thread-safe state.

**Q: Filter vs Interceptor?**
A: Filters are servlet-container level, run before/after the DispatcherServlet (auth, CORS, logging). Interceptors are Spring MVC level with access to the handler and `ModelAndView`.

**Q: `@Component` vs `@Bean`?**
A: `@Component` (+ scanning) is for your own classes; `@Bean` in a `@Configuration` is for programmatic creation or third-party classes you can't annotate.

**Q: Optimistic vs pessimistic locking?**
A: Optimistic (`@Version`) assumes rare conflicts and fails at commit — cheap, retry on conflict. Pessimistic locks the row up front (`FOR UPDATE`) — use for hot, high-contention rows.

---

## Revision Checklist
- [ ] DI types + proxy/self-invocation
- [ ] Bean lifecycle + scopes (prototype-in-singleton)
- [ ] Auto-config + config precedence + HikariCP
- [ ] MVC flow + filter vs interceptor + `@RestControllerAdvice`
- [ ] `@Transactional` propagation + pitfalls
- [ ] JPA N+1, fetch, caching, locking, open-in-view
- [ ] Security filter chain, JWT vs OAuth2, CSRF/CORS
- [ ] Test slices + Testcontainers
