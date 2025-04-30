# Few Things to Remember

## Definitions, Tips & Rules related to Java OOPS

### Class & Constructor

- *A class in Java can contain: fields, methods, constructors, blocks, nested class and interface.*
- *Object is an instance of a class.*
- *Constructor in java is a special type of method that is used to initialize the object.*
- *If there is no constructor in a class, compiler automatically creates a default constructor.*
- *There is no copy constructor in java. But, we can copy the values of one object to another like copy constructor in C++.*
- *A constructor can perform other tasks instead of initialization like object creation, starting a thread, calling method etc.*
- *You can perform any operation in the constructor as you perform in the method.*
- *Constructors can be overloaded, allowing different ways to initialize objects.*
- *Constructor chaining is possible using this() and super() calls.*
- *Private constructors are used to implement singleton pattern and prevent instantiation.*

```java
// Basic class example with enhanced features
class Car {
    // Fields (instance variables)
    private String brand;
    private String model;
    private int year;
    private static int totalCars = 0;  // Static field to track total cars

    // Default constructor
    public Car() {
        this("Unknown", "Unknown", 0);  // Constructor chaining
    }

    // Parameterized constructor
    public Car(String brand, String model, int year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
        totalCars++;
    }

    // Constructor with initialization tasks
    public Car(String brand) {
        this(brand, "Unknown", 0);  // Constructor chaining
        System.out.println("New car created: " + brand);
    }

    // Method to copy values from another car
    public void copyFrom(Car other) {
        this.brand = other.brand;
        this.model = other.model;
        this.year = other.year;
    }

    // Static method to get total cars
    public static int getTotalCars() {
        return totalCars;
    }

    // Getters and setters
    public String getBrand() { return brand; }
    public void setBrand(String brand) { this.brand = brand; }
    public String getModel() { return model; }
    public void setModel(String model) { this.model = model; }
    public int getYear() { return year; }
    public void setYear(int year) { this.year = year; }
}

// Singleton pattern example
class Database {
    private static Database instance;
    private String connectionString;

    // Private constructor to prevent instantiation
    private Database() {
        this.connectionString = "jdbc:mysql://localhost:3306/mydb";
    }

    // Static method to get instance
    public static Database getInstance() {
        if (instance == null) {
            instance = new Database();
        }
        return instance;
    }

    public String getConnectionString() {
        return connectionString;
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Creating cars using different constructors
        Car car1 = new Car();  // Uses default constructor
        Car car2 = new Car("Toyota", "Camry", 2023);  // Uses parameterized constructor
        Car car3 = new Car("Honda");  // Uses constructor with initialization

        // Copying values
        Car car4 = new Car();
        car4.copyFrom(car2);

        // Using singleton
        Database db1 = Database.getInstance();
        Database db2 = Database.getInstance();
        System.out.println(db1 == db2);  // true - same instance

        // Accessing static method
        System.out.println("Total cars created: " + Car.getTotalCars());
    }
}

// Additional example: Complex class with multiple constructors
class Employee {
    private String name;
    private int id;
    private double salary;
    private String department;
    private static int totalEmployees = 0;

    // Default constructor
    public Employee() {
        this("Unknown", 0, 0.0, "Unknown");
    }

    // Parameterized constructor
    public Employee(String name, int id, double salary, String department) {
        this.name = name;
        this.id = id;
        this.salary = salary;
        this.department = department;
        totalEmployees++;
    }

    // Constructor with default department
    public Employee(String name, int id, double salary) {
        this(name, id, salary, "General");
    }

    // Copy constructor (Java style)
    public Employee(Employee other) {
        this(other.name, other.id, other.salary, other.department);
    }

    // Static method to get total employees
    public static int getTotalEmployees() {
        return totalEmployees;
    }
}

// Usage of Employee class
Employee emp1 = new Employee();  // Uses default constructor
Employee emp2 = new Employee("John", 101, 50000.0, "IT");  // Full parameter constructor
Employee emp3 = new Employee("Jane", 102, 45000.0);  // Uses department default
Employee emp4 = new Employee(emp2);  // Creates a copy of emp2
System.out.println("Total Employees: " + Employee.getTotalEmployees());
```

### static Keyword

- *The static can be: variable (class variable), method (class method), block & nested class.*
- *Java static property is shared to all objects.*
- *A static method belongs to the class rather than object of a class.*
- *A static method can be invoked without the need for creating an instance of a class.*
- *A static method can access static data member and can change the value of it.*
- *The static method can not use non static data member or call non-static method directly.*
- *this and super cannot be used in static context.*
- *The main method is static because object is not required to call static method if it were non-static method, jvm create object first then call main() method that will lead the problem of extra memory allocation.*
- *A static block is used to initialize the static data member. It is executed before main method at the time of classloading.*
- *Static variables are initialized only once, at the start of the program execution.*
- *Static methods can be overloaded but cannot be overridden (they are hidden instead).*
- *Static nested classes can access only static members of the outer class.*

```java
class Counter {
    // Static variable (class variable)
    static int count = 0;

    // Static final variable (constant)
    static final int MAX_COUNT = 100;

    // Instance variable
    int instanceCount = 0;

    // Constructor
    Counter() {
        count++;
        instanceCount++;
    }

    // Static method
    static void displayCount() {
        System.out.println("Total count: " + count);
        // Cannot access instanceCount here - compile error
    }

    // Static block
    static {
        System.out.println("Static block executed first");
        // Can initialize static variables
        count = 0;
    }

    // Static nested class
    static class CounterInfo {
        void displayInfo() {
            System.out.println("Max count: " + MAX_COUNT);
            // Can only access static members of outer class
        }
    }
}

// Static utility class
class MathUtils {
    // Private constructor to prevent instantiation
    private MathUtils() {}

    // Static constants
    public static final double PI = 3.14159;
    public static final double E = 2.71828;

    // Static methods
    public static int max(int a, int b) {
        return (a > b) ? a : b;
    }

    public static double calculateCircleArea(double radius) {
        return PI * radius * radius;
    }

    // Static method overloading
    public static double max(double a, double b) {
        return (a > b) ? a : b;
    }

    // Static nested class
    public static class Constants {
        public static final double GRAVITY = 9.81;
        public static final double LIGHT_SPEED = 299792458;
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Using Counter class
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        Counter.displayCount();  // Can call without creating instance

        // Using static nested class
        Counter.CounterInfo info = new Counter.CounterInfo();
        info.displayInfo();

        // Using MathUtils
        double area = MathUtils.calculateCircleArea(5.0);
        int maximum = MathUtils.max(10, 20);
        double maxDouble = MathUtils.max(10.5, 20.5);
        double gravity = MathUtils.Constants.GRAVITY;

        // Demonstrating static method hiding
        Parent.staticMethod();  // Calls Parent's method
        Child.staticMethod();   // Calls Child's method (hiding, not overriding)
    }
}

// Static method hiding example
class Parent {
    static void staticMethod() {
        System.out.println("Parent's static method");
    }
}

class Child extends Parent {
    static void staticMethod() {
        System.out.println("Child's static method");
    }
}
```

### this Keyword

- *In Java, this is a reference variable that refers to the current object.*
- *Call to this() must be the first statement in constructor.*
- *this can be used to: refer current class instance variable, invoke current class method and constructor.*
- *this can be passed as an argument in the method and constructor call.*
- *this can be used to return the current class instance from the method.*
- *It is better approach to use meaningful names for variables. So we use same name for instance variables and parameters in real time, and always use this keyword.*
- *this can be used to differentiate between instance variables and local variables when they have the same name.*
- *this can be used to pass the current object as a parameter to another method.*
- *this can be used to return the current object from a method, enabling method chaining.*

```java
class Student {
    private String name;
    private int age;
    private String department;

    // Using this to refer to instance variables
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
        this.department = "General";
    }

    // Using this to call another constructor
    public Student() {
        this("Unknown", 0);  // Must be first statement
    }

    // Using this to return current instance (method chaining)
    public Student setName(String name) {
        this.name = name;
        return this;  // Enables method chaining
    }

    public Student setAge(int age) {
        this.age = age;
        return this;
    }

    public Student setDepartment(String department) {
        this.department = department;
        return this;
    }

    // Using this as method parameter
    public void printStudent(Student s) {
        System.out.println("Name: " + s.name + ", Age: " + s.age + ", Department: " + s.department);
    }

    public void printThisStudent() {
        printStudent(this);  // Passing current object
    }

    // Method to demonstrate this in instance method
    public void display() {
        System.out.println("Name: " + this.name);
        System.out.println("Age: " + this.age);
        System.out.println("Department: " + this.department);
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Creating student using constructor
        Student student1 = new Student("John", 20);

        // Method chaining using this
        Student student2 = new Student()
            .setName("Jane")
            .setAge(21)
            .setDepartment("Computer Science");

        // Using this to pass current object
        student1.printThisStudent();
        student2.printThisStudent();

        // Demonstrating this in instance method
        student1.display();
    }
}

// Additional example: Builder pattern using this
class CarBuilder {
    private String brand;
    private String model;
    private int year;
    private String color;

    public CarBuilder setBrand(String brand) {
        this.brand = brand;
        return this;
    }

    public CarBuilder setModel(String model) {
        this.model = model;
        return this;
    }

    public CarBuilder setYear(int year) {
        this.year = year;
        return this;
    }

    public CarBuilder setColor(String color) {
        this.color = color;
        return this;
    }

    public Car build() {
        return new Car(brand, model, year, color);
    }
}

// Usage of builder pattern
class Main {
    public static void main(String[] args) {
        Car car = new CarBuilder()
            .setBrand("Toyota")
            .setModel("Camry")
            .setYear(2023)
            .setColor("Red")
            .build();
    }
}
```

### Inheritance

- *Inheritance (IS-A) is a mechanism in which one object acquires all the properties and behaviors of parent object.*
- *The extends keyword indicates that you are making a new class that derives from an existing class.*
- *Multiple inheritance is not supported in Java through class. We can use Interface to perform it.*
- *To reduce the complexity and simplify the language, multiple inheritance is not supported in java.*
- *If a class have an entity reference, it is known as Aggregation (HAS-A relationship).*
- *Inheritance should be used only if the relationship is-a is maintained throughout the lifetime of the objects involved; otherwise, aggregation is the best choice.*
- *Java supports single inheritance for classes but multiple inheritance for interfaces.*
- *All classes in Java implicitly extend the Object class.*
- *Constructors are not inherited, but they can be invoked using super().*
- *Private members of the parent class are not accessible in the child class.*
- *The protected access modifier allows access within the same package and through inheritance.*

```java
// Parent class
class Animal {
    private String name;  // Private member
    protected int age;    // Protected member
    public String species; // Public member

    public Animal(String name, int age, String species) {
        this.name = name;
        this.age = age;
        this.species = species;
    }

    // Protected method
    protected void eat() {
        System.out.println(name + " is eating...");
    }

    // Public method
    public void sleep() {
        System.out.println(name + " is sleeping...");
    }

    // Final method - cannot be overridden
    public final void breathe() {
        System.out.println(name + " is breathing...");
    }
}

// Child class
class Dog extends Animal {
    private String breed;

    public Dog(String name, int age, String breed) {
        super(name, age, "Canine");  // Must be first statement
        this.breed = breed;
    }

    // Method overriding
    @Override
    protected void eat() {
        System.out.println("Dog " + super.species + " is eating bones...");
    }

    // New method specific to Dog
    public void bark() {
        System.out.println("Dog is barking...");
    }

    // Cannot override final method
    // public void breathe() { }  // Compile error
}

// HAS-A relationship (Aggregation)
class Engine {
    private String type;
    private int horsepower;

    public Engine(String type, int horsepower) {
        this.type = type;
        this.horsepower = horsepower;
    }

    public void start() {
        System.out.println("Engine started: " + type + " with " + horsepower + " HP");
    }
}

class Car {
    private String brand;
    private Engine engine;  // HAS-A relationship

    public Car(String brand, Engine engine) {
        this.brand = brand;
        this.engine = engine;
    }

    public void start() {
        System.out.println("Starting " + brand);
        engine.start();
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Inheritance example
        Dog dog = new Dog("Buddy", 3, "Labrador");
        dog.eat();      // Calls overridden method
        dog.sleep();    // Calls inherited method
        dog.bark();     // Calls Dog-specific method
        dog.breathe();  // Calls final method from Animal

        // Aggregation example
        Engine engine = new Engine("V6", 300);
        Car car = new Car("Toyota", engine);
        car.start();

        // Demonstrating protected access
        System.out.println("Dog's age: " + dog.age);  // Accessible through inheritance
        // System.out.println(dog.name);  // Not accessible - private
    }
}

// Additional example: Multi-level inheritance
class Vehicle {
    protected String brand;
    protected int year;

    public Vehicle(String brand, int year) {
        this.brand = brand;
        this.year = year;
    }

    public void displayInfo() {
        System.out.println("Brand: " + brand + ", Year: " + year);
    }
}

class Car extends Vehicle {
    private int numberOfDoors;

    public Car(String brand, int year, int numberOfDoors) {
        super(brand, year);
        this.numberOfDoors = numberOfDoors;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Number of doors: " + numberOfDoors);
    }
}

class ElectricCar extends Car {
    private int batteryCapacity;

    public ElectricCar(String brand, int year, int numberOfDoors, int batteryCapacity) {
        super(brand, year, numberOfDoors);
        this.batteryCapacity = batteryCapacity;
    }

    @Override
    public void displayInfo() {
        super.displayInfo();
        System.out.println("Battery capacity: " + batteryCapacity + " kWh");
    }
}
```

### Method Overloading

- *If a class has multiple methods having same name but different in parameters, it is known as Method Overloading.*
- *There are two ways to overload the method in java : by changing number of arguments, by changing the data type.*
- *In Java, Method Overloading is not possible by changing the return type of the method only because of ambiguity.*
- *Compile Time Error is better than Run Time Error. So, java compiler renders compiler time error if you declare the same method having same parameters.*
- *We can also overload Java main() method, but JVM calls main() method which receives string array as arguments only.*
- *One type is promoted to another implicitly if no matching datatype is found. eg. byte can be promoted to short, int, etc.*
- *If there are no matching type arguments method, and each method promotes similar number of arguments, there will be ambiguity.*
- *One type is not de-promoted implicitly for example double cannot be depromoted to any type implicitly.*
- *Method overloading can be done with different access modifiers.*
- *Method overloading can be done with different exception handling.*
- *Method overloading can be done with different static/non-static methods.*

```java
class Calculator {
    // Different number of parameters
    public int add(int a, int b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }

    // Different parameter types
    public double add(double a, double b) {
        return a + b;
    }

    // Different parameter order
    public void display(int a, String b) {
        System.out.println("int: " + a + ", String: " + b);
    }

    public void display(String a, int b) {
        System.out.println("String: " + a + ", int: " + b);
    }

    // Type promotion example
    public void display(int a) {
        System.out.println("int: " + a);
    }

    public void display(long a) {
        System.out.println("long: " + a);
    }

    // Different access modifiers
    protected int multiply(int a, int b) {
        return a * b;
    }

    public int multiply(int a, int b, int c) {
        return a * b * c;
    }

    // Different exception handling
    public void divide(int a, int b) throws ArithmeticException {
        if (b == 0) throw new ArithmeticException("Division by zero");
        System.out.println(a / b);
    }

    public void divide(double a, double b) {
        if (b == 0) {
            System.out.println("Cannot divide by zero");
            return;
        }
        System.out.println(a / b);
    }

    // Static method overloading
    public static int subtract(int a, int b) {
        return a - b;
    }

    public static double subtract(double a, double b) {
        return a - b;
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();

        // Different number of parameters
        System.out.println(calc.add(5, 10));        // Calls first method
        System.out.println(calc.add(5, 10, 15));    // Calls second method

        // Different parameter types
        System.out.println(calc.add(5.5, 10.5));    // Calls third method

        // Different parameter order
        calc.display(10, "Hello");
        calc.display("Hello", 10);

        // Type promotion
        byte b = 5;
        calc.display(b);  // Promoted to int

        // Different access modifiers
        System.out.println(calc.multiply(5, 10));
        System.out.println(calc.multiply(5, 10, 2));

        // Different exception handling
        try {
            calc.divide(10, 2);
            calc.divide(10, 0);
        } catch (ArithmeticException e) {
            System.out.println(e.getMessage());
        }

        // Static method overloading
        System.out.println(Calculator.subtract(10, 5));
        System.out.println(Calculator.subtract(10.5, 5.5));

        // Overloaded main method
        main("Test");  // Calls overloaded main
    }

    // Overloaded main method
    public static void main(String arg) {
        System.out.println("Overloaded main: " + arg);
    }
}

// Additional example: Constructor overloading
class Person {
    private String name;
    private int age;
    private String address;

    // Default constructor
    public Person() {
        this("Unknown", 0, "Unknown");
    }

    // Constructor with name only
    public Person(String name) {
        this(name, 0, "Unknown");
    }

    // Constructor with name and age
    public Person(String name, int age) {
        this(name, age, "Unknown");
    }

    // Full parameter constructor
    public Person(String name, int age, String address) {
        this.name = name;
        this.age = age;
        this.address = address;
    }

    // Copy constructor
    public Person(Person other) {
        this(other.name, other.age, other.address);
    }
}
```

### Method Overriding

- *If subclass (child class) has the same method as declared in the parent class, it is known as method overriding.*
- *Method must have same name and parameters as in the parent class for overriding.*
- *Method overriding is used to provide specific implementation of a method that is already provided by its super class. Also used for runtime polymorphism.*
- *We cannot override static method (not also main method) because static method is bound with class whereas instance method is bound with object. Static belongs to class area and instance belongs to heap area.*
- *Method Overriding with Access Modifier: if you are overriding a method, overridden method (i.e. declared in subclass) must not be more restrictive.*
- *Covariant Return Type: It is possible to override method by changing the return type if subclass overrides any method whose return type is Non-Primitive but it changes its return type to subclass type.*
- *Private methods cannot be overridden as they are not visible to the child class.*
- *Final methods cannot be overridden.*
- *Constructors cannot be overridden.*
- *The @Override annotation is used to ensure that a method is actually overriding a method from the parent class.*

```java
// Parent class
class Bank {
    protected double balance;

    public Bank(double balance) {
        this.balance = balance;
    }

    // Method to be overridden
    public double getRateOfInterest() {
        return 0.0;
    }

    // Final method - cannot be overridden
    public final void displayBalance() {
        System.out.println("Current balance: " + balance);
    }

    // Private method - cannot be overridden
    private void internalProcess() {
        System.out.println("Internal processing");
    }

    // Method with covariant return type
    public Bank getBankDetails() {
        return this;
    }
}

// Child class
class SBI extends Bank {
    public SBI(double balance) {
        super(balance);
    }

    // Method overriding
    @Override
    public double getRateOfInterest() {
        return 8.0;
    }

    // Cannot override final method
    // public void displayBalance() { }  // Compile error

    // Cannot override private method
    // private void internalProcess() { }  // This is a new method, not overriding

    // Covariant return type
    @Override
    public SBI getBankDetails() {
        return this;
    }

    // Additional method specific to SBI
    public void sbiSpecificMethod() {
        System.out.println("SBI specific processing");
    }
}

// Another child class
class ICICI extends Bank {
    public ICICI(double balance) {
        super(balance);
    }

    @Override
    public double getRateOfInterest() {
        return 7.0;
    }

    // Cannot make access more restrictive
    // protected double getRateOfInterest() { return 7.0; }  // Compile error
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Runtime polymorphism
        Bank bank1 = new SBI(10000);
        Bank bank2 = new ICICI(20000);

        System.out.println("SBI Rate: " + bank1.getRateOfInterest());
        System.out.println("ICICI Rate: " + bank2.getRateOfInterest());

        // Using final method
        bank1.displayBalance();
        bank2.displayBalance();

        // Using covariant return type
        SBI sbi = new SBI(5000);
        SBI details = sbi.getBankDetails();
        details.sbiSpecificMethod();

        // Demonstrating method hiding (static methods)
        Parent.staticMethod();
        Child.staticMethod();
    }
}

// Additional example: Method hiding with static methods
class Parent {
    public static void staticMethod() {
        System.out.println("Parent's static method");
    }
}

class Child extends Parent {
    public static void staticMethod() {
        System.out.println("Child's static method");
    }
}

// Additional example: Abstract class with method overriding
abstract class Shape {
    protected String color;

    public Shape(String color) {
        this.color = color;
    }

    // Abstract method to be overridden
    public abstract double calculateArea();

    // Concrete method
    public void displayColor() {
        System.out.println("Shape color: " + color);
    }
}

class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double length;
    private double width;

    public Rectangle(String color, double length, double width) {
        super(color);
        this.length = length;
        this.width = width;
    }

    @Override
    public double calculateArea() {
        return length * width;
    }
}
```

### super Keyword

- *The super keyword is a reference variable which is used to refer immediate parent class object.*
- *super can be used to refer immediate parent class instance variable or invoke immediate parent class method and constructor.*
- *super() is added in each class constructor automatically by compiler if there is no super() or this().*
- *super() must be the first statement in the constructor.*
- *super can be used to access hidden fields of the parent class.*
- *super can be used to call overridden methods of the parent class.*
- *super cannot be used in static context.*
- *super can be used to access parent class constructors with different parameters.*

```java
class Animal {
    String color = "white";
    protected String name;

    Animal() {
        System.out.println("Animal default constructor");
    }

    Animal(String name) {
        this.name = name;
        System.out.println("Animal parameterized constructor");
    }

    void eat() {
        System.out.println("Animal is eating...");
    }

    void display() {
        System.out.println("Animal display");
    }
}

class Dog extends Animal {
    String color = "black";
    private String breed;

    Dog() {
        super();  // Calls parent default constructor
        System.out.println("Dog default constructor");
    }

    Dog(String name, String breed) {
        super(name);  // Calls parent parameterized constructor
        this.breed = breed;
        System.out.println("Dog parameterized constructor");
    }

    void printColor() {
        System.out.println("Dog color: " + color);        // Prints black
        System.out.println("Animal color: " + super.color);  // Prints white
    }

    @Override
    void eat() {
        System.out.println("Dog is eating bones...");
        super.eat();  // Calls parent method
    }

    void display() {
        super.display();  // Calls parent method
        System.out.println("Dog display");
    }

    void showDetails() {
        System.out.println("Name: " + name);  // Accessing protected field
        System.out.println("Breed: " + breed);
    }
}

// Multi-level inheritance example
class Mammal extends Animal {
    protected boolean hasFur;

    Mammal(String name, boolean hasFur) {
        super(name);
        this.hasFur = hasFur;
    }

    void displayMammal() {
        System.out.println("Mammal display");
        super.display();  // Calls Animal's display
    }
}

class Cat extends Mammal {
    private String color;

    Cat(String name, boolean hasFur, String color) {
        super(name, hasFur);
        this.color = color;
    }

    @Override
    void display() {
        super.display();  // Calls Mammal's display
        System.out.println("Cat display");
    }

    void showAllDetails() {
        System.out.println("Name: " + name);  // From Animal
        System.out.println("Has fur: " + hasFur);  // From Mammal
        System.out.println("Color: " + color);  // From Cat
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Basic super usage
        Dog dog = new Dog();
        dog.printColor();
        dog.eat();
        dog.display();

        // Parameterized constructor
        Dog dog2 = new Dog("Buddy", "Labrador");
        dog2.showDetails();

        // Multi-level inheritance
        Cat cat = new Cat("Whiskers", true, "Gray");
        cat.display();
        cat.showAllDetails();

        // Demonstrating constructor chaining
        new Cat("Tom", true, "Black");
    }
}

// Additional example: Constructor chaining
class Vehicle {
    private String brand;
    private int year;

    Vehicle(String brand, int year) {
        this.brand = brand;
        this.year = year;
        System.out.println("Vehicle constructor");
    }
}

class Car extends Vehicle {
    private String model;

    Car(String brand, int year, String model) {
        super(brand, year);  // Must be first statement
        this.model = model;
        System.out.println("Car constructor");
    }
}

class ElectricCar extends Car {
    private int batteryCapacity;

    ElectricCar(String brand, int year, String model, int batteryCapacity) {
        super(brand, year, model);
        this.batteryCapacity = batteryCapacity;
        System.out.println("ElectricCar constructor");
    }
}
```

### final Keyword

- *The final keyword in java is used to restrict the user.*
- *You cannot change the value of final variable(It will be constant).*
- *If you make any method as final, you cannot override it.*
- *If you make any class as final, you cannot extend it.*
- *Final method is inherited but you cannot override it.*
- *A final variable that is not initialized at the time of declaration is known as blank final variable.*
- *We can initialize a blank final variable only in constructor.*
- *A static final variable that is not initialized at the time of declaration is known as static blank final variable. It can be initialized only in static block.*
- *If you declare any parameter as final, you cannot change the value of it.*
- *A constructor cannot be declared final because it is never inherited.*
- *Final variables can be initialized in instance initializer blocks.*
- *Final variables can be used in lambda expressions and anonymous classes.*
- *Final variables can be used to create immutable objects.*

```java
// Final variable examples
class FinalExample {
    // Final variable (constant)
    final int MAX_VALUE = 100;

    // Blank final variable
    final int MIN_VALUE;

    // Static blank final variable
    static final int DEFAULT_VALUE;

    // Final object reference
    final List<String> names = new ArrayList<>();

    // Static block
    static {
        DEFAULT_VALUE = 50;
    }

    // Constructor
    FinalExample() {
        MIN_VALUE = 0;  // Must initialize in constructor
    }

    // Parameterized constructor
    FinalExample(int minValue) {
        MIN_VALUE = minValue;
    }

    // Final method
    final void display() {
        System.out.println("This is a final method");
    }

    // Method with final parameter
    void process(final int value) {
        // value = 10;  // Cannot modify final parameter
        System.out.println("Processing value: " + value);
    }

    // Method demonstrating final object reference
    void addName(String name) {
        names.add(name);  // Can modify object's state
        // names = new ArrayList<>();  // Cannot reassign reference
    }
}

// Final class
final class FinalClass {
    void display() {
        System.out.println("This is a final class");
    }
}

// Cannot extend FinalClass
// class Child extends FinalClass { }  // Compile error

// Immutable class using final
final class ImmutablePerson {
    private final String name;
    private final int age;
    private final List<String> hobbies;

    public ImmutablePerson(String name, int age, List<String> hobbies) {
        this.name = name;
        this.age = age;
        this.hobbies = new ArrayList<>(hobbies);  // Defensive copy
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public List<String> getHobbies() {
        return new ArrayList<>(hobbies);  // Defensive copy
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Final variable examples
        FinalExample example = new FinalExample();
        example.process(42);
        example.addName("John");
        example.addName("Jane");

        // Immutable class usage
        List<String> hobbies = new ArrayList<>();
        hobbies.add("Reading");
        hobbies.add("Swimming");

        ImmutablePerson person = new ImmutablePerson("Alice", 30, hobbies);
        System.out.println("Name: " + person.getName());
        System.out.println("Age: " + person.getAge());
        System.out.println("Hobbies: " + person.getHobbies());

        // Demonstrating immutability
        hobbies.add("Running");  // Original list is modified
        System.out.println("Person's hobbies: " + person.getHobbies());  // Unchanged

        // Final in lambda expressions
        final int multiplier = 2;
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        numbers.forEach(n -> System.out.println(n * multiplier));
    }
}

// Additional example: Final in inheritance
class Parent {
    // Final method
    final void finalMethod() {
        System.out.println("Parent's final method");
    }

    // Non-final method
    void nonFinalMethod() {
        System.out.println("Parent's non-final method");
    }
}

class Child extends Parent {
    // Cannot override final method
    // void finalMethod() { }  // Compile error

    // Can override non-final method
    @Override
    void nonFinalMethod() {
        System.out.println("Child's non-final method");
    }
}

// Additional example: Final in anonymous classes
class AnonymousExample {
    void process() {
        final int localVar = 10;

        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("Local variable: " + localVar);
                // localVar = 20;  // Cannot modify final variable
            }
        };

        new Thread(r).start();
    }
}
```

### Runtime Polymorphism

- *Polymorphism is a concept by which we can perform a single action by different ways.*
- *There are two types of polymorphism in java: compile time polymorphism and runtime polymorphism.*
- *We can perform polymorphism in java by method overloading and method overriding.*
- *If you overload static method in java, it is the example of compile time polymorphism.*
- *In Runtime polymorphism (Dynamic Method Dispatch), an overridden method is resolved at runtime rather than compile-time.*
- *A Virtual Method is an inheritable and overridable method for which dynamic dispatch is facilitated.*
- *All non-static, non-final and non-private methods are Virtual Methods by default.*
- *When reference variable of Parent class refers to the object of Child class, it is known as upcasting.*
- *Method is overridden not the datamembers, so runtime polymorphism can't be achieved by data members.*
- *Connecting a method call to the method body is known as binding.*
- *There are two types of binding : Static binding (early binding) and Dynamic binding (late binding).*
- *Runtime polymorphism is achieved through method overriding and inheritance.*
- *The JVM determines which method to call at runtime based on the actual object type.*
- *Runtime polymorphism allows for more flexible and extensible code.*

```java
// Base class
class Shape {
    protected String color;

    public Shape(String color) {
        this.color = color;
    }

    // Virtual method
    public double calculateArea() {
        System.out.println("Calculating area of generic shape");
        return 0.0;
    }

    public void display() {
        System.out.println("Shape color: " + color);
    }

    // Static method (compile-time polymorphism)
    public static void printType() {
        System.out.println("This is a Shape");
    }
}

// Derived classes
class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }

    @Override
    public void display() {
        super.display();
        System.out.println("Circle radius: " + radius);
    }

    // Method hiding (not overriding)
    public static void printType() {
        System.out.println("This is a Circle");
    }
}

class Rectangle extends Shape {
    private double length;
    private double width;

    public Rectangle(String color, double length, double width) {
        super(color);
        this.length = length;
        this.width = width;
    }

    @Override
    public double calculateArea() {
        return length * width;
    }

    @Override
    public void display() {
        super.display();
        System.out.println("Rectangle dimensions: " + length + "x" + width);
    }

    // Method hiding
    public static void printType() {
        System.out.println("This is a Rectangle");
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Runtime polymorphism
        Shape shape1 = new Circle("Red", 5.0);  // Upcasting
        Shape shape2 = new Rectangle("Blue", 4.0, 6.0);  // Upcasting

        // Dynamic method dispatch
        System.out.println("Circle area: " + shape1.calculateArea());
        System.out.println("Rectangle area: " + shape2.calculateArea());

        // Method calls are resolved at runtime
        shape1.display();
        shape2.display();

        // Static method calls (compile-time polymorphism)
        Shape.printType();
        Circle.printType();
        Rectangle.printType();

        // Demonstrating method hiding vs overriding
        Shape circle = new Circle("Green", 3.0);
        circle.printType();  // Calls Shape's printType (static method)
        ((Circle)circle).printType();  // Calls Circle's printType

        // Array of shapes
        Shape[] shapes = new Shape[3];
        shapes[0] = new Circle("Yellow", 2.0);
        shapes[1] = new Rectangle("Purple", 3.0, 4.0);
        shapes[2] = new Circle("Orange", 1.0);

        // Polymorphic method calls
        for (Shape shape : shapes) {
            System.out.println("Area: " + shape.calculateArea());
            shape.display();
        }
    }
}

// Additional example: Interface-based polymorphism
interface Drawable {
    void draw();
    default void display() {
        System.out.println("Displaying drawable object");
    }
}

class Circle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing circle");
    }
}

class Rectangle implements Drawable {
    @Override
    public void draw() {
        System.out.println("Drawing rectangle");
    }
}

// Usage of interface-based polymorphism
class Main {
    public static void main(String[] args) {
        Drawable[] drawables = new Drawable[2];
        drawables[0] = new Circle();
        drawables[1] = new Rectangle();

        for (Drawable d : drawables) {
            d.draw();
            d.display();
        }
    }
}

// Additional example: Abstract class polymorphism
abstract class Animal {
    protected String name;

    public Animal(String name) {
        this.name = name;
    }

    abstract void makeSound();

    public void display() {
        System.out.println("Animal name: " + name);
    }
}

class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    @Override
    void makeSound() {
        System.out.println("Woof!");
    }
}

class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }

    @Override
    void makeSound() {
        System.out.println("Meow!");
    }
}

// Usage of abstract class polymorphism
class Main {
    public static void main(String[] args) {
        Animal[] animals = new Animal[2];
        animals[0] = new Dog("Buddy");
        animals[1] = new Cat("Whiskers");

        for (Animal animal : animals) {
            animal.display();
            animal.makeSound();
        }
    }
}
```

### instanceof Keyword

- *instanceof operator is used to test whether the object is an instance of the specified type (class/subclass/interface).*
- *When Subclass type refers to the object of Parent class, it is known as downcasting.*
- *If we perform downcasting directly, there is compile error.*
- *If we perform downcasting by typecasting, ClassCastException is thrown at runtime.*
- *If we use instanceof operator, downcasting is possible!*
- *instanceof operator returns true if the object is an instance of the specified type or its subclass.*
- *instanceof operator returns false if the object is null.*
- *instanceof operator can be used with interfaces.*
- *instanceof operator can be used to check array types.*
- *instanceof operator is useful for type checking before performing operations.*

```java
// Base class
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}

// Derived classes
class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}

class Cat extends Animal {
    void meow() {
        System.out.println("Cat is meowing");
    }
}

// Interface
interface Swimmable {
    void swim();
}

class Fish extends Animal implements Swimmable {
    @Override
    public void swim() {
        System.out.println("Fish is swimming");
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Basic instanceof usage
        Animal animal = new Dog();
        System.out.println(animal instanceof Animal);  // true
        System.out.println(animal instanceof Dog);     // true
        System.out.println(animal instanceof Cat);     // false

        // Safe downcasting with instanceof
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;  // Safe downcasting
            dog.bark();
        }

        // Interface checking
        Animal fish = new Fish();
        System.out.println(fish instanceof Swimmable);  // true
        if (fish instanceof Swimmable) {
            ((Swimmable) fish).swim();
        }

        // Null checking
        Animal nullAnimal = null;
        System.out.println(nullAnimal instanceof Animal);  // false

        // Array type checking
        int[] numbers = new int[5];
        System.out.println(numbers instanceof int[]);     // true
        System.out.println(numbers instanceof Object);    // true

        // Complex example with multiple checks
        processAnimal(new Dog());
        processAnimal(new Cat());
        processAnimal(new Fish());
        processAnimal(null);
    }

    // Method demonstrating instanceof usage
    static void processAnimal(Animal animal) {
        if (animal == null) {
            System.out.println("Animal is null");
            return;
        }

        animal.eat();

        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;
            dog.bark();
        } else if (animal instanceof Cat) {
            Cat cat = (Cat) animal;
            cat.meow();
        }

        if (animal instanceof Swimmable) {
            ((Swimmable) animal).swim();
        }
    }
}

// Additional example: instanceof with generics
class GenericExample<T> {
    private T value;

    public GenericExample(T value) {
        this.value = value;
    }

    public void process() {
        if (value instanceof String) {
            String str = (String) value;
            System.out.println("String length: " + str.length());
        } else if (value instanceof Number) {
            Number num = (Number) value;
            System.out.println("Number value: " + num.doubleValue());
        }
    }
}

// Usage of generic example
class Main {
    public static void main(String[] args) {
        GenericExample<String> strExample = new GenericExample<>("Hello");
        strExample.process();

        GenericExample<Integer> intExample = new GenericExample<>(42);
        intExample.process();
    }
}

// Additional example: instanceof with inheritance hierarchy
class Vehicle {
    void start() {
        System.out.println("Vehicle starting");
    }
}

class Car extends Vehicle {
    void drive() {
        System.out.println("Car driving");
    }
}

class ElectricCar extends Car {
    void charge() {
        System.out.println("Electric car charging");
    }
}

// Usage of inheritance hierarchy
class Main {
    public static void main(String[] args) {
        Vehicle vehicle = new ElectricCar();

        // Checking inheritance hierarchy
        System.out.println(vehicle instanceof Vehicle);      // true
        System.out.println(vehicle instanceof Car);          // true
        System.out.println(vehicle instanceof ElectricCar);  // true

        // Safe downcasting through hierarchy
        if (vehicle instanceof ElectricCar) {
            ElectricCar electricCar = (ElectricCar) vehicle;
            electricCar.charge();
        }
    }
}
```

### Abstract Class

- *A class that is declared as abstract (keyword) is abstract class. It can have abstract and non-abstract methods.*
- *Abstraction is a process of hiding the implementation details and showing only functionality to the user.*
- *There are two ways to achieve abstraction in java : Abstract class (0 to 100%) and Interface (100%).*
- *A method that is declared as abstract and does not have implementation is abstract method.*
- *Any method with a body is non-abstract method.*
- *An abstract class can have data member, abstract method, method body, constructor and even main() method.*
- *If there is any abstract method in a class, that class must be abstract.*
- *If extending any abstract class that have abstract method, we must either provide the implementation of the method or make this class abstract.*
- *Abstract class can also be used to provide some implementation of an interface. Then, the end user extending thtis abstract class is free to skip implementing that method while overriding all the methods of the interface.*

```java
abstract class Shape {
    abstract void draw();  // Abstract method

    void display() {       // Non-abstract method
        System.out.println("Displaying shape");
    }
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing circle");
    }
}

// Usage
Shape shape = new Circle();
shape.draw();
shape.display();
```

### Interface

- *An interface in java is a blueprint of a class. It has static constants and abstract methods.*
- *Since Java 8, we can have method body in interface. But we need to make it default or static method.*
- *The interface is a mechanism to achieve abstraction. It represents IS-A relationship.*
- *By using interface, we can support multiple inheritance.*
- *It can be also used to achieve loose coupling (coupling is degree of direct knowledge that one element has of another).*
- *The Java compiler adds public & abstract before the interface method. Adds public, static & final before data members.*
- *A class extends another class, an interface extends another interface but a class implements an interface.*
- *Multiple inheritance is not supported by class because of ambiguity. But, supported by interface because there is no ambiguity as implementation is provided by the implementation class.*
- *An interface with no member is called marker/tagged interface. For example: Serializable, Cloneable, Remote etc.*
- *Marker interface are used to provide essential information to JVM, so that JVM may perform some useful operation.*
- *An interface can have another interface i.e. known as nested interface.*
- *Since Java 9, interfaces can have private methods.*
- *Interfaces can have static methods with implementation.*
- *Interfaces can extend multiple interfaces.*
- *Interfaces can have default methods with implementation.*

```java
// Basic interface
interface Drawable {
    // Constant (public static final by default)
    String DEFAULT_COLOR = "Black";

    // Abstract method (public abstract by default)
    void draw();

    // Default method (Java 8+)
    default void display() {
        System.out.println("Displaying drawable object");
    }

    // Static method (Java 8+)
    static void printType() {
        System.out.println("This is a Drawable");
    }

    // Private method (Java 9+)
    private void internalProcess() {
        System.out.println("Internal processing");
    }
}

// Interface extending another interface
interface Resizable extends Drawable {
    void resize(int width, int height);
}

// Multiple inheritance through interfaces
interface Printable {
    void print();
}

// Class implementing multiple interfaces
class Rectangle implements Drawable, Printable {
    private String color;
    private int width;
    private int height;

    public Rectangle(String color, int width, int height) {
        this.color = color;
        this.width = width;
        this.height = height;
    }

    @Override
    public void draw() {
        System.out.println("Drawing rectangle with color: " + color);
    }

    @Override
    public void print() {
        System.out.println("Printing rectangle");
    }

    // Using default method from interface
    public void show() {
        display();
    }
}

// Marker interface example
interface Cloneable {
    // No methods - just a marker
}

class Document implements Cloneable {
    private String content;

    public Document(String content) {
        this.content = content;
    }

    public Document clone() {
        return new Document(this.content);
    }
}

// Nested interface example
interface Vehicle {
    void start();
    void stop();

    // Nested interface
    interface Engine {
        void start();
        void stop();
    }
}

class Car implements Vehicle {
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }

    @Override
    public void start() {
        System.out.println("Car starting");
        engine.start();
    }

    @Override
    public void stop() {
        System.out.println("Car stopping");
        engine.stop();
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Using basic interface
        Drawable drawable = new Rectangle("Red", 10, 20);
        drawable.draw();
        drawable.display();
        Drawable.printType();

        // Using multiple interfaces
        Rectangle rectangle = new Rectangle("Blue", 15, 25);
        rectangle.draw();
        rectangle.print();
        rectangle.show();

        // Using marker interface
        Document doc1 = new Document("Hello");
        Document doc2 = doc1.clone();

        // Using nested interface
        Vehicle.Engine engine = new Vehicle.Engine() {
            @Override
            public void start() {
                System.out.println("Engine starting");
            }

            @Override
            public void stop() {
                System.out.println("Engine stopping");
            }
        };

        Car car = new Car(engine);
        car.start();
        car.stop();
    }
}

// Additional example: Functional Interface
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);

    // Can have default methods
    default void displayResult(int result) {
        System.out.println("Result: " + result);
    }

    // Can have static methods
    static void printOperation(String operation) {
        System.out.println("Performing: " + operation);
    }
}

// Usage of functional interface
class Main {
    public static void main(String[] args) {
        // Using lambda expression
        Calculator add = (a, b) -> a + b;
        Calculator subtract = (a, b) -> a - b;

        int result1 = add.calculate(10, 5);
        add.displayResult(result1);

        int result2 = subtract.calculate(10, 5);
        subtract.displayResult(result2);

        Calculator.printOperation("Addition");
    }
}

// Additional example: Interface with private methods
interface Logger {
    default void logInfo(String message) {
        log("INFO", message);
    }

    default void logError(String message) {
        log("ERROR", message);
    }

    private void log(String level, String message) {
        System.out.println("[" + level + "] " + message);
    }
}

class FileLogger implements Logger {
    public void logToFile(String message) {
        logInfo(message);
    }
}
```

### Package

- *A java package is a group of similar types of classes, interfaces and sub-packages.*
- *Java package is used to categorize the classes and interfaces, provides access protection and removes naming collision.*
- *The package keyword is used to create a package. Package inside the package is called the subpackage.*
- *If you import a package (package.* ), subpackages will not be imported.*
- *To import subpackage, use import package.classname.*
- *Use fully qualified name to access only the declared class of a package.*
- *Sequence of the program must be package then import then class.*
- *The standard of defining package is domain.company.package. eg - com.oracle.database*
- *There can be only one public class in a java source file and it must be saved by the public class name.*


```java
// File: com/example/vehicle/Car.java
package com.example.vehicle;

public class Car {
    public void display() {
        System.out.println("This is a car");
    }
}

// File: com/example/test/Test.java
package com.example.test;

import com.example.vehicle.Car;

public class Test {
    public static void main(String[] args) {
        Car car = new Car();
        car.display();
    }
}
```

### Access Modifiers

- *There are two types of modifiers in java: access modifiers and non-access modifiers.*
- *There are 4 types of java access modifiers: private, default, protected & public.*
- *There are many non-access modifiers such as static, abstract, synchronized, native, volatile, transient etc.*
- *The private access modifier is accessible only within class.*
- *If you make any class constructor private, you cannot create the instance of that class from outside the class.*
- *If we don't use any modifier, it is treated as default. Default modifier is accessible only within package.*
- *A Class cannot be private or protected except nested class.*
- *The protected access modifier is accessible within package and outside the package but through inheritance only.*
- *The public access modifier is accessible everywhere. It has the widest scope among all other modifiers.*
- *If you are overriding any method, overridden method (i.e. declared in subclass) must not be more restrictive.*
- *Access modifiers can be applied to classes, methods, variables, and constructors.*
- *Access modifiers control the visibility and accessibility of class members.*

```java
// Example demonstrating different access modifiers
class AccessExample {
    // Private members - accessible only within this class
    private int privateVar = 1;
    private void privateMethod() {
        System.out.println("Private method");
    }

    // Default (package-private) members - accessible within package
    int defaultVar = 2;
    void defaultMethod() {
        System.out.println("Default method");
    }

    // Protected members - accessible within package and through inheritance
    protected int protectedVar = 3;
    protected void protectedMethod() {
        System.out.println("Protected method");
    }

    // Public members - accessible everywhere
    public int publicVar = 4;
    public void publicMethod() {
        System.out.println("Public method");
    }

    // Private constructor - can be used for singleton pattern
    private AccessExample() {
        System.out.println("Private constructor");
    }

    // Public static method to create instance
    public static AccessExample createInstance() {
        return new AccessExample();
    }
}

// Subclass in the same package
class Subclass extends AccessExample {
    void testAccess() {
        // privateVar and privateMethod() not accessible
        System.out.println(defaultVar);      // Accessible in same package
        System.out.println(protectedVar);    // Accessible through inheritance
        System.out.println(publicVar);       // Accessible everywhere

        defaultMethod();     // Accessible in same package
        protectedMethod();   // Accessible through inheritance
        publicMethod();      // Accessible everywhere
    }
}

// Class in a different package
package com.example.other;

import com.example.AccessExample;

class OtherPackageClass extends AccessExample {
    void testAccess() {
        // privateVar, privateMethod(), defaultVar, defaultMethod() not accessible
        System.out.println(protectedVar);    // Accessible through inheritance
        System.out.println(publicVar);       // Accessible everywhere

        protectedMethod();   // Accessible through inheritance
        publicMethod();      // Accessible everywhere
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Creating instance using factory method
        AccessExample example = AccessExample.createInstance();

        // Accessing public members
        System.out.println(example.publicVar);
        example.publicMethod();

        // Cannot access private members
        // System.out.println(example.privateVar);
        // example.privateMethod();

        // Testing access in same package
        Subclass subclass = new Subclass();
        subclass.testAccess();

        // Demonstrating method overriding access rules
        Parent parent = new Parent();
        Child child = new Child();
        parent.display();  // Calls Parent's method
        child.display();   // Calls Child's method
    }
}

// Additional example: Method overriding with access modifiers
class Parent {
    protected void display() {
        System.out.println("Parent's display");
    }
}

class Child extends Parent {
    // Can make access more permissive
    @Override
    public void display() {
        System.out.println("Child's display");
    }

    // Cannot make access more restrictive
    // @Override
    // void display() { }  // Compile error
}

// Additional example: Nested class access modifiers
class OuterClass {
    private int privateVar = 10;
    protected int protectedVar = 20;
    public int publicVar = 30;

    // Private nested class
    private class PrivateNested {
        void display() {
            System.out.println("Private nested: " + privateVar);
        }
    }

    // Protected nested class
    protected class ProtectedNested {
        void display() {
            System.out.println("Protected nested: " + protectedVar);
        }
    }

    // Public nested class
    public class PublicNested {
        void display() {
            System.out.println("Public nested: " + publicVar);
        }
    }

    // Method to demonstrate nested class access
    public void testNestedClasses() {
        PrivateNested privateNested = new PrivateNested();
        privateNested.display();

        ProtectedNested protectedNested = new ProtectedNested();
        protectedNested.display();

        PublicNested publicNested = new PublicNested();
        publicNested.display();
    }
}

// Usage of nested classes
class Main {
    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        outer.testNestedClasses();

        // Can create instances of public and protected nested classes
        OuterClass.PublicNested publicNested = outer.new PublicNested();
        OuterClass.ProtectedNested protectedNested = outer.new ProtectedNested();
        // OuterClass.PrivateNested privateNested = outer.new PrivateNested();  // Not accessible
    }
}
```

### Encapsulation

- *Encapsulation is a process of wrapping code and data together into a single unit.*
- *To create a fully encapsulated class, make all data members of the class private, & use setter/getter methods to access data.*
- *By providing only setter or getter method, you can make the class read-only or write-only.*
- *Encapsulation provides data hiding and protection.*
- *Encapsulation helps in maintaining the integrity of data.*
- *Encapsulation makes the code more maintainable and flexible.*
- *Encapsulation allows for validation of data before setting values.*
- *Encapsulation enables the implementation of business logic in getters and setters.*

```java
// Fully encapsulated class
class Student {
    // Private data members
    private String name;
    private int age;
    private String department;
    private double gpa;
    private final String studentId;  // Final field - can only be set once

    // Constructor
    public Student(String name, int age, String department, String studentId) {
        this.name = name;
        setAge(age);  // Using setter for validation
        this.department = department;
        this.studentId = studentId;
        this.gpa = 0.0;
    }

    // Getter methods
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getDepartment() {
        return department;
    }

    public double getGpa() {
        return gpa;
    }

    public String getStudentId() {
        return studentId;
    }

    // Setter methods with validation
    public void setName(String name) {
        if (name != null && !name.isEmpty()) {
            this.name = name;
        } else {
            System.out.println("Invalid name");
        }
    }

    public void setAge(int age) {
        if (age >= 0 && age <= 120) {
            this.age = age;
        } else {
            System.out.println("Invalid age");
        }
    }

    public void setDepartment(String department) {
        if (department != null && !department.isEmpty()) {
            this.department = department;
        } else {
            System.out.println("Invalid department");
        }
    }

    public void setGpa(double gpa) {
        if (gpa >= 0.0 && gpa <= 4.0) {
            this.gpa = gpa;
        } else {
            System.out.println("Invalid GPA");
        }
    }

    // Business logic methods
    public void updateGpa(double newGrade, int credits) {
        if (newGrade >= 0.0 && newGrade <= 4.0 && credits > 0) {
            double totalPoints = this.gpa * getTotalCredits() + newGrade * credits;
            int totalCredits = getTotalCredits() + credits;
            this.gpa = totalPoints / totalCredits;
        } else {
            System.out.println("Invalid grade or credits");
        }
    }

    // Private helper method
    private int getTotalCredits() {
        // Implementation to get total credits
        return 30;  // Example value
    }

    // Public method to display student information
    public void displayInfo() {
        System.out.println("Student ID: " + studentId);
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Department: " + department);
        System.out.println("GPA: " + gpa);
    }
}

// Read-only class example
class ReadOnlyPerson {
    private final String name;
    private final int age;

    public ReadOnlyPerson(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Only getters, no setters
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

// Write-only class example
class WriteOnlyLogger {
    private String logFile;

    // Only setter, no getter
    public void setLogFile(String logFile) {
        this.logFile = logFile;
    }

    public void log(String message) {
        // Implementation to log message to file
        System.out.println("Logging to " + logFile + ": " + message);
    }
}

// Usage examples
public class Main {
    public static void main(String[] args) {
        // Using fully encapsulated class
        Student student = new Student("John Doe", 20, "Computer Science", "CS123");
        student.displayInfo();

        // Testing validation in setters
        student.setAge(-5);  // Invalid age
        student.setGpa(5.0); // Invalid GPA
        student.setName(""); // Invalid name

        // Updating GPA with business logic
        student.updateGpa(3.5, 3);
        student.displayInfo();

        // Using read-only class
        ReadOnlyPerson person = new ReadOnlyPerson("Alice", 25);
        System.out.println("Name: " + person.getName());
        System.out.println("Age: " + person.getAge());

        // Using write-only class
        WriteOnlyLogger logger = new WriteOnlyLogger();
        logger.setLogFile("app.log");
        logger.log("Application started");
    }
}

// Additional example: Immutable class
final class ImmutablePoint {
    private final double x;
    private final double y;

    public ImmutablePoint(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double getX() {
        return x;
    }

    public double getY() {
        return y;
    }

    // Returns new instance instead of modifying existing one
    public ImmutablePoint translate(double dx, double dy) {
        return new ImmutablePoint(x + dx, y + dy);
    }

    @Override
    public String toString() {
        return "Point(" + x + ", " + y + ")";
    }
}

// Usage of immutable class
class Main {
    public static void main(String[] args) {
        ImmutablePoint point = new ImmutablePoint(1.0, 2.0);
        System.out.println("Original point: " + point);

        // Creating new point instead of modifying existing one
        ImmutablePoint translated = point.translate(3.0, 4.0);
        System.out.println("Translated point: " + translated);
        System.out.println("Original point remains unchanged: " + point);
    }
}

### Miscellaneous

- *The Object class is the parent class of all the classes in java by default.*
- *The Cloneable interface must be implemented by the class if we want to create a clone of an object.*
- *Wrapper class is used to convert primitive into object and object into primitive.*
- *Autoboxing and unboxing feature converts primitive into object and object into primitive automatically.*
- *There is only call by value in java, not call by reference.*
- *A method in java that calls itself is called recursive method.*
- *The Object class provides several important methods like equals(), hashCode(), toString(), etc.*
- *Wrapper classes provide utility methods for primitive types.*
- *Recursive methods must have a base case to terminate the recursion.*

```java
// Object class methods example
class ObjectMethodsExample {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = new String("Hello");

        // equals() method
        System.out.println(str1.equals(str2));  // true
        System.out.println(str1.equals(str3));  // true

        // hashCode() method
        System.out.println(str1.hashCode());
        System.out.println(str2.hashCode());

        // toString() method
        System.out.println(str1.toString());

        // getClass() method
        System.out.println(str1.getClass().getName());

        // clone() method
        Person p1 = new Person("John", 25);
        try {
            Person p2 = (Person) p1.clone();
            System.out.println("Cloned person: " + p2);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}

// Cloneable interface example
class Person implements Cloneable {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

// Wrapper classes and autoboxing
class WrapperExample {
    public static void main(String[] args) {
        // Autoboxing
        Integer i = 10;  // int to Integer
        Double d = 3.14; // double to Double
        Boolean b = true; // boolean to Boolean

        // Unboxing
        int j = i;       // Integer to int
        double e = d;    // Double to double
        boolean f = b;   // Boolean to boolean

        // Wrapper class methods
        int num = Integer.parseInt("123");
        double dbl = Double.parseDouble("123.45");
        String s1 = Integer.toString(123);
        String s2 = Double.toString(123.45);

        // Value comparison
        Integer i1 = 100;
        Integer i2 = 100;
        System.out.println(i1 == i2);  // true (cached values)

        Integer i3 = 200;
        Integer i4 = 200;
        System.out.println(i3 == i4);  // false (not cached)
    }
}

// Recursive examples
class RecursionExamples {
    // Fibonacci sequence
    int fibonacci(int n) {
        if (n <= 1) return n;
        return fibonacci(n-1) + fibonacci(n-2);
    }

    // Binary search
    int binarySearch(int[] arr, int left, int right, int x) {
        if (right >= left) {
            int mid = left + (right - left) / 2;

            if (arr[mid] == x) return mid;
            if (arr[mid] > x) return binarySearch(arr, left, mid - 1, x);
            return binarySearch(arr, mid + 1, right, x);
        }
        return -1;
    }

    // Factorial
    int factorial(int n) {
        if (n == 0) return 1;
        return n * factorial(n-1);
    }

    // Tower of Hanoi
    void towerOfHanoi(int n, char from, char to, char aux) {
        if (n == 1) {
            System.out.println("Move disk 1 from " + from + " to " + to);
            return;
        }
        towerOfHanoi(n-1, from, aux, to);
        System.out.println("Move disk " + n + " from " + from + " to " + to);
        towerOfHanoi(n-1, aux, to, from);
    }
}

// Call by value example
class CallByValue {
    void modifyPrimitive(int x) {
        x = x * 2;
        System.out.println("Inside method: " + x);
    }

    void modifyObject(StringBuilder sb) {
        sb.append(" World");
        System.out.println("Inside method: " + sb);
    }

    public static void main(String[] args) {
        CallByValue obj = new CallByValue();

        // Primitive type (call by value)
        int num = 10;
        obj.modifyPrimitive(num);
        System.out.println("Outside method: " + num);  // Still 10

        // Object reference (call by value of reference)
        StringBuilder sb = new StringBuilder("Hello");
        obj.modifyObject(sb);
        System.out.println("Outside method: " + sb);  // "Hello World"
    }
}

// Additional example: Object class methods
class Employee {
    private String name;
    private int id;
    private double salary;

    public Employee(String name, int id, double salary) {
        this.name = name;
        this.id = id;
        this.salary = salary;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Employee employee = (Employee) obj;
        return id == employee.id &&
               Double.compare(employee.salary, salary) == 0 &&
               name.equals(employee.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, id, salary);
    }

    @Override
    public String toString() {
        return "Employee{" +
               "name='" + name + '\'' +
               ", id=" + id +
               ", salary=" + salary +
               '}';
    }
}

// Usage of Employee class
class Main {
    public static void main(String[] args) {
        Employee emp1 = new Employee("John", 101, 50000.0);
        Employee emp2 = new Employee("John", 101, 50000.0);
        Employee emp3 = new Employee("Jane", 102, 60000.0);

        System.out.println(emp1.equals(emp2));  // true
        System.out.println(emp1.equals(emp3));  // false
        System.out.println(emp1.hashCode());
        System.out.println(emp1.toString());
    }
}
```



