In C#, an indexer allows an object to be indexed like an array. This means you can access elements of an object using the array-like syntax. Indexers are particularly useful when you want to provide array-like access to a collection of items within a class.
# When to Use Indexers

**Encapsulation:** To encapsulate the internal data structure and provide a more intuitive way to access elements.

**Simplified Syntax:** To simplify the syntax for accessing elements, making the code more readable and maintainable.

**Custom Collections:** When creating custom collection classes that need to provide array-like access to their elements.

# Example
Let’s consider a real-world example where we have a Company class that holds a list of Employee objects. We can use an indexer to access employees by their ID.

# Employee Class
```cs
public class Employee
{
    public int EmployeeId { get; set; }
    public string Name { get; set; }
    public string Gender { get; set; }
    public double Salary { get; set; }
}
```
# Company Class with Indexer
```cs
using System.Collections.Generic;
using System.Linq;

public class Company
{
    private List<Employee> listEmployees = new List<Employee>();

    public Company()
    {
        listEmployees.Add(new Employee { EmployeeId = 101, Name = "Pranaya", Gender = "Male", Salary = 1000 });
        listEmployees.Add(new Employee { EmployeeId = 102, Name = "Preety", Gender = "Female", Salary = 2000 });
        listEmployees.Add(new Employee { EmployeeId = 103, Name = "Anurag", Gender = "Male", Salary = 5000 });
        listEmployees.Add(new Employee { EmployeeId = 104, Name = "Priyanka", Gender = "Female", Salary = 4000 });
        listEmployees.Add(new Employee { EmployeeId = 105, Name = "Hina", Gender = "Female", Salary = 3000 });
    }

    public string this[int employeeId]
    {
        get
        {
            return listEmployees.FirstOrDefault(x => x.EmployeeId == employeeId)?.Name;
        }
        set
        {
            var employee = listEmployees.FirstOrDefault(x => x.EmployeeId == employeeId);
            if (employee != null)
            {
                employee.Name = value;
            }
        }
    }
}
```
# Using the Indexer
```cs
public class Program
{
    public static void Main()
    {
        Company company = new Company();

        // Accessing employee names using the indexer
        Console.WriteLine(company[101]); // Output: Pranaya
        Console.WriteLine(company[102]); // Output: Preety

        // Modifying employee names using the indexer
        company[101] = "Pranay";
        Console.WriteLine(company[101]); // Output: Pranay
    }
}

```