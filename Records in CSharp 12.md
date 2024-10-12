# C# Record

# Introduction to C# record
C# record provides built-in functionality for encapsulating data, making it easy to work with **immutable and strong-typed data**.

**Records are immutable by default**. It means that you cannot mutate (or change) their property values once created.

Records have built-in support for **value-based equality checking**, meaning that **two records with the same values are equal**.

Records provide default formatting, which can be customized by overriding the ToString() method.

# Defining a Record
To define a record, you use the record keyword with its properties:

`record RecordName(type property1, type property2, ..);`

The following example demonstrates how to define a Person record with three properties FirstName, LastName, and Age:

``` cs
public record Person(string FirstName, string LastName, int Age);
```
# Creating a Record object
To create a new instance of a record, you can use the new keyword followed by the name of the record and provide the values for its properties. For example:

```cs
var person = new Person("John", "Doe", 22);
```
In this example, we created a new Person record with the values "John" for the FirstName property, "Doe" for the LastName property, and 22 for the Age property.

# Immutability
Records are immutable by default. The following attempts to change the Age of the person record and cause a compiled error:
```cs
var person = new Person("John", "Doe", 22);
person.Age = 25; // ERROR

public record Person(string FirstName, string LastName, int Age);
```
# Nondestructive mutation
If you want to copy a record with some modifications, you can use the with expression. This is called a non-destructive mutation.

The with expression copies an existing record, with specified properties changed. For example:
```cs
var person = new Person("John", "Doe", 22);
var person2 = person with
{
    FirstName = "Jane",
    Age = 20
};
Console.WriteLine(person2);

public record Person(string FirstName, string LastName, int Age);
```
Output:
```plaintext
Person { FirstName = Jane, LastName = Doe, Age = 20 }
```
In this example, we use the with expression to copy the person record and change the FirstName and Age properties using the object initializer syntax to specify the values to be changed.

# Value-based equality checking
Records have built-in value-based equality checking, which means that two records with the same values are considered equal.

For example, if you create two Person records with the same values, they are equal:
```cs
using static System.Console;

var person1 = new Person("John", "Doe", 30);
var person2 = new Person("John", "Doe", 30);
WriteLine(person1 == person2); // True

public record Person(string FirstName, string LastName, int Age);
```
Output:
```php
True
```
# Deconstruction record properties
You can deconstruct a record into its constituent properties. For example:
```cs
using static System.Console;

var person = new Person("John", "Doe", 2);
var (FirstName, LastName, Age) = person;
WriteLine($"FirstName: {FirstName}, LastName: {LastName}, Age: {Age}");
public record Person(string FirstName, string LastName, int Age);
```
Output:
```plaintext
FirstName: John, LastName: Doe, Age: 22
```
# Formatting
Records have built-in formatting capabilities that allow you to specify how they should be displayed as a string. Also, you can get a string representation of the record’s values by using the ToString() method:
```cs
using static System.Console;

var person = new Person("John", "Doe", 22);
WriteLine(person);
public record Person(string FirstName, string LastName, int Age);
```
Output:
```php
Person { FirstName = John, LastName = Doe, Age = 22 }
```
By default, the ToString() method uses the record’s name followed by its property names and values. In case you want to customize the formatting, you can override the ToString() method like this:
```cs
using static System.Console;
var person = new Person("John", "Doe", 22);
WriteLine(person);
public record Person(string FirstName, string LastName, int Age)
{
    public override string ToString()
        => $"({FirstName},{LastName},{Age})";
}
```
Output:
```php
(John,Doe,22)
```
# Defining mutable records
It’s possible to define a mutable record. For example:
```cs
using static System.Console;
var person = new Person { 
    FirstName = "John", 
    LastName = "Doe", 
    Age = 22 
};
person.Age = 25; // OK
person.LastName = "Smith"; // OK
WriteLine(person );
public record Person
{
    public string FirstName { get; set;}
    public string LastName  { get; set;} 
    public int Age { get; set;}
}
```
Output:

Person { FirstName = John, LastName = Smith, Age = 25 }

# C# Record applications
In practice, you can use the C# record in the following scenarios:

**API response models:** you can use records to represent response models in RESTful APIs. In this case, you can define the record with the properties that correspond to the data being returned by the API. Records help deserialize the response into a strongly-typed object easily and work with the data more simply.

**Configuration settings:** you can use records to represent configuration settings for an application. In this case, you define a record with the properties that correspond to the various settings of the application. This allows you to pass the settings around between methods and services easily while enforcing the immutability of the settings.

**Domain models:** you can use records to represent domain models in an application. In this scenario, you define a record with properties that correspond to the data being modeled. Records allow you to easily work with the data in a strongly-typed and immutable way. Also, you can take advantage of the built-in equality checking and formatting capabilities of records.

# Summary
C# record is a reference type that provides built-in functionality for encapsulating data.
Use C# records in API response models, configuration settings, and domain models.