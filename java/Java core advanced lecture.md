git commit -m "Java core advanced lecture: add SimpleThreadExample"
## Threads vs Tasks (key mental model)

### Threads

A `Thread` is a worker that can run code _independently_ from others.

```java
public class SimpleThreadExample {
    public static void main(String[] args) {
        Thread t = new Thread(() -> {
            System.out.println("Running in thread: " + Thread.currentThread().getName());
        });

        t.start(); // async
        System.out.println("Main finished");
    }
}
```

- **Example**: In this `SimpleThreadExample`, we explicitly create a new `Thread` object and start it.
    
- **Characteristics**:
    - Runs concurrently with other threads.
    - Managed directly by the operating system.
    - Each thread has its own stack and incurs overhead in memory and scheduling.
