# Builder (GoF)

## Intent
Construct a complex object step-by-step while keeping the construction process separate from the final representation.

## When to use (real-world)
Builder is a strong fit when:
- You have many optional parameters (constructor becomes unreadable)
- You want immutability for the final object
- You need different representations/variations from the same construction steps

Typical examples:
- UI configuration objects
- Requests with optional headers/params
- Complex domain objects (e.g., `Order`, `Invoice`, `Report`)

## Trade-offs / pitfalls
- More classes/abstraction than a plain constructor.
- If builders become too “smart”, they can hide business rules; keep validation/constraints clear.

## Structure (conceptual roles)
- `Builder`: interface that defines building steps
- `ConcreteBuilder`: maintains intermediate state and produces the `Product`
- `Product`: the complex object being built
- `Director` (optional): orchestrates the building steps

In Java, many teams implement “Builder” with a nested static builder class (and often skip `Director` unless needed).

## Java sketch (classic builder)
```java
public final class Meal {
    private final String bread;
    private final String filling;
    private final boolean toasted;

    private Meal(Builder b) {
        this.bread = b.bread;
        this.filling = b.filling;
        this.toasted = b.toasted;
    }

    public static class Builder {
        private String bread;
        private String filling;
        private boolean toasted;

        public Builder bread(String bread) {
            this.bread = bread;
            return this;
        }

        public Builder filling(String filling) {
            this.filling = filling;
            return this;
        }

        public Builder toasted(boolean toasted) {
            this.toasted = toasted;
            return this;
        }

        public Meal build() {
            // Minimal example validation:
            if (bread == null || filling == null) {
                throw new IllegalStateException("bread and filling are required");
            }
            return new Meal(this);
        }
    }
}

// Usage:
// Meal meal = new Meal.Builder()
//     .bread("wheat")
//     .filling("cheese")
//     .toasted(true)
//     .build();
```

## Resume-friendly takeaway
Builder turns a fragile “telescoping constructor” into a readable, maintainable construction API. It’s especially valuable in large systems where objects grow over time with new optional fields.

