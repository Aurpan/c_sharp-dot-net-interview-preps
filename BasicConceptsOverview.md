# OOP Concepts

## 1. Encapsulation
- Bundling of data and methods in a single unit, which is called class.
- Do not need to expose everything to the public space. It is achieved through ‘**Access Modifiers**’ and ‘**getter-setter**’ methods
    
    ### Access Modifiers:  
    - **Public:** can be accessed by all
    - **Private:** can only be access by anyone within the same class
    - **Protected:** can only be accessed by anyone in the class, or only from child class (*parent can’t access protected prop of child*)
    - **Internal:** can be access within the same assembly
    - **Protected Internal:** accessible within same assembly or derived class

## 2. Abstraction
- Hiding implementation details and showing only functionality to the user.
- Can be achieved through **Interface** or **Abstract Class**.

## 3. Inheritance
- Allows a class to inherit attributes and methods from another class.
- Parent can hold child’s reference, not vice-versa.

```csharp
Parent parent = new Child() // this is correct

Child child = new Parent() // this is error
```

- Base class constructor is always called first.
- Constructor of the parent class is never inherited. Base class constructor needs to be manually called.

```csharp
public class Employee
{
    private int _age;

    public Employee(int age)
    {
        _age = age;
    }
}

public class Manager : Employee
{
    public Manager(int age)
        : base(age){}       // base class constructor is called manually
}
```

### Upcasting

 putting a derived class object to base class reference

```csharp
Employee empManager = new Manager(); // Employee class is inherited by Manager class
```

### Downcasting

putting base class object into derived class reference

```csharp
Manager manager = new Employee(); // compile error

Manager manager1 = (Manager)employee; // correct
Manager manager2 = employee as Manager; // correct
```

‘**as**’ keyword can be used for casting one object to another.

‘**is**’ keyword is used to check the object type. It return bool value.

```csharp
if (manager1 is Manager)
{
		// do something
}
```

### Boxing-Unboxing

- **Boxing:** converting a value type instance to an object reference (upcasting)
- **Unboxing:** casting object reference to value type (downcasting)

```csharp
// Boxing
int age = 50;
object obj = age;
object numbObj = 50;

// Unboxing
object numbObj = 50;
int age = (int)numbObj;
```

## 4. Polymorphism

- Ability of a single interface (like a method or object) to behave differently based on the underlying actual type.
- it allows a method or object to have multiple forms
    
    ### Overloading:
    
    - method with same name but different signature (diff. return type, diff. parameters)
    
    ### Overriding:
    
    - method with same name and same signature in the derived classes, but different implementation
    
    ### **Why use ‘virtual’ and ‘override’ keyword?**
    
    Let’s assume ‘**Manager**’ class inherits ‘**Employee**’ class and both the class has ‘**CalculateSalary**’ method and there is no **virtual** or **override** keyword is used. Now, when Manager object is upcasted to Employee reference, it will invoke the Employee.CalculateSalary() method, not Manager.CalculateSalary() method.
    
    ```csharp
    public class Employee
    {
        public void CalculateSalary()
        {
            Console.WriteLine("This is the Salary of the Employee!");
        }
    }
    
    public class Manager : Employee
    {
        public void CalculateSalary()
        {
            Console.WriteLine("This is the Salary of the Manager!");
        }
    }
    
    internal class Program
    {
        static void Main(string[] args)
        {
            Employee employee = new Manager();
            employee.CalculateSalary();
        }
    }
    
    // output: This is the Salary of the Employee!
    ```
    
    But when **virtual** is used, it will invoke the Manager.CalculateSalary() method.
    
      
    
    ```csharp
    public class Employee
    {
        public virtual void CalculateSalary()
        {
            Console.WriteLine("This is the Salary of the Employee!");
        }
    }
    
    public class Manager : Employee
    {
        public override void CalculateSalary()
        {
            Console.WriteLine("This is the Salary of the Manager!");
        }
    }
    
    internal class Program
    {
        static void Main(string[] args)
        {
            Employee employee = new Manager();
            employee.CalculateSalary();
        }
    }
    
    // output: This is the Salary of the Manager!
    ```
<br><br><br>

# Modifiers (Abstract, Sealed, Static)

## Abstract Modifier

- can be used with Methods or Classes
- an Abstract Method doesn’t have an implementation (no body), only declaration
- if even a single class is Abstract, the whole class needs to be Abstract
- child classes are forced to implement that method
- no instance can be created for Abstract class

## Sealed Modifier

- can be used with Methods or Classes
- it prevents classes from being inherited and methods from being overridden
- if applied to a method, the whole class can be inherited, just the method can’t be overridden

## Static Modifiers

- ‘static’ keyword can be used with property, method and class
- when this keyword is used with property or method, that is then only belong to Class itself. No object of that class has ownership.

```csharp
Employee emp = new ();
emp.Name = "Aurpan" // if 'Name' is a static property, it will show error

// This is the correct way to access static property, Name
Employee.Name = "Aurpan";
```

- can’t access non-static props from static methods; but can access static props from non-static methods

### Static Class

- can’t create instance/object, can’t be inherited
- all the props and methods inside static class must be static
- constructor of a class can be static. A static constructor can’t have a **Access Modifier** (see example below). This static constructor is invoked automatically by CLR when any static property or method is accessed.

```csharp
public class TestStatic
{
    public string FirstName { get; set; }
    public static string LastName { get; set; }
    public static int StaticVal { get; set; }
    public static int StaticVal2 { get; set; }
    public int NonStaticVal { get; set; }

    static TestStatic() // static constructor - no Access Modifier
    {
        StaticVal2++;
        NonStaticVal++; // will show error - can't use any non-static props or method inside static constructor
    }
    public TestStatic()
    {
        NonStaticVal++;
        StaticVal2++; 
    }
}
```

> **doesn’t matter how many times we access any static property or method, the static constructor is invoked only once.**

<br><br><br>

# Variable Types

## 1. Value Type

- stored in stack
- limited amount of space is allocated against each value type variable
- short life. Can’t be used outside the scope
- Example: int, byte, bool, char, struct …….

## 2. Reference Type

- stored in a heap
- unlimited amount of memory
- Example: String, Array, Object, Class ……

 

# Parameter Types

## 1. Ref

variable will behave like reference type and become **mutable** (mutable - can be modified; immutable - can’t be modified)

```csharp
static void Main(string[] args)
{
    int num = 5;
    Increment(ref num);

    Console.WriteLine(num);
}

public static void Increment(ref int num)
{
    num++;
}

// Output: 6
```

Here, the num variable is modified inside ‘Increment’ method.

## 2. Out

Works similar to ‘ref’, but needs to be initialized inside the method.

```csharp
static void Main(string[] args)
{
    int num = 5;
    Decreament(out num);

    Console.WriteLine(num);
}

public static void Decreament(out int num)
{
    num = 10; // Must initialize before use
    num--;
}

// Output: 9
```

<br><br><br>

# Getter-Setter Method

getter and setter (get-set) methods provides a control for handling the setting of data and fetching of data from outside of the class.

```csharp
public class Employee
{
    private int days;

    public void Salary()
    {
        Console.WriteLine($"Salary: {1000 * days}");
    }

    public int WorkDays
    {
        get { return days; }
        set 
        {
            if (value > 25)
                days = 25;
            else 
                days = value;
        }
    }
}
```

<br><br><br>
# Generics

```csharp
// generic class
public class GenericExample<T> where T : IComparable, new()
{}

// generic method
public T GetMaxValue<T>(T val1, T val2)
{}
```

with ‘where’, we put constrain on the T. 

There can be 5 types of constrains:

- where T : IComparable (any interface)
- where T : Product (any class or sub classes)
- where T : struct (value type)
- where T : class (reference type)
- where T : new() (an object who has default constructor)

<br><br><br>

# Delegates

- an object that can call a method
- it can carry reference of a method (similar to js)
- delegates are classes derived from System.MulticastDelegate. Has 2 public property, **Target** & **Method**

```csharp
public class DemoDelegate
{
    public delegate int MathOperation(int a, int b); // declaration of a delegate

    public void Calculator(int a, int b, MathOperation operation) // takes a delegate as perameter
    {
        int result = operation(a, b);
        Console.WriteLine($"Result: {result}");
    }
}

internal class Program
{
    static void Main(string[] args)
    {
		    DemoDelegate.MathOperation calculationTask = Add;
		    
        DemoDelegate demo = new DemoDelegate();
        demo.Calculator(10, 5, calculationTask);
    }

    public static int Add(int a, int b)
    {
        return a + b;
    }
}
```

**‘Action’** and **‘Func’** both are generic delegates provided by .NET

```csharp
public class DemoDelegate
{
    public void Calculator(int a, int b, Func<int, int, int> operation) // delegate is replaced with Func<in, in, out>
    {
        int result = operation(a, b);
        Console.WriteLine($"Result: {result}");
    }
}

internal class Program
{
    static void Main(string[] args)
    {
		    Func<int, int, int> operation = (a, b) => a + b;
		    
        DemoDelegate demo = new DemoDelegate();
        demo.Calculator(10, 5, operation );
    }
}
```

> Difference in **Func** and **Action:**
Func has the last parameter to be OUT variable. So, Func returns something. But Action returns void
> 

## Use Case

```jsx
public static bool MyAny<T>(this IEnumerable<T> source, Func<T, bool> predicate)
{
    if (source == null) throw new ArgumentNullException();

    foreach (var item in source)
    {
        if (predicate(item)) return true;
    }

    return false;
}
```

> this extension method works similar to List.Any()
>

<br><br><br>

# Events

- way of invoking multiple methods on specific conditions. Similar to notification.
- Publisher - Subscriber model: Publisher publish an event and different class (user) subscribe to it.
- must use a delegate with it. Event is a wrapper on to of delegate.

The event can be created in many ways. Here are some examples

**EventHandler:** it is delegate itself

```csharp
public class Account
{
    public event EventHandler<decimal>? BalanceLow; // publishing event  

    public decimal AccountBalance { get; set; } = 20;
    public decimal LowBalanceThreshold { get; set; } = 10;

    public void Withdraw(decimal amount)
    {
        if (amount > AccountBalance)
            throw new InvalidOperationException("Insufficient funds.");

        AccountBalance -= amount;
        Console.WriteLine($"Withdraw amount is {amount}");

        if (AccountBalance < LowBalanceThreshold) 
            BalanceLow?.Invoke(this, LowBalanceThreshold); // raise event if balance is low
            // BalanceLow?.Invoke(this, EventArgs.Empty); => for non-generic EventHandler
    }
}

internal class Program
{
    static void Main(string[] args)
    {
        Account account = new Account();
        account.BalanceLow += OnBalanceLow; // subscribing to the event
        account.Withdraw(11);
    }

    private static void OnBalanceLow(object? sender, decimal threshold)
    {
        Console.WriteLine($"Warning: Your account balance is less than {threshold}!");
    }
}
```

**Action and Delegate**

```csharp
public class Account
{
    public delegate void BalanceLowEventHandler(decimal lowBalanceThreshold); // delegate definition
    public event BalanceLowEventHandler? BalanceLow; // publishing event with custom delegate 
    // OR
    public event Action<decimal>? BalanceLow; // publishing event with system provided delegate - Action

    public decimal AccountBalance { get; set; } = 20;
    public decimal LowBalanceThreshold { get; set; } = 10;

    public void Withdraw(decimal amount)
    {
        if (amount > AccountBalance)
            throw new InvalidOperationException("Insufficient funds.");

        AccountBalance -= amount;
        Console.WriteLine($"Withdraw amount is {amount}");

        if (AccountBalance < LowBalanceThreshold) 
            BalanceLow?.Invoke(LowBalanceThreshold); // raise event if balance is low  
    }
}

internal class Program
{
    static void Main(string[] args)
    {
        Account account = new Account();
        account.BalanceLow += OnBalanceLow; // subscribing to the event
        account.Withdraw(11);
    }

    public static void OnBalanceLow(decimal threshold)
    {
        Console.WriteLine($"Warning: Your account balance is less than {threshold}!");
    }
}
```

> must unsubscribe after use, otherwise memory leakage might happen.
> 

```csharp
// unsubscribe event
account.BalanceLow -= OnBalanceLow;
```

<br><br><br>
# Lambda Expression

**Format: args = > {expressions}**

```csharp
static void Main(string[] args)
{
    DemoDelegate.MathOperation calculationTask = Add;
    // OR, it can be written like this with Lambda:
    DemoDelegate.MathOperation calculationTask = (num1, num2) => num1 + num2; // no need for separate Add method
    
    DemoDelegate demo = new DemoDelegate();
    demo.Calculator(10, 5, calculationTask);
}

public static int Add(int a, int b)
{
    return a + b;
}
```
**Predicate:** method which return bool value.

<br><br><br>

# IEnumerable & IQueryable

```csharp
// IEnumerable
IEnumerable<Customer> enumerableCustomers = GetCustomer(); // already fetches all data; takes huge memory
var filteredCustomers = enumerableCustomers.Where(c => c.Age > 40); 

// IQueryable
IQueryable<Customer> queryableCustomers = GetCustomer(); // fetches zero data;
var filteredCustomers = queryableCustomers .Where(c => c.Age > 40); // still doesn't fetch the data
var data = filteredCustomers.ToList(); // now fetches data
```

<br><br><br>

# Mutable- Immutable

**Mutable:** An object is mutable if its state (data/fields/properties) can be changed after it is created.

```csharp
public class Employee
{
	public string FullName {get; set;}
	
	public Employee(string fullName)
	{
		FullName = fullName;
	}
}

Employee emp = new Employee("Aurpan");
emp.FullName = "John"; // emp object is modified here. 
```

Here, ‘**Employee**’ class is mutable, because object of Employee can be modified after creation.

If there are some publicly available methods for setting value to the props, the **Employee** class will still be **Mutable.**

**Immutable:** just the opposite

```csharp
public class Employee
{
	public string FullName {get; }
	
	public Employee(string fullName)
	{
		FullName = fullName;
	}
}

Employee emp = new Employee("Aurpan");
emp.FullName = "John"; // will show error
```

> **strings** are **Immutable,** because every time a new value is assigned to a string variable, it doesn’t remove the previous value. Rather the previous value is stored in and internal array (or memory) and the new value is saved in another index. The string variable just points to the different index (different memory location).
If two string variable has same value, they share the same memory location.

<br><br><br>

# Partial Class

- Allows a class to be split into multiple classes with same name but ‘**partial**’ keyword on it
- All props, methods and constructors in all files will be considered as a single file by the compiler
- No prop, constructor or method can be duplicate

  

```csharp
// Demo.cs
public partial class Demo
{
    public int MyProperty1 { get; set; }

    public void MyMethod1()
    {
        // Method implementation
    }
}

// DemoPartial.cs
public partial class Demo
{
    public int MyProperty2 { get; set; }

    public void MyMethod2()
    {
        // Method implementation
    }
}
```

<br><br><br>

# Attributes - Custom Attributes

- kind of a label that allows us to add extra information or metadata to a class/method/prop which can be used by compiler/runtime/framework
- attribute is simply a **class**
    
    ## Custom Attribute
    
    - a class with **‘Attribute’ suffix**
    - should be derived from **System.Attribute** class or any of its child class
    
    ```csharp
    public class SalaryValidationAttribute : ValidationAttribute // ValidationAttribute is derived from Attribute (System.Attribute)
    {
        public int Min { get; }
        public int Max { get; }
    
        public SalaryValidationAttribute(int min, int max)
        {
            Min = min;
            Max = max;
            ErrorMessage = $"Salary must be between {Min} and {Max}."; // ErrorMessage: public prop from ValidationAttribute class
        }
    
        public override bool IsValid(object? value) // IsValis: public 
        {
            if (value is int salary)
            {
                return salary >= Min && salary <= Max;
            }
            return false;
        }
    }
    
    // Employee.cs
    public class Employee
    {
        public string? FullName { get; set; }
    
        [SalaryValidation(1000, 5000)]
        public int Salary { get; set; }
    }
    
    // Program.cs
    internal class Program
    {
        static void Main(string[] args)
    		{
    		    Employee employee = new Employee { Salary = 8000 };
    		
    		    var context = new ValidationContext(employee);
    		    var results = new List<ValidationResult>();
    		    bool isValid = Validator.TryValidateObject(employee, context, results, true);
    		}
    }
    ```
    
    Here, the output will be false. The ‘**results’** variable will have list of validation error object with only one error and errorMessage.
    
    ```csharp
    [AttributeUsage(AttributeTargets.Class)] // indicates that is Attribute can only applied on Class types
    public class MyCustomClassAttribute : Attribute
    {}
    ```
    Here, AttributeUsage applies some conditions over the Custom Attribute class.

  <br><br><br>

  # Expression

- Abstract representation of an executable code
- it’s a data structure that can contain piece of executable code

```csharp
Expression<Func<int, int>> expr = x => x + 1;
```

‘expr’ can carry the lambda expression

```csharp
public Book GetBookById(Expression<Func<Book, bool>> func)
{
	var book = _context.Books.Where(func); // book is IQuaryable here
	return book.FirstOrDefault();
}
```

## Difference between Expression and Delegate

```csharp
public Book GetBookById(Expression<Func<Book, bool>> func)
{
	var book = _context.Books.Where(func); // book is IQuaryable here
	return book.FirstOrDefault();
}

// VS

public Book GetBookById(Func<Book, bool> func)
{
	var book = _context.Books.Where(func); // book is IEnumerable here
	return book.FirstOrDefault();
}
```

<br><br><br>

# Garbage Collection

- Automatically collects objects with no references and removes them from memory

```csharp
// Book.cs
public class Book
{
	public string Name {get; set; }
	
	~Book() // this is destructor
	{
		// Do something here
	}
}
```

> Destructor is always called just before the disposal of an object by Garbage Collector (GC)
> 

### How it Works

- When any object goes out of scope, that is removed from the stack
- when GC starts collecting the garbage, it checks into **stack** and **marks the references** in the **Heap**. This is called **Marking Process**.
- **Unmarked references** are then removed from **Heap**

### 3 Generational Heap (3G Heap)

- Conceptually, there are **3 heaps in .NET runtime (CLR)**
- While collection garbage, GC transfers the marked ones from **Heap-0 ****to **Heap-1**.
    - **Unmarked ones are not removed** from Heap-0, rather the address pointer is restored to lowest value and by time the **unmarked references are replaced with new references**
    - References are in Heap-1, means they have longer life time
- When Heap-1 is about get full, references with longest life time are moved to Heap-2. This heap is most likely to contain the references with Singleton lifetime.

### Large Object Heap

- Heaps for object with 85Kb
- Works similar to Heap-2, but works independently

### Reference Videos:

- [https://www.youtube.com/watch?v=BeuNvhd1L_g](https://www.youtube.com/watch?v=BeuNvhd1L_g)
