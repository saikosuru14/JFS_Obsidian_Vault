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

> Fast recall for [[Spring]]. See the [[Spring Index|Spring domain]] for depth.

## Core / IoC
- IoC container manages bean lifecycle; DI via constructor (preferred), setter, field.
- Bean scopes: `singleton` (default), `prototype`, `request`, `session`.
- `@Component/@Service/@Repository/@Controller`; `@Configuration` + `@Bean`.
- `@Autowired`, `@Qualifier`, `@Primary`, `@Value`, `@Profile`.

## Spring Boot
- Auto-configuration + starters; `@SpringBootApplication` = `@Configuration` + `@EnableAutoConfiguration` + `@ComponentScan`.
- External config precedence: CLI args > env > `application-{profile}.yml` > `application.yml`.
- Actuator exposes health/metrics endpoints.

## Web / MVC
- Request flow: DispatcherServlet → HandlerMapping → Controller → ViewResolver/`@ResponseBody`.
- `@RestController`, `@RequestMapping`, `@GetMapping`, `@PathVariable`, `@RequestParam`, `@RequestBody`.
- `@ControllerAdvice` + `@ExceptionHandler` for global error handling; `@Valid` for validation.
- `ResponseEntity` for status + headers + body.

## Data JPA / Hibernate
- `JpaRepository` gives CRUD + paging; derived queries, `@Query` (JPQL/native), Specifications.
- Entity states: transient → persistent → detached → removed. Dirty checking flushes changes.
- Lazy vs eager fetch; the **N+1 problem** → fix with `JOIN FETCH`/entity graph.
- First-level cache = session; second-level cache = shared, optional.
- Optimistic (`@Version`) vs pessimistic locking.

## Security
- Filter chain intercepts requests; `AuthenticationManager` + `UserDetailsService` + `PasswordEncoder` (BCrypt).
- Authentication (who) vs authorization (`@PreAuthorize`, roles).
- Stateless APIs: JWT; delegated auth: OAuth2. CSRF matters for browser sessions.

## Top Interview One-Liners
- Why constructor injection? Immutability + easy testing + fail-fast.
- Bean scope default = singleton (one per container).
- How does `@Transactional` work? AOP proxy around the method.

## Revision Checklist
- [ ] IoC, DI types, scopes
- [ ] Boot auto-config + config precedence
- [ ] Request lifecycle
- [ ] JPA states, N+1, caching, locking
- [ ] Security filter chain, JWT vs OAuth2
