# Equals() vs ==

The Equals method in C# is used to determine whether two object instances are considered equal. It is a fundamental method for comparing objects and is defined in the System.Object class, which means it is available to all objects in C#.
# Key Uses of Equals Method
## Value Comparison:

**For value types** (like int, double, etc.), Equals checks if the values are the same.

**For reference types** (like objects), Equals can be overridden to provide custom equality logic.
**Custom Equality Logic:**

You can override the Equals method in your own classes to define what it means for two instances of your class to be equal.
**Collections and LINQ:**

Equals is often used in collections (like List, Dictionary) and LINQ queries to compare elements.
# Example of Overriding Equals
Here’s an example of how you might override the Equals method in a custom class:
```cs
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public override bool Equals(object obj)
    {
        if (obj == null || !(obj is Person))
            return false;

        Person other = (Person)obj;
        return this.Name == other.Name && this.Age == other.Age;
    }
}
```
# Using Equals Method
Here’s how you can use the Equals method:
```cs
class Program
{
    static void Main()
    {
        Person person1 = new Person { Name = "Alice", Age = 30 };
        Person person2 = new Person { Name = "Alice", Age = 30 };
        Person person3 = new Person { Name = "Bob", Age = 25 };

        Console.WriteLine(person1.Equals(person2)); // True
        Console.WriteLine(person1.Equals(person3)); // False
    }
}
```
# Differences from == Operator
**Equals Method:** Checks for value equality and can be overridden to provide custom equality logic.

**== Operator:** By default, checks for reference equality for reference types (i.e., whether two references point to the same object). For value types, it checks for value equality.

# When to Use Equals
Use Equals when you need to compare the contents or values of objects.
Override Equals in your custom classes to define what it means for two instances to be considered equal.