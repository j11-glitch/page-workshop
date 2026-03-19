# Exercise 2 — Dependency Injection

Learn how Spring manages your beans and wires them together.

## The scenario

You have a `GreetingService` that generates greetings. Instead of creating it with `new`, let Spring inject it.

## Your task

1. Create a `GreetingService` interface
2. Implement it as a `@Service`
3. Inject it into a controller using constructor injection

## Solution

```java
public interface GreetingService {
    String greet(String name);
}
```

```java
@Service
public class SimpleGreetingService implements GreetingService {

    @Override
    public String greet(String name) {
        return "Hello, " + name + "!";
    }
}
```

```java
@RestController
public class GreetingController {

    private final GreetingService greetingService;

    public GreetingController(GreetingService greetingService) {
        this.greetingService = greetingService;
    }

    @GetMapping("/greet")
    public String greet(@RequestParam String name) {
        return greetingService.greet(name);
    }
}
```

!!! note
    Spring Boot detects `@Service`, `@Component`, and `@Repository` automatically via **component scanning** — no XML config needed.
