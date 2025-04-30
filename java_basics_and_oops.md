# Java Fundamentals and Object Oriented Programming

Object-Oriented Programming is a methodology or paradigm to design a program using classes and objects. It simplifies the software development and maintenance. Main Concepts - Inheritance, Polymorphism, Abstraction, Encapsulation.

## Data Types in Java

<table class="alt">
<tbody><tr>
  <th id="table_dvpt_datatype"><strong>Data Type</strong></th>
  <th id="table_dvpt_defaultvalue"><strong>Default Value</strong></th>
  <th id="table_dvpt_defaultsize"><strong>Default size</strong></th>
</tr>
<tr>
<td headers="table_dvpt_datatype">boolean</td>
<td headers="table_dvpt_defaultvalue">false</td>
<td headers="table_dvpt_defaultsize">1 bit</td>
</tr>
<tr>
<td headers="table_dvpt_datatype">char</td>
<td headers="table_dvpt_defaultvalue">'\u0000'</td>
<td headers="table_dvpt_defaultsize">2 byte</td>
</tr>
<tr>
<td headers="table_dvpt_datatype">byte</td>
<td headers="table_dvpt_defaultvalue">0</td>
<td headers="table_dvpt_defaultsize">1 byte</td>
</tr>
<tr>
<td headers="table_dvpt_datatype">short</td>
<td headers="table_dvpt_defaultvalue">0</td>
<td headers="table_dvpt_defaultsize">2 byte</td>
</tr>
<tr>
<td headers="table_dvpt_datatype">int</td>
<td headers="table_dvpt_defaultvalue">0</td>
<td headers="table_dvpt_defaultsize">4 byte</td>
</tr>
<tr>
<td headers="table_dvpt_datatype">long</td>
<td headers="table_dvpt_defaultvalue">0L</td>
<td headers="table_dvpt_defaultsize">8 byte</td>
</tr>
<tr>
<td headers="table_dvpt_datatype">float</td>
<td headers="table_dvpt_defaultvalue">0.0f</td>
<td headers="table_dvpt_defaultsize">4 byte</td>
</tr>
<tr>
<td headers="table_dvpt_datatype">double</td>
<td headers="table_dvpt_defaultvalue">0.0d</td>
<td headers="table_dvpt_defaultsize">8 byte</td>
</tr>
</tbody></table>

NOTE : UTF-8 is the most popular unicode character encoding with 90% websites using it.

### Example: Data Types
```java
public class DataTypesExample {
    public static void main(String[] args) {
        // Primitive data types
        boolean isJavaFun = true;
        char grade = 'A';
        byte age = 25;
        short salary = 30000;
        int population = 1000000;
        long worldPopulation = 8000000000L;
        float pi = 3.14f;
        double gravity = 9.81;

        // Wrapper classes
        Boolean isActive = true;
        Character firstLetter = 'J';
        Integer count = 100;
        Double price = 99.99;

        System.out.println("Is Java fun? " + isJavaFun);
        System.out.println("Grade: " + grade);
        System.out.println("Age: " + age);
        System.out.println("Salary: " + salary);
        System.out.println("Population: " + population);
        System.out.println("World Population: " + worldPopulation);
        System.out.println("Pi: " + pi);
        System.out.println("Gravity: " + gravity);
    }
}
```

## Data Type Promotion in Java :

![data type promotion small](https://user-images.githubusercontent.com/2780145/34364362-403e9db4-eaab-11e7-914b-7acc9007cf41.png)

### Example: Data Type Promotion
```java
public class TypePromotionExample {
    public static void main(String[] args) {
        byte b = 42;
        char c = 'a';
        short s = 1024;
        int i = 50000;
        float f = 5.67f;
        double d = .1234;

        // The expression is automatically promoted to double
        double result = (f * b) + (i / c) - (d * s);
        System.out.println("Result = " + result);
    }
}
```

## Wrapper Classes in Java

<table class="alt">
<tbody><tr><th>Primitive Type</th><th>Wrapper class</th></tr>
<tr><td>boolean</td><td>Boolean</td></tr>
<tr><td>char</td><td>Character</td></tr>
<tr><td>byte</td><td>Byte</td></tr>
<tr><td>short</td><td>Short</td></tr>
<tr><td>int</td><td>Integer</td></tr>
<tr><td>long</td><td>Long</td></tr>
<tr><td>float</td><td>Float</td></tr>
<tr><td>double</td><td>Double</td></tr>
</tbody></table>

### Example: Wrapper Classes
```java
public class WrapperExample {
    public static void main(String[] args) {
        // Autoboxing: primitive to wrapper
        Integer intObj = 10;
        Double doubleObj = 10.5;
        Boolean boolObj = true;

        // Unboxing: wrapper to primitive
        int intValue = intObj;
        double doubleValue = doubleObj;
        boolean boolValue = boolObj;

        // Using wrapper class methods
        System.out.println("Integer value: " + intObj.intValue());
        System.out.println("Double value: " + doubleObj.doubleValue());
        System.out.println("Boolean value: " + boolObj.booleanValue());

        // Parsing strings to numbers
        String number = "123";
        int parsedInt = Integer.parseInt(number);
        System.out.println("Parsed integer: " + parsedInt);
    }
}
```

## Operators in Java

<table class="alt">
<tbody><tr><th>Operator Type</th><th>Category</th><th>Precedence</th></tr>
<tr>
<td rowspan="2">Unary</td><td>postfix</td><td><code><em>expr</em>++ <em>expr</em>--</code></td>
</tr>
<tr>
<td>prefix</td><td headers="precedence"><code>++<em>expr</em> --<em>expr</em> +<em>expr</em> -<em>expr</em> ~ !</code></td>
</tr>
<tr>
<td rowspan="2">Arithmetic</td><td>multiplicative</td><td headers="precedence"><code>* / %</code></td>
</tr>
<tr>
<td>additive</td><td headers="precedence"><code>+ -</code></td>
</tr>
<tr>
<td>Shift</td><td>shift</td><td headers="precedence"><code>&lt;&lt; &gt;&gt; &gt;&gt;&gt;</code></td>
</tr>
<tr>
<td rowspan="2">Relational</td><td>comparison</td><td headers="precedence"><code>&lt; &gt; &lt;= &gt;= instanceof</code></td>
</tr>
<tr>
<td>equality</td><td headers="precedence"><code>== !=</code></td>
</tr>
<tr>
<td rowspan="3">Bitwise</td><td>bitwise AND</td><td headers="precedence"><code>&amp;</code></td>
</tr>
<tr>
<td>bitwise exclusive OR</td><td headers="precedence"><code>^</code></td>
</tr>
<tr>
<td>bitwise inclusive OR</td><td headers="precedence"><code>|</code></td>
</tr>
<tr>
<td rowspan="2">Logical</td><td>logical AND</td><td headers="precedence"><code>&amp;&amp;</code></td>
</tr>
<tr>
<td>logical OR</td><td headers="precedence"><code>||</code></td>
</tr>
<tr>
<td>Ternary</td><td>ternary</td><td headers="precedence"><code>? :</code></td>
</tr>
<tr>
<td>Assignment</td><td>assignment</td><td headers="precedence"><code>= += -= *= /= %= &amp;= ^= |= &lt;&lt;= &gt;&gt;= &gt;&gt;&gt;=</code></td>
</tr>
</tbody></table>

### Example: Operators
```java
public class OperatorsExample {
    public static void main(String[] args) {
        // Arithmetic operators
        int a = 10, b = 5;
        System.out.println("Addition: " + (a + b));
        System.out.println("Subtraction: " + (a - b));
        System.out.println("Multiplication: " + (a * b));
        System.out.println("Division: " + (a / b));
        System.out.println("Modulus: " + (a % b));

        // Relational operators
        System.out.println("a > b: " + (a > b));
        System.out.println("a < b: " + (a < b));
        System.out.println("a == b: " + (a == b));

        // Logical operators
        boolean x = true, y = false;
        System.out.println("x && y: " + (x && y));
        System.out.println("x || y: " + (x || y));
        System.out.println("!x: " + (!x));

        // Bitwise operators
        int num1 = 5; // 0101
        int num2 = 7; // 0111
        System.out.println("Bitwise AND: " + (num1 & num2)); // 0101 = 5
        System.out.println("Bitwise OR: " + (num1 | num2));  // 0111 = 7
        System.out.println("Bitwise XOR: " + (num1 ^ num2)); // 0010 = 2
    }
}
```

## Java Naming Conventions :

<table class="alt">
<tbody><tr><th>Name</th><th>Convention</th></tr>
<tr><td>class name</td><td> should start with uppercase letter and be a noun
<br>e.g. String, Color, Button, System, Thread etc.</td></tr>
<tr><td>interface name</td><td>should start with uppercase letter and be an adjective
<br>e.g. Runnable, Remote, ActionListener etc.</td></tr>
<tr><td>method name</td><td>should start with lowercase letter and be a verb
<br>e.g. actionPerformed(), main(), print(), println() etc.
</td></tr>
<tr><td>variable name</td><td>should start with lowercase letter
<br>e.g. firstName, orderNumber etc.</td></tr>
<tr><td>package name</td><td>should be in lowercase letter
<br>e.g. java, lang, sql, util etc.
</td></tr>
<tr><td>constants name</td><td>should be in uppercase letter.
<br>e.g. RED, YELLOW, MAX_PRIORITY etc.</td></tr>
</tbody></table>

## Object vs Class

<table class="alt">
<tbody><tr><th>Object</th><th>Class</th></tr>
<tr><td>Object is an <strong>instance</strong> of a class.</td><td>Class is a <strong>blueprint or template</strong> from which objects are created.</td></tr>
<tr><td>Object is a <strong>real world entity</strong> such as pen, laptop, mobile, bed, keyboard, mouse, chair etc.</td><td>Class is a <strong>group of similar objects</strong>.</td></tr>
<tr><td>Object is a <strong>physical</strong> entity.</td><td>Class is a <strong>logical</strong> entity.</td></tr>
<tr><td>Object is created through <strong>new keyword</strong> mainly e.g. Student s1=new Student();</td><td>Class is declared using <strong>class keyword</strong> e.g. class Student{}</td></tr>
<tr><td>Object is created <strong>many times</strong> as per requirement.</td><td>Class is declared <strong>once</strong>.</td></tr>
<tr><td>Object <strong>allocates memory when it is created</strong>.</td><td>Class <strong>doesn't allocated memory when it is created</strong>.</td></tr>
<tr><td>There are <strong>many ways to create object</strong> like new keyword, newInstance() method, clone() method, factory method & deserialization.</td><td>There is only <strong>one way to define class</strong> in java using class keyword.</td></tr>
</tbody></table>

### Example: Class and Object
```java
// Class definition
class Car {
    // Fields (properties)
    private String brand;
    private String model;
    private int year;

    // Constructor
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
    }

    // Methods (behaviors)
    public void start() {
        System.out.println("Starting the " + brand + " " + model);
    }

    public void displayInfo() {
        System.out.println("Brand: " + brand);
        System.out.println("Model: " + model);
        System.out.println("Year: " + year);
    }
}

public class ClassObjectExample {
    public static void main(String[] args) {
        // Creating objects of Car class
        Car car1 = new Car("Toyota", "Camry", 2020);
        Car car2 = new Car("Honda", "Civic", 2021);

        // Using object methods
        car1.displayInfo();
        car1.start();

        car2.displayInfo();
        car2.start();
    }
}
```

## Constructors vs Methods

<table class="alt">
<tbody><tr><th>Java Constructor</th><th>Java Method</th></tr>
<tr><td>Constructor is used to initialize the state of an object.</td><td>Method is used to expose behaviour of an object.</td></tr>
<tr><td>Constructor must not have return type.</td><td>Method must have return type.</td></tr>
<tr><td>Constructor is invoked implicitly.</td><td>Method is invoked explicitly.</td></tr>
<tr><td>Compiler provides a default constructor if you don't have any constructor.</td><td>Method is not provided by compiler in any case.</td></tr>
<tr><td>Constructor name must be same as the class name.</td><td> Method name may or may not be same as class name.</td></tr>
</tbody></table>

### Example: Constructors and Methods
```java
class Student {
    private String name;
    private int age;

    // Default constructor
    public Student() {
        this.name = "Unknown";
        this.age = 0;
    }

    // Parameterized constructor
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Method
    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }

    // Method with return type
    public String getName() {
        return name;
    }
}

public class ConstructorMethodExample {
    public static void main(String[] args) {
        // Using default constructor
        Student student1 = new Student();
        student1.displayInfo();

        // Using parameterized constructor
        Student student2 = new Student("John", 20);
        student2.displayInfo();

        // Using method with return type
        String name = student2.getName();
        System.out.println("Student name: " + name);
    }
}
```

## Types of Inheritance (Supported through Class)

![single inheritance](https://user-images.githubusercontent.com/2780145/34364364-40b6b646-eaab-11e7-8c92-2c4cd9d0b2ca.png)

## Types of Inheritance (Supported through Interface only)

![multiple inheritance](https://user-images.githubusercontent.com/2780145/34364363-407486b8-eaab-11e7-94e2-5c1876f414d3.png)

### Example: Inheritance
```java
// Single Inheritance
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}

// Multilevel Inheritance
class BabyDog extends Dog {
    void weep() {
        System.out.println("Baby dog is weeping");
    }
}

// Hierarchical Inheritance
class Cat extends Animal {
    void meow() {
        System.out.println("Cat is meowing");
    }
}

public class InheritanceExample {
    public static void main(String[] args) {
        // Single Inheritance
        Dog dog = new Dog();
        dog.eat();
        dog.bark();

        // Multilevel Inheritance
        BabyDog babyDog = new BabyDog();
        babyDog.eat();
        babyDog.bark();
        babyDog.weep();

        // Hierarchical Inheritance
        Cat cat = new Cat();
        cat.eat();
        cat.meow();
    }
}
```

### Example: Multiple Inheritance and Hybrid Inheritance using Interfaces
```java
// Multiple Inheritance using Interfaces
interface Flyable {
    void fly();
    default void takeOff() {
        System.out.println("Taking off...");
    }
}

interface Swimmable {
    void swim();
    default void dive() {
        System.out.println("Diving into water...");
    }
}

// Class implementing multiple interfaces
class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck is flying");
    }

    @Override
    public void swim() {
        System.out.println("Duck is swimming");
    }
}

// Hybrid Inheritance Example
interface Animal {
    void eat();
    default void sleep() {
        System.out.println("Animal is sleeping");
    }
}

interface Mammal extends Animal {
    void giveBirth();
}

interface Bird extends Animal {
    void layEggs();
}

// Class implementing multiple interfaces with inheritance
class Bat implements Mammal, Bird {
    @Override
    public void eat() {
        System.out.println("Bat is eating insects");
    }

    @Override
    public void giveBirth() {
        System.out.println("Bat is giving birth to live young");
    }

    @**Override**
    public void layEggs() {
        System.out.println("Bat does not lay eggs");
    }
}

public class MultipleInheritanceExample {
    public static void main(String[] args) {
        // Multiple Inheritance Example
        Duck duck = new Duck();
        duck.takeOff();
        duck.fly();
        duck.dive();
        duck.swim();

        // Hybrid Inheritance Example
        Bat bat = new Bat();
        bat.eat();
        bat.sleep();
        bat.giveBirth();
        bat.layEggs();
    }
}
```

## Association vs Aggregation vs Composition

![association-aggregation-composition](https://user-images.githubusercontent.com/2780145/34364371-5db00694-eaab-11e7-8ef2-bf56d3394f15.png)

### Example: Association, Aggregation, and Composition
```java
// Association Example
class Driver {
    private String name;

    public Driver(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

class Car {
    private String model;
    private Driver driver; // Association

    public Car(String model) {
        this.model = model;
    }

    public void setDriver(Driver driver) {
        this.driver = driver;
    }

    public void displayInfo() {
        System.out.println("Car Model: " + model);
        if (driver != null) {
            System.out.println("Driver: " + driver.getName());
        }
    }
}

// Aggregation Example
class Department {
    private String name;
    private List<Employee> employees; // Aggregation

    public Department(String name) {
        this.name = name;
        this.employees = new ArrayList<>();
    }

    public void addEmployee(Employee employee) {
        employees.add(employee);
    }
}

class Employee {
    private String name;

    public Employee(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

// Composition Example
class House {
    private final Room room; // Composition

    public House() {
        this.room = new Room(); // Room cannot exist without House
    }
}

class Room {
    private String type;

    public Room() {
        this.type = "Living Room";
    }
}

public class RelationshipExample {
    public static void main(String[] args) {
        // Association
        Car car = new Car("Toyota");
        Driver driver = new Driver("John");
        car.setDriver(driver);
        car.displayInfo();

        // Aggregation
        Department department = new Department("IT");
        Employee emp1 = new Employee("Alice");
        Employee emp2 = new Employee("Bob");
        department.addEmployee(emp1);
        department.addEmployee(emp2);

        // Composition
        House house = new House();
        // Room is created automatically with House
    }
}
```

## Aggregation vs Composition

<table class="alt">
<tbody><tr><th>Aggregation</th><th>Composition</th></tr>
<tr><td>Aggregation is a weak Association.</td><td>Composition is a strong Association.</td></tr>
<tr><td>Class can exist independently without owner.</td><td>Class can not meaningfully exist without owner.</td></tr>
<tr><td>Have their own Life Time.</td><td>Life Time depends on the Owner.</td></tr>
<tr><td>A uses B.</td><td>A owns B.</td></tr>
<tr><td>Child is not owned by 1 owner.</td><td>Child can have only 1 owner.</td></tr>
<tr><td>Has-A relationship. A has B.</td><td>Part-Of relationship. B is part of A.</td></tr>
<tr><td>Denoted by a empty diamond in UML.</td><td>Denoted by a filled diamond in UML.</td></tr>
<tr><td>We do not use "final" keyword for Aggregation.</td><td>"final" keyword is used to represent Composition.</td></tr>
<tr><td>Examples:<br>- Car has a Driver.<br>- A Human uses Clothes.<br>- A Company is an aggregation of People.<br>- A Text Editor uses a File.<br>- Mobile has a SIM Card.</td><td>Examples:<br>- Engine is a part of Car.<br>- A Human owns the Heart.<br>- A Company is a composition of Accounts.<br>- A Text Editor owns a Buffer.<br>- IMEI Number is a part of a Mobile.</td></tr>
</tbody></table>

NOTE : "final" keyword is used in Composition to make sure child variable is initialized.

## Polymorphism - Method Overloading vs Method Overriding

<table class="alt">
<tbody><tr><th>Method Overloading </th><th>Method Overriding</th></tr>
<tr><td>Method overloading is used <em>to increase the readability</em> of the program.</td><td>Method overriding is used <em>to provide the specific implementation</em> of the method that is already provided by its super class.</td></tr>
<tr><td>Method overloading is performed <em>within class</em>.</td><td>Method overriding occurs <em>in two classes</em> that have IS-A (inheritance) relationship.</td></tr>
<tr><td>In case of method overloading, <em>parameter must be different</em>.</td><td>In case of method overriding, <em>parameter must be same</em>.</td></tr>
<tr><td>Method overloading is the example of <em>compile time polymorphism</em>.</td><td>Method overriding is the example of <em>run time polymorphism</em>.</td></tr>
<tr><td>In java, method overloading can't be done by changing only the return type of method. <em>Return type can be same/different</em> in overloading, but you must change the parameter.</td><td><em>Return type must be same or covariant (changing return type to subclass type)</em> in method overriding.</td></tr>
</tbody></table>

### Example: Method Overloading and Overriding
```java
class Calculator {
    // Method Overloading
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }
}

class AdvancedCalculator extends Calculator {
    // Method Overriding
    @Override
    public int add(int a, int b) {
        System.out.println("Using advanced addition");
        return a + b;
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        Calculator calc = new Calculator();

        // Method Overloading
        System.out.println("Adding integers: " + calc.add(5, 3));
        System.out.println("Adding doubles: " + calc.add(5.5, 3.3));
        System.out.println("Adding three numbers: " + calc.add(5, 3, 2));

        // Method Overriding
        AdvancedCalculator advCalc = new AdvancedCalculator();
        System.out.println("Advanced addition: " + advCalc.add(5, 3));
    }
}
```

## Abstract Class vs Interface

<table class="alt">
<tbody><tr><th>Abstract class</th><th>Interface</th></tr>
<tr><td>Abstract class can <strong>have abstract and non-abstract</strong> methods.</td><td>Interface can have <strong>only abstract</strong> methods. Since Java8, it can have <strong>default & static methods</strong> also.</td></tr>
<tr><td>Abstract class <strong>doesn't support multiple inheritance</strong>.</td><td>Interface <strong>supports multiple inheritance</strong>.</td></tr>
<tr><td>Abstract class <strong>can have final, non-final, static and non-static variables</strong>.</td><td>Interface has <strong>only static and final variables</strong>.</td></tr>
<tr><td>Abstract class <strong>can provide the implementation of interface</strong>.</td><td>Interface <strong>can't provide the implementation of abstract class</strong>.</td></tr>
<tr><td>The <strong>abstract keyword</strong> is used to declare abstract class.</td><td>The <strong>interface keyword</strong> is used to declare interface.</td></tr>
<tr><td><strong>Example:</strong><br> public abstract class Shape{<br>public abstract void draw();}</td><td><strong>Example:</strong><br> public interface Drawable{<br>void draw();}</td></tr>
</tbody></table>

### Example: Abstract Class and Interface
```java
// Abstract Class
abstract class Shape {
    protected String color;

    public Shape(String color) {
        this.color = color;
    }

    // Abstract method
    abstract double calculateArea();

    // Concrete method
    public String getColor() {
        return color;
    }
}

// Interface
interface Drawable {
    void draw();
    default void print() {
        System.out.println("Printing shape");
    }
}

class Circle extends Shape implements Drawable {
    private double radius;

    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }

    @Override
    double calculateArea() {
        return Math.PI * radius * radius;
    }

    @Override
    public void draw() {
        System.out.println("Drawing a " + color + " circle");
    }
}

public class AbstractInterfaceExample {
    public static void main(String[] args) {
        Circle circle = new Circle("Red", 5.0);
        System.out.println("Area: " + circle.calculateArea());
        circle.draw();
        circle.print();
    }
}
```

## Java Access Modifiers

<table class="alt">
<tbody><tr><th>Access Modifier</th><th>within class</th><th>within package</th><th>outside package by subclass only</th><th>outside package</th></tr>
<tr><td><b>Private</b></td><td>Y</td><td>N</td><td>N</td><td>N</td></tr>
<tr><td><b>Default</b></td><td>Y</td><td>Y</td><td>N</td><td>N</td></tr>
<tr><td><b>Protected</b></td><td>Y</td><td>Y</td><td>Y</td><td>N</td></tr>
<tr><td><b>Public</b></td><td>Y</td><td>Y</td><td>Y</td><td>Y</td></tr>
</tbody></table>

### Example: Access Modifiers
```java
class AccessExample {
    private int privateVar = 1;
    int defaultVar = 2;
    protected int protectedVar = 3;
    public int publicVar = 4;

    private void privateMethod() {
        System.out.println("Private method");
    }

    void defaultMethod() {
        System.out.println("Default method");
    }

    protected void protectedMethod() {
        System.out.println("Protected method");
    }

    public void publicMethod() {
        System.out.println("Public method");
    }
}

class SubClass extends AccessExample {
    void testAccess() {
        // Can access protected and public members
        System.out.println(protectedVar);
        System.out.println(publicVar);
        protectedMethod();
        publicMethod();

        // Cannot access private and default members
        // System.out.println(privateVar); // Error
        // System.out.println(defaultVar); // Error
        // privateMethod(); // Error
        // defaultMethod(); // Error
    }
}

public class AccessModifierExample {
    public static void main(String[] args) {
        AccessExample obj = new AccessExample();

        // Can only access public members from outside
        System.out.println(obj.publicVar);
        obj.publicMethod();

        // Cannot access other members
        // System.out.println(obj.privateVar); // Error
        // System.out.println(obj.defaultVar); // Error
        // System.out.println(obj.protectedVar); // Error
        // obj.privateMethod(); // Error
        // obj.defaultMethod(); // Error
        // obj.protectedMethod(); // Error
    }
}
```

## Methods of Object Class

The Object class is the parent class of all the classes in java by default.

<table class="alt">
<tbody><tr><th>Method</th><th>Description</th></tr>
<tr><td>public final Class getClass()</td><td>returns the Class class object of this object. The Class class can further be used to get the metadata of this class.</td></tr>
<tr><td>public int hashCode()</td><td> returns the hashcode number for this object.</td></tr>
<tr><td>public boolean equals(Object obj)</td><td> compares the given object to this object.</td></tr>
<tr><td>protected Object clone() throws CloneNotSupportedException</td><td> creates and returns the exact copy (clone) of this object.</td></tr>
<tr><td>public String toString()</td><td> returns the string representation of this object.</td></tr>
<tr><td>public final void notify()</td><td> wakes up single thread, waiting on this object's monitor.</td></tr>
<tr><td>public final void notifyAll()</td><td> wakes up all the threads, waiting on this object's monitor.</td></tr>
<tr><td>public final void wait(long timeout)throws InterruptedException</td><td> causes the current thread to wait for the specified milliseconds, until another thread notifies (invokes notify() or notifyAll() method).</td></tr>
<tr><td>public final void wait(long timeout,int nanos)throws InterruptedException</td><td>causes the current thread to wait for the specified milliseconds and nanoseconds, until another thread notifies (invokes notify() or notifyAll() method).</td></tr>
<tr><td>public final void wait()throws InterruptedException</td><td> causes the current thread to wait, until another thread notifies (invokes notify() or notifyAll() method).</td></tr>
<tr><td>protected void finalize()throws Throwable</td><td> is invoked by the garbage collector before object is being garbage collected.</td></tr>
</tbody></table>

### Example: Object Class Methods
```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person[name=" + name + ", age=" + age + "]";
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return age == person.age && name.equals(person.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}

public class ObjectClassExample {
    public static void main(String[] args) {
        Person person1 = new Person("John", 25);
        Person person2 = new Person("John", 25);

        // toString() method
        System.out.println(person1.toString());

        // equals() method
        System.out.println("Are persons equal? " + person1.equals(person2));

        // hashCode() method
        System.out.println("Person1 hashcode: " + person1.hashCode());
        System.out.println("Person2 hashcode: " + person2.hashCode());

        // getClass() method
        System.out.println("Class name: " + person1.getClass().getName());
    }
}
```
