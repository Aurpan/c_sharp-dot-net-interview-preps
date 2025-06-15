# Initial Screening @Cefalo

This is what I can remember from the Initial screening test I attended on June 14, 2025 (9:30 am - 11:50 am)

### **Job Description**

- **Experience:** 3 to 12 years
- **Tech Stack:** .NET Core, Web API, REST, EF, JS, SQL Server

### **Topics for the Test:**

- C#, .NET Core
- RESTful API, Web API
- Async Programming
- Dependency Injection
- Entity Framework, SQL
- Algorithm & Data Structure
- Design Patterns

These topics were clearly mentioned in the invitation email

### **Some instructions regarding the test:**

- You’ll have to attend the test physically in Cefalo office
- You need to carry your own laptop or inform them to arrange when you get the invitation email
- Duration of the test was 140 mins (2 hours 20 mins)
- The test is done in HackerRank platform
- You’ll have to join a cefalo-guest wi-fi, not allowed to use mobile data.
- All sites except HackerRank will be blocked
- There were 23 questions, 20 mcq and 3 coding problems

# Questions (as far as I can remember)

### MCQ Part

---

What is the output the following code?

```csharp
int x = 5;
int y = 2;
double result = x / y;
Console.WriteLine(result);
```

**Options:** (pick only one)

- 2
- 2.5
- 3
- 2.50

---

Why would you choose ‘StringBuilder’ over ‘string’?

**Options:** (pick many)

- Immutable
- Mutable
- Every when modified it doesn’t preserve the previous string, hence takes less memory
- *can’t remember*

  

---

You have an app that sends 4 digit OTP. Now business requirement changed and need to send 6 digit OTP. But the old app is so closely coupled with 4 digit OTP that they need to remain same. How would you make the change in new app using SOLID, Clean Code and proper design patterns?

**Options:** (pick only one)

- Leave the existing endpoint and make a new one and send the 6 digit OTP through it
- Modify the existing endpoint and add a query string. The logic will be handled in the service layer.
- Make new version of the api and create a new endpoint there.

---

Two database tables given with some data - **Product** and **Order.** 

The application needs the list of all products with their total sales. The product with no orders should have ‘0’ shown in the list. What is the correct query?

---

Which of the following option relates the most with “TestFixture”?

**Options:** (pick only one)

- Mocking of a service
- Necessary environment for test
- Collection of all similar test classes
- *can’t remember*

---

You need to test a mail sending service that uses an external SMTP service. How would you test that?

**Options:** (pick only one)

- Mocking the external service
- Actually calling the service
- *can’t remember*
- *can’t remember*

---

You are working on networking application where huge number of packets needs to received and stored in a specified order. Which data structure will you use?

**Options:** (pick only one)

- Stack
- Linked List
- Queue
- Array

---

Look at the following code, where a Scoped service is injected inside Singleton service in a .NET Core Web API application. 

```csharp
public class ScopedService : IScopedService
{}

public class SingletonService : ISingletonService
{
	private readonly IScopedService _scopedService;
	
	public SingletonService (IScopedService scopedService)
	{
		_scopedService = scopedService;
	}
	
	_scopedService.SomeMethodCall();
}
```

 

```csharp
// DI
builder.Services.AddSingleton<ISingletonService, SingletonService>();
builder.Services.AddScoped<IScopedService, ScopedService>();
```

Which of the following option is true?

**Options:** (pick only one)

- When SingletonService is used, the lifetime will Singleton
- When SingletonService is used, the lifetime will Scoped
- When ScopedServiceis used, the lifetime will Singleton
- When ScopedServiceis used, the lifetime will Scoped

---

Rest of the questions had a big code snippet and output or output sequence was asked.

<br>

### Coding Part

---

There is a RealEstate application where users can list their real-estates assets. They can show, delete, update and add assets.

There is a class named ‘**RealEstateListings**’ which inherits ‘**IRealEstateListings**’ interface. This class represents a real-estate. You’ll have to create a class called ‘**AppRealEstate**’. Inherit the class ‘**IAppRealEstate**’ and implement the methods. You’ll create a private field of **List<IRealEstateListings>** type named ‘**listings**’ in the ‘**AppRealEstate**’ class.

Here are the methods and what they do:

- **GetAllListings:** Returns **List<RealEstateListings>** containing all the data inside **listings**
- **GetListingByID:** Returns a single **IRealEstateListings** object that matches with the ID (if exists)
- **AddListing:** Adds the provided **RealEstateListings** object to the **listings**
- **RemoveListing:** Removes the **RealEstateListings** object from **listings** which matched the **RealEstateListings** object provided
- **GetListingsByLocation:** Returns **List<RealEstateListings>** which matches the provided location string
- **GetListingsByPriceRange:** Returns **List<RealEstateListings>** where the price falls between the minPrice and maxPrice

```csharp
public interface IRealEstateListing
{
	public Guid Id;
	public string Title;
	public string Description;
	public string Location;
	public decimal Price;
}

public class RealEstateListing : IRealEstateListing
{
	public Guid Id {get; set;};
	public string Title {get; set;};
	public string Description {get; set;};
	public string Location {get; set;};
	public decimal Price {get; set;};
}

public interface IAppRealEstate
{
	List<RealEstateListings> GetAllListings();
	RealEstateListings GetListingByID(Guid ID);
	void AddListing();
	void RemoveListing(RealEstateListings listing);
	List<RealEstateListings> GetListingsByLocation(string location);
	List<RealEstateListings> GetListingsByPriceRange(decimal minPrice, decimal maxPrice);
}

public class AppRealEstate : IAppRealEstate
{
	// start your code here
}
```

---

You’ll have to create **PasswordSanitizer** class which has a **Filtered** method which takes some passwords, basically **List<string>**. Remove all the passwords that meets the following conditions:

- password has length less than 5
- password only has digits (i.e 6411649731)
- password only has english letters (i.e passNewpass)

The method should return the eligible password as space separated string.

**Sample Inputs:**

[”WordPress”,  “123321”, “pass@123, p12@”, “admin@5764”]

**Sample Output:**

pass@123 admin@5764

```csharp
public class PasswordSanitizer
{
	public string Filtered(List<string> passwords)
	{
		// start your code here
	}
}
```

---

Your method will take a list of integer which represents the market-price of a stock in each days. If the price goes higher in any consecutive days, it is considered **UpTrend** and **DownTrend** otherwise. In any set of price given, if the **UpTrend** dominates then the user should be told to ‘**BUY**’, else ‘**WAIT**’.

**Sample - 1:**

**Input:** [102, 103, 106, 115, 105, 102, 106, 108]

**Output:** “BUY”

**Sample - 2:**

**Input:** [102, 103, 102, 104, 105, 102, 100, 98]

**Output:** “WAIT”

```csharp
public class TrendPredictor
{
	public string Predict(List<int> prices)
	{
		// start your code here
	}
}
```
