# Exercise 1 — Hello Spring

Get a Spring Boot app running in under 5 minutes.

## Setup

Generate a new project at [start.spring.io](https://start.spring.io) with:

- **Group:** `com.example`
- **Artifact:** `hello`
- **Dependencies:** Spring Web

## Your task

Create a REST controller that responds with `"Hello, Spring!"` on `GET /hello`.

## Solution

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring!";
    }
}
```

Run it:

```bash
./mvnw spring-boot:run
```

Then visit [http://localhost:8080/hello](http://localhost:8080/hello).

!!! tip
    Spring Boot auto-configures an embedded Tomcat server. No `web.xml`, no deployment — just run the main class.
