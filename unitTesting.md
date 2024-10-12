# Nunit Test in C#
# What is Unit Testing?
Unit test is an automated test written and run by the developer to ensure that a piece of an application behaves as intended. Usually, unit tests cover the smallest logic unit of an application, and it helps developers to be sure that the application’s pieces work correctly. 

A single unit test has a proper structure – well-known as triple A. **Arrange, Act, Assert.** It helps to identify what happens inside the test case. 

Let’s take a look at the test case where we have triple-A separation: 
```cs
public void WhenCallPlusWithTwoOperands_ThenItSumsValues()
{
    // Arrange
    var a = 1;
    var b = 2;

    var expected = 3;

    // Act
    var sum = a + b;

    // Assert
    Assert.AreEqual(sum, expected);
}
```
This test case verifies that operator + correctly sums two operands a and b. To keep the assertion part as simple as possible, we should define the expected value in the Arrange part. 

The test case in our example verifies the result. But also, we can be interested in verifying a component interaction.

# Test Method Naming Convention
The most important part of the development and unit testing is a proper naming convention. The name of the unit test should reflect what we are trying to test and the conditions for the test case. 

Let’s take a look at one of the commonly used naming conventions:

`[GivenX]_When[Y]_Then[Z]`

It starts with an optional “Given” part that gives some context to the test, after which we describe some action that needs to be done in the “When” part. Finally, we describe what we expect to happen for a particular test case in the “Then” part of the method name.

# Test Project and Files Naming Convention 
It’s common good practice to keep separate test projects for each business project inside the solution. So if our solution has a business project named Project.Business than test’s project name should be Project.Business.UnitTests.

We use a proper suffix to show the intention of tests. For functional tests, the name would be Project.Business.FunctionalTests.

We should keep the same structure that we have in our business project. Each class we cover with tests should have a test class in the test project named accordingly with Test suffix. 

# NUnit Project Setup
Let’s define the simplest business logic class that we are going to test in this article. We are going to create a  NUnitProject project with a single Calculator class that has just one method, Divide. It’s enough for our purposes:
```cs
public class Calculator
{
    public double Divide(int a, int b)
    {
        return a / b;
    }
}
```

The next step would be to add a test project to the solution. We should rely on the naming convention and name it NUnitProject.UnitTests. It’s a simple class library. Also, we are going to add the reference from the main project to the testing project. 

Now it’s time to add the required NuGet packages. 

 Let’s run the command to install the NUnit package in the Test project:

# First Test Case 
Now when we have the test project ready, we can start covering the Calculator class with unit tests. 

Let’s define a simple test case to verify that the Divide method works properly:
```cs
[Test]
public void WhenDivideTwoNumbers_ThenReturnDivisionOfTwoNumbers()
{
    // Arrange
    var a = 300;
    var b = 100;

    var expected = 3;
    var calculator = new Calculator();

    // Act
    var actual = calculator.Divide(a, b);

    // Assert
    Assert.AreEqual(expected, actual);
}
```
To mark a method as a test case, we need to add a Test attribute. It tells the NUnit framework that it should run this method.

We can run all tests in a solution using Visual Studio with a few simple steps: 

TopMenu -> Tests -> Run All Tests, with a shortcut Ctrl R + T, or from the console – navigate to the test project directory and run the command:

`dotnet test`

It’s a good approach to run our test methods with different arguments, without copy-pasting our test methods. We can define test method parameters by using the [TestCase] attribute.

The [TestCase] attribute allows us to provide params for the test method:
```cs
[TestCase(300,100, 3)]
[TestCase(400, 200, 2)]
public void WhenDivideTwoNumbers_ThenReturnDivisionOfTwoNumbers(int a, int b, double expected)
{
    // Arrange
    var calculator = new Calculator();

    // Act
    var actual = calculator.Divide(a, b);

    // Assert
    Assert.AreEqual(expected, actual);
}
```
The [TestCase] attribute allows only constant values for params, but we can find ourselves in a situation where we need to create a value on the fly.

# Providing a Source With the TestCaseSource Attribute
We can solve this by using the [TestCaseSource] attribute. It accepts the name of the static method or property, which provides values for the test method:
```cs
[TestCaseSource(nameof(SourceProvider))]
public void WhenDivideTwoNumbers_ThenReturnDivisionOfTwoNumbersProvidedBySource(int a, int b, double expected)
{
    // Arrange
    var calculator = new Calculator();
    // Act
    var actual = calculator.Divide(a, b);

    // Assert
    Assert.AreEqual(expected, actual);
}

public static IEnumerable<int[]> SourceProvider()
{
    yield return new int[] { 300, 100, 3 };
    yield return new int[] { 400, 200, 2 };
}
```
Now, we face the problem of creating a calculator instance inside each test method. NUnit provides a convenient way to execute a piece of code before all test methods or before each test method run. 

With the [Setup] attribute, we can execute a method before each test case run, and we can create a Calculator class instance inside this method:
```cs
private Calculator _calculator;
[SetUp]
public void Setup()
{
    _calculator = new Calculator();
}
```
We have another attribute that runs just once before all test cases run. It’s named OneTimeSetup. 

It depends on what kind of resources we are going to set up before test case execution. Sometimes we have a strict restriction to use a single instance of an object between all test cases and using the OneTimeSetup method to create such an object is the best option.

Also, we have replacements for the Setup attributes that we can use to execute code after the test case is finished. The attributes as TearDown and, accordingly, OneTimeTearDown give us such ability. 

# Unit Test Metadata
In a huge project, we can end up with a very large number of unit tests. In that case, we can use additional metadata attributes to add information to our unit tests.

Later we can run tests relying on specific values provided by metadata attributes. 

# Author
Test framework can’t check git history and determine the author of a test. To do that, we need to mark the test method with the [Author] attribute:
```cs
[Author("Geetha")]
[Test]
public void WhenHasAuthor_ThenCanAccessItInCode()
{
    var expected = "Geetha";
    // Act
    var author = (string)TestContext.CurrentContext.Test.Properties.Get("Author");
    // Assert
    Assert.AreEqual(author, expected);
}
```

# Description
If the intention of the test case is not clear, it’s possible to provide additional descriptions to clarify what exactly is tested inside the test case. It’s helpful when we run tests automatically and give the test framework additional information to display in the log message:
```cs
[Test]
[Description("this is simple test case")]
public void WhenHaveDescription_ThenItsEasierToGetWhatItTests()
{
    //test logic
}
```

# MaxTime
In some cases, we need to verify that method works fast enough. We can use [MaxTime] attribute to specify a maximum time for a test case to succeed. When the method exceeds the defined time it fails with a proper explanation:
```cs
[MaxTime(1000)]
public async Task WhenTakesMoreTime_ThenItFails()
{
     await Task.Delay(1100);

     // Assert
     Assert.IsTrue(true);
}
```
# Category
The [Category] attribute marks that test related to a specific feature, and it allows us to run a set of unit tests for the feature without running all other tests. 

In huge projects, this saves a lot of time to run just a few tests for a new feature instead of running thousands of existing tests:
```cs
[Test]
[Category("simple_tests")]
public void WhenHaveCategory_ThenItCanBeInvokedWithCategoryFilder()
{
    //test logic
}
```

# Final Example
```cs
internal class MathOperationTest
{
    [TestFixture]
    [Category("MathOperations")]
    [Author("geetha", "geethasamynathan2011@gmail.com")]
    public class MathOperationsTests
    {
        private Calculator _mathOperations;

        [OneTimeSetUp]
        public void OneTimeSetUp()
        {
            Console.WriteLine("OneTimeSetUp: Executed once before all tests.");
        }

        [SetUp]
        public void SetUp()
        {
            _mathOperations = new Calculator();
            Console.WriteLine("SetUp: Executed before each test.");
        }

        [TearDown]
        public void TearDown()
        {
            Console.WriteLine("TearDown: Executed after each test.");
        }

        [OneTimeTearDown]
        public void OneTimeTearDown()
        {
            Console.WriteLine("OneTimeTearDown: Executed once after all tests.");
        }

        [Test]
        [Description("Test for Add method")]
        [TestCase(1, 2, 3)]
        [TestCase(-1, -1, -2)]
        [TestCase(0, 0, 0)]
        public void Add_WhenCalled_ReturnsSum(int a, int b, int expectedResult)
        {
            var result = _mathOperations.Add(a, b);
            Assert.AreEqual(expectedResult, result);
          //  (Or with 4.0 version of NunitTestAdapter)
          Assert.That(result, Is.EqualTo(expectedResult));
        }

        [Test]
        [Description("Test for Divide method")]
        [TestCase(4, 2, 2)]
        [TestCase(10, 5, 2)]
        [MaxTime(1000)]
        public void Divide_WhenCalled_ReturnsQuotient(int a, int b, int expectedResult)
        {
            var result = _mathOperations.Division(a, b);
            Assert.AreEqual(expectedResult, result);
        }

        [Test]
        [Description("Test for Divide method with zero divisor")]
        public void Divide_WhenDivisorIsZero_ThrowsDivideByZeroException()
        {
            Assert.Throws<DivideByZeroException>(() => _mathOperations.Division(1, 0));
        }
    }
    ```