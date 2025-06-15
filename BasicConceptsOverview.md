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
    
    ### Abstract Modifier
    
    - can be used with Methods or Classes
    - an Abstract Method doesn’t have an implementation (no body), only declaration
    - if even a single class is Abstract, the whole class needs to be Abstract
    - child classes are forced to implement that method
    - no instance can be created for Abstract class
    
    ### Sealed Modifier
    
    - can be used with Methods or Classes
    - it prevents classes from being inherited and methods from being overridden
    - if applied to a method, the whole class can be inherited, just the method can’t be overridden
