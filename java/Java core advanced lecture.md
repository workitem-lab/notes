
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
