
* [successivetech](https://medium.com/successivetech/s-o-l-i-d-the-first-5-principles-of-object-oriented-design-with-php-b6d2742c90d7)
* [SOLID_cheatsheet](https://www.monterail.com/hubfs/PDF%20content/SOLID_cheatsheet.pdf)
* [thinktocode](https://www.thinktocode.com/2017/10/10/solid-principles-in-php/)
* [laracasts](https://laracasts.com/series/solid-principles-in-php)
* [evrtrabajo](https://dev.to/evrtrabajo/solid-in-php-d8e)
* [youtube](https://www.youtube.com/watch?v=rtmFCcjEgEw)
* [youtube laracon](https://www.youtube.com/watch?v=NeXQEJNWO5w)
* [katerina's slide](https://www.slideshare.net/KaterinaTrajchevska/from-good-to-solid-how-to-become-a-better-developer)

# Open/Closed principle

the Open/Closed Principle (OCP) is a design principle in object-oriented programming that states that a class or module should be open for extension but closed for modification. In other words, you should be able to extend the behavior of a class without modifying its source code.

Here is a PHP example of a class that violates the Open/Closed Principle:

```php
class PaymentProcessor {
  public function pay($amount, $paymentMethod) {
    if ($paymentMethod == 'credit_card') {
      // Process credit card payment
    } else if ($paymentMethod == 'paypal') {
      // Process PayPal payment
    } else if ($paymentMethod == 'bitcoin') {
      // Process Bitcoin payment
    } else {
      throw new Exception('Invalid payment method');
    }
  }
}
```

In this example, the PaymentProcessor class has a pay method that accepts an amount and a payment method as parameters. The method then checks the payment method and processes the payment accordingly. However, if a new payment method is added, the class would need to be modified to handle it, which violates the OCP.

A better approach would be to create a separate class for each payment method, and to make them implement a common interface, like this:

```php
interface PaymentMethod {
  public function processPayment($amount);
}

class CreditCardPayment implements PaymentMethod {
  public function processPayment($amount) {
    // Process credit card payment
  }
}

class PayPalPayment implements PaymentMethod {
  public function processPayment($amount) {
    // Process PayPal payment
  }
}

class BitcoinPayment implements PaymentMethod {
  public function processPayment($amount) {
    // Process Bitcoin payment
  }
}

class PaymentProcessor {
  public function pay($amount, PaymentMethod $paymentMethod) {
    $paymentMethod->processPayment($amount);
  }
}
```

This way, the `PaymentProcessor` class is open for extension, as new payment methods can be added by creating new classes that implement the `PaymentMethod` interface, without modifying the `PaymentProcessor` class. This promotes better code organization, reduces coupling, and makes the code more flexible and maintainable.

# Dependency Inversion

* [digitalocean](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#dependency-inversion-principle)
* [stackify](https://stackify.com/dependency-inversion-principle/#:~:text=Definition%20of%20the%20Dependency%20Inversion%20Principle&text=To%20achieve%20that%2C%20you%20need,level%20modules%20from%20each%20other.&text=Both%20should%20depend%20on%20abstractions,Details%20should%20depend%20on%20abstractions.)


# Single resposilibity

Single Responsibility Principle (SRP) is a design principle in object-oriented programming that states that a class should have only one reason to change, i.e., it should have only one responsibility or job.

In practical terms, this means that a class should be responsible for one thing and one thing only, and that it should not have multiple responsibilities or concerns. This helps to keep classes focused, maintainable, and flexible, and to avoid complex dependencies and coupling between different parts of the code.

Here is a PHP example of a class that violates the Single Responsibility Principle:

```php
class User {
  public function register() {
    // Register the user
  }

  public function login() {
    // Log in the user
  }

  public function sendEmail() {
    // Send an email to the user
  }

  public function getProfile() {
    // Get the user's profile
  }
}
```

In this example, the User class has multiple responsibilities: registering users, logging them in, sending them emails, and retrieving their profiles. This violates the SRP, as each of these responsibilities should be handled by a separate class.

A better approach would be to split the responsibilities into separate classes, like this:

```php
class UserRegistration {
  public function register() {
    // Register the user
  }
}

class UserLogin {
  public function login() {
    // Log in the user
  }
}

class UserEmail {
  public function sendEmail() {
    // Send an email to the user
  }
}

class UserProfile {
  public function getProfile() {
    // Get the user's profile
  }
}
```

# Liskov substitution

The Liskov Substitution Principle (LSP) is one of the SOLID principles that states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, a subclass should be able to be used in place of its parent class without any unexpected behavior.

example: php

```php
<?php

interface Shape {
  public function area();
}

class Rectangle implements Shape {
  protected $width;
  protected $height;
  
  public function setWidth($width) {
    $this->width = $width;
  }
  
  public function setHeight($height) {
    $this->height = $height;
  }
  
  public function area() {
    return $this->width * $this->height;
  }
}

class Square implements Shape {
  protected $side;
  
  public function setSide($side) {
    $this->side = $side;
  }
  
  public function area() {
    return $this->side * $this->side;
  }
}

function printArea(Shape $shape) {
  echo "The area is: " . $shape->area() . "\n";
}

$rectangle = new Rectangle();
$rectangle->setWidth(5);
$rectangle->setHeight(10);
printArea($rectangle); // Output: The area is: 50

$square = new Square();
$square->setSide(5);
printArea($square); // Output: The area is: 25

```

In this example, the `Rectangle` and `Square` classes implement the Shape interface, which has a `area()` method. The `printArea()` function takes a Shape object as a parameter and calls its `area()` method to calculate and print the area. Both `Rectangle` and `Square` classes can be used interchangeably with the `Shape` interface, demonstrating the Liskov Substitution Principle.

# Interface Segragation

Interface Segregation Principle (ISP) is a design principle in object-oriented programming that states that a class should not be forced to implement interfaces it does not use. In other words, it is better to have several small and focused interfaces rather than a single large and generic interface.

```php
interface Machine {
  public function print();
  public function scan();
  public function fax();
}

class AllInOnePrinter implements Machine {
  public function print() {
    // Print the document
  }

  public function scan() {
    // Scan the document
  }

  public function fax() {
    // Fax the document
  }
}
```

split the interface 

```php
interface Printer {
  public function print();
}

interface Scanner {
  public function scan();
}

interface Fax {
  public function fax();
}

class AllInOnePrinter implements Printer, Scanner {
  public function print() {
    // Print the document
  }

  public function scan() {
    // Scan the document
  }
}

```
# code smell //

~ bad smell / bad practise

* https://hackernoon.com/5-easy-wins-to-refactor-even-the-worst-legacy-code-7vuc3069
