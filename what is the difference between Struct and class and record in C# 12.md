In C# 12, **classes, structs, and records** serve different purposes and have distinct characteristics. Here’s a detailed comparison to help you understand their differences and when to use each:

**Classes**
**Type:** Reference type.

**Memory Allocation:** Allocated on the heap.

**Mutability:** Mutable by default.

**Inheritance:** Supports inheritance and polymorphism.

**Equality:** Reference equality by default (unless overridden).

**Use Case:** Suitable for complex objects with behavior and state that can change over time.

# Example
```cs
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    public void DisplayInfo()
    {
        Console.WriteLine($"Name: {Name}, Age: {Age}");
    }
}
```
# Structs
**Type:** Value type.

**Memory Allocation:** Allocated on the stack (or inline in containing types).

**Mutability:** Mutable by default, but can be made immutable.

**Inheritance:** Does not support inheritance.

**Equality:** Value equality by default.

**Use Case:** Ideal for small, lightweight objects that are frequently created and destroyed, where performance and memory usage are critical.

# Example
```cs
public struct Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }
}
```
# Records

**Type:** Reference type (record class) or value type (record struct).

**Memory Allocation:** Record class on the heap, record struct on the stack.

**Mutability:** Immutable by default.

**Inheritance:** Record classes support inheritance; record structs do not.

**Equality:** Value equality by default.

**Use Case:** Best for immutable data models, data transfer objects (DTOs), and scenarios where value-based equality is important.

# Example (Record Class)
```cs
public record Person(string Name, int Age);
```
# Example (Record Struct)
```cs
public record struct Point(int X, int Y);
```

# Key Differences

# Type and Memory Allocation:
**Class:** Reference type, heap allocation.

**Struct:** Value type, stack allocation.

**Record:** Can be either reference type (record class) or value type (record struct).

# Mutability:
**Class:** Mutable by default.

**Struct:** Mutable by default, but can be made immutable.

**Record:** Immutable by default.

# Inheritance:
**Class:** Supports inheritance and polymorphism.

**Struct:** Does not support inheritance.

**Record:** Record classes support inheritance; record structs do not.

# Equality:
**Class:** Reference equality by default.

**Struct:** Value equality by default.

**Record:** Value equality by default.

# When to Use Each
**Class:** Use when you need a complex object with behavior, state changes, and inheritance.

**Struct:** Use for small, lightweight objects where performance and memory efficiency are crucial.

**Record:** Use for immutable data models and scenarios where value-based equality is important, such as DTOs and data containers.