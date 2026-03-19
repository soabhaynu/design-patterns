# Prototype (GoF)

## Intent
Create new objects by **copying an existing instance** (cloning/prototyping) instead of creating from scratch.

## When to use (real-world)
Use Prototype when:
- Creating an object is **expensive** (heavy initialization, costly setup).
- You need many **similar** objects with small differences.
- You want to avoid tight coupling to constructors (e.g., “copy a template”).

## Trade-offs / pitfalls (important for senior engineers)
- **Shallow vs deep copy**: ensure correct copying of nested/mutable fields.
- **Maintenance risk**: every field must be included in the copy logic.
- **Hidden shared state**: a bad clone can accidentally share mutable references.

## Structure (conceptual roles)
- `Prototype`: defines a `clone`/`copy` operation.
- `ConcretePrototype`: implements copying behavior for a specific type.
- `Client`: requests copies instead of constructing new objects directly.

## Java sketch (copy via interface)
```java
public interface Prototype<T> {
    T copy();
}

public final class UserProfile implements Prototype<UserProfile> {
    private final String userId;
    private final java.util.Map<String, String> attributes; // mutable -> must copy deeply

    public UserProfile(String userId, java.util.Map<String, String> attributes) {
        this.userId = userId;
        this.attributes = attributes;
    }

    @Override
    public UserProfile copy() {
        // Deep copy map to avoid shared mutable state between clones
        return new UserProfile(userId, new java.util.HashMap<>(attributes));
    }
}

// Usage:
// UserProfile p1 = ...
// UserProfile p2 = p1.copy();
```

## Common variants in Java
- **Prototype registry**: keep a map of named templates and copy from the registry.
- **Copy constructor**: `new MyType(existing)` is often a practical “prototype-like” approach.

## Resume-friendly takeaway
Prototype is a high-leverage pattern when object creation is costly or you need rapid creation of similar objects. The key is correctness of copy semantics (deep copy when needed).

## References (read more)
- [Wikipedia: Prototype pattern](https://en.wikipedia.org/wiki/Prototype_pattern)

