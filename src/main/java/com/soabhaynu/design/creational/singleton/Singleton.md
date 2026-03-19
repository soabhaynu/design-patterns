# Singleton (GoF)

## Intent
Ensure a class has **exactly one instance** and provide a **global access point** to it.

## When to use (real-world)
Use Singleton when there is a true single “conceptual” instance, such as:
- Application-wide configuration/registry
- Metrics/logging facade (often implemented as a singleton internally)
- A shared resource manager (with careful lifecycle control)

## Trade-offs / pitfalls (important for senior engineers)
- **Hidden dependencies**: global access can hide coupling.
- **Testing**: singletons can be hard to mock; consider interfaces or dependency injection.
- **Thread-safety**: lazy singletons require correct synchronization.
- **Serialization & reflection**: can break “single instance” guarantees if not handled carefully.

## Variants (Java)
1. **Eager initialization**: instance created at class load time.
   - Simple, inherently thread-safe.
   - Might waste resources if never used.
2. **Lazy initialization (synchronized)**: create on first use with synchronization.
   - Thread-safe but synchronization overhead on every call.
3. **Double-checked locking**: reduce sync cost; requires `volatile`.
   - Easy to get wrong.
4. **Enum singleton** (recommended in modern Java):
   - Simple, thread-safe by JVM rules
   - Protects better against serialization/reflection issues

## Structure (conceptual roles)
- `Singleton`: controls instance creation and exposes `getInstance()`
- Clients: call the global accessor

## Java sketch (enum-based, recommended)
```java
public enum Singleton {
    INSTANCE;

    // Example shared state
    private final java.util.concurrent.atomic.AtomicLong counter = new java.util.concurrent.atomic.AtomicLong();

    public long nextId() {
        return counter.incrementAndGet();
    }
}

// Usage:
// long id = Singleton.INSTANCE.nextId();
```

## Resume-friendly takeaway
Singleton is not “just a global variable”; it’s a controlled lifecycle + access pattern. In production, prefer it only when there is a clear single responsibility and mitigate coupling with interfaces or injection when appropriate.

