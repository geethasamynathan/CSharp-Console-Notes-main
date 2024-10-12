
# Serialization

**Serialization** in C# is the process of **converting an object into a format** that can be easily stored or transmitted. This format can be a **binary, XML, or JSON** representation of the object. The primary purpose of serialization is to save the state of an object so that it can be recreated later, which is known as deserialization.
# When to Use Serialization
Serialization is useful in various scenarios, such as:

**Persisting Data:** Saving the state of an object to a file or database.

**Data Transfer:** Sending objects over a network, such as in web services or remote method calls.

**Caching:** Storing objects in memory for quick access.

**Cloning:** Creating a deep copy of an object.

# Example: JSON Serialization

## Step 1: Define the Class to Serialize
```cs
public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
    public decimal Price { get; set; }
}
```

# Step 2: Serialize the Object to JSON
```cs
using System;
using System.Text.Json;

class Program
{
    static void Main()
    {
        Product product = new Product { Id = 1, Name = "Laptop", Price = 1000m };

        // Serialize the object to JSON
        string jsonString = JsonSerializer.Serialize(product);
        Console.WriteLine("Serialized JSON: " + jsonString);

        // Save JSON to a file
        System.IO.File.WriteAllText("product.json", jsonString);
    }
}

```
# Step 3: Deserialize the JSON to an Object
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Text.Json;
namespace SerializationDemo
{
    internal class Program
    {
        static void Main(string[] args)
        {
            //Product product = new Product { Id = 1, Name = "Laptop", Price = 78000 };
            //Console.WriteLine($"Before serialization = {product}");
            //string jsonString=JsonSerializer.Serialize(product);
            //Console.WriteLine($"Serialized Json ={jsonString}");
            //File.WriteAllText(@"D:\Test yantra\Batch 1\M1\product.json", jsonString);
            ////File.WriteAllText("products.json", jsonString);

            // Read JSON from a file
            string jsonString1 = System.IO.File.ReadAllText("product.json");

            // Deserialize the JSON to an object
            Product product1 = JsonSerializer.Deserialize<Product>(jsonString1);
            Console.WriteLine($"Deserialized Product: {product1.Name}, Price: {product1.Price}");
        }
    }
}

```
# Example: Binary Serialization is obsolete in .Net 5 and above version .so go with Json and xml serialization

# example for XML Serialization
## Step 1: Define the Class to Serialize
```cs
 [Serializable]
 public class Product
 {
     public int Id { get; set; }
     public string  Name { get; set; }
     public double Price { get; set; }
 }

```
# Step 2: Serialize the Object to XML
```cs
program.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Xml.Serialization;
namespace SerializationDemo
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Product product = new Product { Id = 1, Name = "Laptop", Price = 78000 };
            string filePath = @"D:\Test yantra\Batch 1\M1\product.dat";
            XmlSerializer serializer = new XmlSerializer(typeof(Product));
            using (FileStream fs = new FileStream(filePath, FileMode.Create))
            {
                serializer.Serialize(fs, product);
            }
            Console.WriteLine("Product serialized to XML format.");
        }
    }
}
```

# Step 3: Deserialize the XML to an Object

program.cs
```cs
string filePath = @"D:\Test yantra\Batch 1\M1\product.dat";
XmlSerializer serializer = new XmlSerializer(typeof(Product));
using (FileStream fs = new FileStream(filePath, FileMode.Open))
{
    Product product = (Product)serializer.Deserialize(fs);
    Console.WriteLine($"Deserialized Product:Id= {product.Id} Name= {product.Name}, Price: {product.Price}");
}
```