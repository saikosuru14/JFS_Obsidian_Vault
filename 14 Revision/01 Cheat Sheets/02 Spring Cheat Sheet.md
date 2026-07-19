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

> Mid-level recall for [[Spring]] — the gotchas that come up in real services and interviews.

## Core / IoC
- DI: constructor (preferred — immutable, testable, fails fast on cycles), setter, field (avoid).
- Scopes: `singleton` (default, one per container), `prototype`, `request`, `session`.
- Proxies: interface → JDK dynamic proxy; class → CGLIB. `@Configuration` beans are CGLIB-enhanced so inter-`@Bean` calls return the singleton.
- Circular deps: constructor cycles fail; break with `@Lazy` or redesign.

## Transactions (@Transactional pitfalls)
- **Self-invocation** (calling a `@Transactional` method from the same bean) bypasses the proxy → no transaction. Split into another bean.
- Only **unchecked** exceptions roll back by default; use `rollbackFor` for checked.
- Propagation: `REQUIRED` (default, joins), `REQUIRES_NEW` (suspends), `NESTED` (savepoint). Isolation maps to DB level.
- `@Transactional` on private/final methods = no proxy = ignored.
- Keep transactions short; don't do remote calls inside them.

## Spring Boot
- `@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`.
- Config precedence: CLI args > env vars > `application-{profile}.yml` > `application.yml`.
- Conditional beans: `@ConditionalOnProperty/Class/MissingBean`; `@Profile` for env-specific.
- Connection pool: **HikariCP** default — size it (`maximum-pool-size`) to DB capacity, not thread count.
- Actuator: `/health`, `/metrics`, Micrometer → Prometheus; enable liveness/readiness groups for k8s.

## Web / MVC
- Flow: DispatcherServlet → HandlerMapping → Controller → `@ResponseBody`/ViewResolver.
- `@ControllerAdvice` + `@ExceptionHandler` for consistent error bodies (never leak stack traces).
- `@Valid` + `MethodArgumentNotValidException`; `ResponseEntity` for status/headers.
- WebFlux only when you need reactive end-to-end (don't mix blocking JDBC into it).

## Data JPA / Hibernate
- **N+1**: fix with `JOIN FETCH` / `@EntityGraph`; watch lazy access outside a session (`LazyInitializationException`).
- Entity states: transient → persistent → detached → removed; dirty checking flushes at commit.
- `@Transactional(readOnly=true)` for reads (skips dirty checking, hints replicas).
- Caches: L1 = session; L2 = shared (optional). Pagination: prefer keyset over large offsets.
- Optimistic (`@Version`) for low contention; pessimistic (`SELECT … FOR UPDATE`) for hot rows.

## Security
- Filter chain → `AuthenticationManager` → `UserDetailsService` + `PasswordEncoder` (BCrypt/Argon2).
- Stateless APIs: JWT (validate signature/expiry; short-lived + refresh). Delegated: OAuth2/OIDC. CSRF matters for cookie-based sessions, not stateless bearer tokens.
- Method security: `@PreAuthorize("hasRole('ADMIN')")`.

## Sharp Interview Answers
- Why does `@Transactional` sometimes "not work"? self-invocation / private / checked exception.
- Constructor vs field injection; `@Configuration` proxying.
- How Boot auto-config works (`spring.factories`/`AutoConfiguration.imports` + conditionals).
- Fixing N+1; optimistic vs pessimistic locking.

## Revision Checklist
- [ ] DI types, scopes, proxying
- [ ] @Transactional propagation + pitfalls
- [ ] Boot auto-config + config precedence + Hikari
- [ ] JPA N+1, caching, locking
- [ ] Security filter chain, JWT vs OAuth2
