# difference between sortedlist generic and non-generic
-----------------------------------------------------
Choosing between a generic SortedList<TKey, TValue> and a non-generic SortedList in C# depends on your specific needs for type safety, performance, and flexibility. Here are some guidelines:

# Generic SortedList<TKey, TValue>
**When to use:**

You need type safety to ensure that all keys and values are of specific types.
You want better performance, as generic collections generally perform faster due to type safety and reduced boxing/unboxing.
You prefer compile-time type checking to catch errors early.
Example:
```cs
SortedList<int, string> sortedList = new SortedList<int, string>();
sortedList.Add(1, "One");
sortedList.Add(2, "Two");
sortedList.Add(3, "Three");
```
# Non-Generic SortedList
You need to store elements of different types in the same collection.
You are working with legacy code that already uses non-generic collections.
You don’t need the type safety provided by generics.
```cs
SortedList sortedList = new SortedList();
sortedList.Add(1, "One");
sortedList.Add("Two", 2);
sortedList.Add(3.0, "Three");
```
# Key Differences
Type Safety: Generic SortedList<TKey, TValue> provides type safety, while non-generic SortedList does not.
Performance: Generic collections are generally faster due to the absence of boxing/unboxing and type casting1.
Flexibility: Non-generic collections offer more flexibility in terms of storing different types of objects

# When to use which collection:
-----------------------------
# 1. ArrayList
**When to use:** Use ArrayList when you need a collection that can store elements of different types and you don’t need type safety.
Example:
```cs

ArrayList arrayList = new ArrayList();
arrayList.Add(1);
arrayList.Add("Hello");
arrayList.Add(true);
 ```
# 2. SortedList
**When to use:** Use SortedList when you need a collection of key/value pairs that are sorted by the keys and you need to access elements by key or index.
Example:
```cs
SortedList sortedList = new SortedList();
sortedList.Add(2, "Two");
sortedList.Add(1, "One");
sortedList.Add(3, "Three");
 ```
# 3. Hashtable
**When to use:** Use Hashtable when you need a collection of key/value pairs that can store elements of different types and you don’t need type safety.
```cs

Hashtable hashtable = new Hashtable();
hashtable.Add(1, "One");
hashtable.Add("Two", 2);
hashtable.Add(true, "True");
 ```
# 4. Dictionary
**When to use:** Use Dictionary<TKey, TValue> when you need a collection of key/value pairs with type safety and better performance.
Example:
```cs
Dictionary<int, string> dictionary = new Dictionary<int, string>();
dictionary.Add(1, "One");
dictionary.Add(2, "Two");
dictionary.Add(3, "Three");
 ```
# 5. Stack
When to use: Use Stack when you need a last-in, first-out (LIFO) collection.
```cs
Stack stack = new Stack();
stack.Push(1);
stack.Push(2);
stack.Push(3);
var top = stack.Pop(); // top is 3
 ```
# 6. Queue
**When to use:** Use Queue when you need a first-in, first-out (FIFO) collection.
Example:
```cs
Queue queue = new Queue();
queue.Enqueue(1);
queue.Enqueue(2);
queue.Enqueue(3);
var front = queue.Dequeue(); // front is 1
 ```
# 7. List
**When to use:** Use List<T> when you need a collection that provides type safety, dynamic resizing, and better performance.
Example:
```cs
List<int> list = new List<int>();
list.Add(1);
list.Add(2);
list.Add(3);
 ```
