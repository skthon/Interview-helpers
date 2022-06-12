# SOLID PRINCIPLES
To ensure maintainability, stability, flexibility and readability of code. robert martin aka uncle bob has compiled list of five rules of good design, which are known as SOLID principles. The term SOLID is an abbreviation which in turn consists of abbreviations, each of which hides a whole class of patterns. Below we will look at each of them.


## Single Responsibility principle
A class should have only one responsibility/job i.e there should not be more than one reason to change.

### Example 1:
Let's consider an example of food delivery app.
A Food delivery process consists of several steps like customer information, order information, billing, preparing the order, Delivering the order, Receiving the order.

For each of these step we need create separate classes which will have only one responsibility, if there are further requirements we need to breakdown into further more classes, like billing will have its own complexity for handling the mode of payment.

### Example 2:
Let's consider backend api route for handling user creation.
Here the route should handle three things. First one is user input validation, creating the user, return the response.
Each of these should be handle separately.


## Open Closed Principle
Software entities such as classes, methods, etc should be closed for any modification and open for extension. Basically if we want to add a functionality we need to create a new class and methods instead of changing the existing one.

### Example
We can consider the example of mode of payments. Let's say currently we support two payment methods credit card and debut card. We can create a Payment class and create methods payWithDebit, payWithCredit. In future we want to integrate other mode of payment then in Payment Class we have to create a new method, this will violate the open/closed principle since we are trying to modify the class by adding a new method.
So therefore, what we need to do is create a interface or abstract class containing pay method without implementation and we need to create the payment classes with necessary pay method and its implementation.
```
interface PaymentMethodInterface
{
    public function pay();
}

class Checkout
{
    public function begin(PaymentMethodInterface $payment)
    {
        return $payment->pay();
    }
}

class CashPayment implements PaymentMethodInterface
{
    public function pay()
    {
       return 'Payment method is cache';
    }
}

echo (new Checkout)->begin(new CashPayment());
```

## Liskov Substitution Principle
This means any interface or abstraction should be substitutable anywhere that the abstraction is accepted. When extending the class remember you should be able to pass objects of the subclass in place of the objects  of the parent class without breaking any code. This means that all the abstracts or interface methods should be compatible with behavior of the super class. The extended class should not throw exceptions of the abstract method. 

### Example
Famous example is the real duck and rubber duck. Some of the actions will not be compatible. To follow the LSP you just need to be concerned about is, the return type & exception type of any method of a child class must match with its parent class or the interface that is implemented.


## Interface Segregation Principle
Interface Segregation Principle means A client should not be forced to implement an interface that it doesn’t use. or No client should be forced to depend on methods it doesn’t use. or a client should never depend on anything more than the method it’s calling. We should replace the fat interface with many small, specific interfaces.


### Example
A work place can have different kind of employees. Their responsibilities will differ. Some of their responsibilities will collide and some will not. In this case for their responsibilities to be implemented, we need to break things into multiple interfaces.


## Dependency Inversion Principle
The Dependency Inversion Principle (DIP) states that high level modules should not depend on low level modules; both should depend on abstractions. Abstractions should not depend on details.  Details should depend upon abstractions.
