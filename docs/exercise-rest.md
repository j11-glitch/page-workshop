# Exercise 3 — REST API

Build a simple CRUD API for a `Task` resource.

## Requirements

| Method | Path | Description |
|--------|------|-------------|
| GET | `/tasks` | List all tasks |
| POST | `/tasks` | Create a task |
| DELETE | `/tasks/{id}` | Delete a task |

## Data model

```java
public record Task(Long id, String title, boolean done) {}
```

## Solution

```java
@RestController
@RequestMapping("/tasks")
public class TaskController {

    private final Map<Long, Task> tasks = new ConcurrentHashMap<>();
    private final AtomicLong idCounter = new AtomicLong();

    @GetMapping
    public Collection<Task> list() {
        return tasks.values();
    }

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public Task create(@RequestBody Task task) {
        long id = idCounter.incrementAndGet();
        Task saved = new Task(id, task.title(), false);
        tasks.put(id, saved);
        return saved;
    }

    @DeleteMapping("/{id}")
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public void delete(@PathVariable Long id) {
        tasks.remove(id);
    }
}
```

## Test it

```bash
# Create a task
curl -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Learn Spring"}'

# List tasks
curl http://localhost:8080/tasks
```

!!! tip "Next step"
    Replace the in-memory map with a real database using Spring Data JPA — just add the `spring-boot-starter-data-jpa` dependency and a `@Repository` interface.
