### SOLID Principles

#### S - Single responsibility principles

> A class should only have one reason to change.

Every module or class should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class.

```csharp

Interface IUser {
    bool Login(string userName, string Password);
    bool Register(string userName, string Password);
}

Interface SendEmail {
    bool SuccessEmailSend();
}

Interface Logger {
    void LogInformation();
}

//If I move email and logging methods to IUser interface, it does not make sense. User does not care about sending emails and logic. USER should only have things that refers to the user.
```

#### O - Open/Closed principles (OCP)

> Software entities should be open for extensions, but closed for modifications.

New functionalities should be added with the minimum set of changes, in the existing code.
Existing code should be unchanged.

Implementation:

- The simplest way to apply OCP is to implement new functionality in new derived classes rather than editing the base class.

- Allow client to access original class with a abstract class

Problem?

If the new changes are done in an existing class

- Entire functionality have to be tested. Even the old methods.
- Overhead on QA team
- Maintenance overhead since everything in the same class.
- Breaks the single responsibility principle.

```csharp
public abstract class Employee{
    public abstract void CalculateBonus()'
}

public class PermEmployee : Employee {
    public override void CalculateBonus(){
        //do something here
    }
}

public class ContractEmployee : Employee {
    public override void CalculateBonus(){
        //do something here
    }
}

//if the employee type increases in the company, we dont have to touch the base class.
```

#### L - Liskov substitution principles

> Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.

If a program is using a base class, the reference for the base class should be replaceable for the derived class.

Basically, the derived types must be substitutes for their base type.

#### I - Interface segregation principles

> Many client specific interfaces are better than one general purpose interface.

We should not enforce clients to implement the interfaces that they don't use. Instead of using a big interface, we should break it down to smaller pieces.

```csharp
//Problem
//If a printer that does not have the capability to to Fax and Print duplex and inherit implement this interface, it will end up with methods that it cannot use. "Clients should not be forced to implement methods that they dont use"

interface Print{
    bool PrintContent();
    bool ScanContent();
    bool PhotoContent();
    bool FaxContent();
    bool PrintDuplex();
}


//How it should be
//Printers should only implement classes that it needs.
interface IPrintsScanContent{
    bool PrintContent();
    bool ScanContent();
    bool PhotoContent();
}

interface IFaxContent(){
    bool FaxContent();
}

interface IPrintDuplexContent{}
    bool PrintDuplex();
]


```

#### D - Dependency inversion principles

> One should depend on abstraction instead on concretion

Abstractions should not depend on details, whereas the details should depend on abstractions.
