# Spring IoC and Dependency Injection Demo

A comprehensive demonstration of Spring Framework's core concepts: **Inversion of Control (IoC)** and **Dependency Injection (DI)** using XML-based configuration and Bean Factory.

## 📋 Table of Contents

- [Overview](#overview)
- [Key Concepts Explained](#key-concepts-explained)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [XML Configuration Breakdown](#xml-configuration-breakdown)
- [Java Implementation Steps](#java-implementation-steps)
- [Running the Application](#running-the-application)
- [Learning Outcomes](#learning-outcomes)

## Overview

This project demonstrates how Spring Framework manages object creation and dependency management through its IoC container. Instead of manually creating objects with `new` keyword, Spring's Bean Factory takes control of object instantiation and wiring.

## Key Concepts Explained

### 🔄 Inversion of Control (IoC)

**What is IoC?**
- Traditional approach: Your code creates and manages objects
- IoC approach: Framework (Spring) creates and manages objects for you
- **Control is inverted** - you give up control to the framework

**In this demo:** The `DefaultListableBeanFactory` creates all objects (Customer, Address, FullName, etc.) instead of using `new Customer()`.

### 💉 Dependency Injection (DI)

**What is DI?**
- A design pattern where objects receive their dependencies from external sources
- Objects don't create their own dependencies
- Spring "injects" dependencies into objects

**Types demonstrated:**
1. **Setter Injection** - Using `<property>` tags (e.g., Customer's email, contactNo)
2. **Constructor Injection** - Using `<constructor-arg>` tags (e.g., Address object)

### 🏭 Bean Factory

The core container that:
- Reads bean definitions from XML
- Creates and manages bean instances
- Resolves dependencies between beans
- Controls bean lifecycle

## Getting Started

### Prerequisites
- Java 8 or higher
- IntelliJ IDEA (Community or Ultimate Edition)
- Git installed on your machine
- Maven (usually bundled with IntelliJ)

### Clone and Setup

#### Step 1: Clone the Repository

```bash
# Clone the repository
git clone https://github.com/Kunal70616c/spring-legacy-ioc.git
# Navigate to project directory
cd spring-legacy-ioc.git
```

Replace `<repository-url>` with the actual URL of this repository.

#### Step 2: Import in IntelliJ IDEA

**Method 1: From Welcome Screen**
1. Open IntelliJ IDEA
2. Click on **"Open"** from the welcome screen
3. Navigate to the cloned repository folder
4. Select the project root folder (containing `pom.xml`)
5. Click **"OK"**
6. IntelliJ will detect it as a Maven project and auto-import dependencies

**Method 2: From File Menu**
1. Open IntelliJ IDEA
2. Go to **File → Open**
3. Navigate to the cloned repository folder
4. Select the folder and click **"OK"**
5. Wait for Maven to download dependencies (check bottom right for progress)

#### Step 3: Configure Project SDK

1. Go to **File → Project Structure** (or press `Ctrl+Alt+Shift+S` / `Cmd+;` on Mac)
2. Under **Project Settings → Project**
3. Set **Project SDK** to Java 8 or higher
4. Set **Project language level** to 8 or higher
5. Click **"Apply"** and **"OK"**

#### Step 4: Maven Sync

1. Look for the **Maven** tab on the right sidebar
2. Click the **Reload** icon (circular arrows) to sync Maven dependencies
3. Wait for all dependencies to download

#### Step 5: Verify XML Configuration File

1. Ensure `banking-app.xml` is in `src/main/resources/` folder
2. If not, create the resources folder and add the XML file there

### Running the Application

#### Option 1: Run from IntelliJ

1. Open `CustomerApp.java` in the editor
2. Right-click anywhere in the file
3. Select **"Run 'CustomerApp.main()'"**
4. View output in the **Run** console at the bottom

#### Option 2: Run using Maven

1. Open the **Terminal** in IntelliJ (bottom toolbar)
2. Execute the following commands:

```bash
# Clean and compile
mvn clean compile

# Run the application
mvn exec:java -Dexec.mainClass="sh.surge.kunal.banking.utils.CustomerApp"
```

#### Option 3: Using Run Configuration

1. Go to **Run → Edit Configurations**
2. Click **+** (Add New Configuration)
3. Select **Application**
4. Set **Name**: `CustomerApp`
5. Set **Main class**: `sh.surge.kunal.banking.utils.CustomerApp`
6. Set **Module**: Select your project module
7. Click **"Apply"** and **"OK"**
8. Click the **Run** button (green play icon) in the toolbar

### Expected Output

When you run the application, you should see output similar to:

```
INFO: FullName=FullName[firstName=Parameswari, lastName=Ettiappan]
INFO: Address1=Address[doorNo=8A, street=Gandhi Street, city=Chennai, pincode=600001]
INFO: Address2=Address[doorNo=16A, street=Nehru Street, city=Bangalore, pincode=800001]
INFO: Customer=Customer[accountNo=6855858, email=param@gmail.com, contactNo=9962376324, ...]
INFO: Customer2=Customer[accountNo=6855858, email=param@gmail.com, contactNo=9962376324, ...]
INFO: After modification Customer1=Customer[accountNo=9876543210, ...]
INFO: After modification Customer2=Customer[accountNo=9876543210, ...]
INFO: Individual=Individual[gender=FEMALE, dob=...]
INFO: Corporate=Corporate[companyType=Public, ...]
```

### Troubleshooting

**Issue: Dependencies not downloading**
- Solution: Check internet connection, try **File → Invalidate Caches → Invalidate and Restart**

**Issue: Cannot find main class**
- Solution: Ensure package structure matches: `sh.surge.kunal.banking.utils`
- Rebuild project: **Build → Rebuild Project**

**Issue: XML file not found**
- Solution: Verify `banking-app.xml` is in `src/main/resources/`
- Mark `resources` folder as **Resources Root** (right-click → Mark Directory as → Resources Root)

**Issue: Java version mismatch**
- Solution: Update `pom.xml` compiler settings:
```xml
<properties>
    <maven.compiler.source>8</maven.compiler.source>
    <maven.compiler.target>8</maven.compiler.target>
</properties>
```

## Project Structure

```
src/
├── main/
│   ├── java/
│   │   └── sh/surge/kunal/banking/
│   │       ├── models/
│   │       │   ├── Customer.java
│   │       │   ├── Individual.java
│   │       │   ├── Corporate.java
│   │       │   ├── FullName.java
│   │       │   ├── Address.java
│   │       │   ├── Gender.java (Enum)
│   │       │   └── CompanyType.java (Enum)
│   │       └── utils/
│   │           └── CustomerApp.java
│   └── resources/
│       └── banking-app.xml
```

## XML Configuration Breakdown

### 1. Basic Bean Definition

```xml
<bean id="customer" class="sh.surge.kunal.banking.models.Customer" autowire="byType">
```

- **`id`**: Unique identifier for the bean (like a variable name)
- **`class`**: Fully qualified class name to instantiate
- **`autowire="byType"`**: Spring automatically wires dependencies by matching types

### 2. Setter-based Dependency Injection

```xml
<property name="accountNo" value="6855858"></property>
<property name="email" value="param@gmail.com"></property>
```

- **`<property>`**: Injects values through setter methods
- **`name`**: Field name in the class (Spring calls `setAccountNo()`, `setEmail()`)
- **`value`**: Primitive/String values injected directly

### 3. Constructor-based Dependency Injection

```xml
<bean id="address1" class="sh.surge.kunal.banking.models.Address">
    <constructor-arg index="0" value="8A"></constructor-arg>
    <constructor-arg index="1" value="Gandhi Street"></constructor-arg>
    <constructor-arg index="2" value="Chennai"></constructor-arg>
    <constructor-arg index="3" value="600001"></constructor-arg>
</bean>
```

- **`<constructor-arg>`**: Passes values to constructor
- **`index`**: Position of argument in constructor (0-based)
- **`value`**: Actual value to pass

### 4. Bean Inheritance

```xml
<bean id="individual" class="sh.surge.kunal.banking.models.Individual" parent="customer">
```

- **`parent`**: Inherits properties from parent bean
- Individual bean inherits accountNo, email, contactNo from customer bean

### 5. Enum Injection with Factory Method

```xml
<bean id="gender" class="sh.surge.kunal.banking.models.Gender" factory-method="valueOf">
    <constructor-arg value="FEMALE"></constructor-arg>
</bean>
```

- **`factory-method`**: Calls static factory method instead of constructor
- For enums, `valueOf()` converts String to enum constant

### 6. Autowiring by Type

```xml
<bean id="customer" class="..." autowire="byType">
```

When enabled, Spring automatically:
- Finds beans with matching types (FullName, Address)
- Injects them without explicit `<property ref="...">` tags

## Java Implementation Steps

### Step-by-Step IoC Container Setup

```java
// Step 1: Locate the XML configuration file
Resource resource = new ClassPathResource("banking-app.xml");
```
**Purpose:** Points to the XML file in the classpath (resources folder)

```java
// Step 2: Create the Bean Factory (IoC Container)
DefaultListableBeanFactory defaultListableBeanFactory = 
    new DefaultListableBeanFactory();
```
**Purpose:** Creates the container that will manage all beans

```java
// Step 3: Create XML Bean Definition Reader
XmlBeanDefinitionReader xmlBeanDefinitionReader = 
    new XmlBeanDefinitionReader(defaultListableBeanFactory);
```
**Purpose:** Parses XML and understands bean definitions

```java
// Step 4: Load Bean Definitions from XML
xmlBeanDefinitionReader.loadBeanDefinitions(resource);
```
**Purpose:** Reads XML, registers all bean definitions with factory

```java
// Step 5: Retrieve Beans (Actual IoC in action!)
FullName fullName = (FullName) defaultListableBeanFactory.getBean("fullName");
Customer customer = (Customer) defaultListableBeanFactory.getBean("customer");
```
**Purpose:** 
- Factory creates objects on-demand
- Dependencies are automatically injected
- You receive fully configured objects

### Key Observations in Code

#### Singleton Behavior
```java
Customer customer1 = (Customer) defaultListableBeanFactory.getBean("customer");
Customer customer2 = (Customer) defaultListableBeanFactory.getBean("customer");

customer2.setAccountNo(9876543210L);
// Both customer1 and customer2 point to SAME object!
```

**Default Scope:** Beans are singletons (one instance per container)

## Learning Outcomes

After studying this demo, you'll understand:

✅ **IoC Concept**: How Spring manages object creation lifecycle  
✅ **Dependency Injection**: Both setter and constructor injection  
✅ **XML Configuration**: Bean definitions, properties, and relationships  
✅ **Bean Factory**: Low-level IoC container operations  
✅ **Autowiring**: Automatic dependency resolution by type  
✅ **Bean Inheritance**: Reusing configurations across beans  
✅ **Factory Methods**: Working with enums and static factories  
✅ **Singleton Pattern**: Default bean scope behavior  

## Configuration Highlights

| Feature | XML Element | Example |
|---------|-------------|---------|
| Setter Injection | `<property>` | `<property name="email" value="...">` |
| Constructor Injection | `<constructor-arg>` | `<constructor-arg index="0" value="...">` |
| Bean Reference | `ref` attribute | `<property name="address" ref="address1">` |
| Autowiring | `autowire` attribute | `autowire="byType"` |
| Inheritance | `parent` attribute | `parent="customer"` |
| Enum/Factory | `factory-method` | `factory-method="valueOf"` |

## Why This Matters

**Traditional Approach:**
```java
Customer customer = new Customer();
customer.setEmail("param@gmail.com");
customer.setContactNo("9962376324");
FullName fullName = new FullName();
fullName.setFirstName("Parameswari");
customer.setFullName(fullName);
// Manual wiring of all dependencies
```

**Spring IoC Approach:**
```java
Customer customer = (Customer) beanFactory.getBean("customer");
// Fully configured object with all dependencies injected!
```

**Benefits:**
- Loose coupling between components
- Easy testing (mock dependencies)
- Centralized configuration
- Better maintainability

---

**Note:** This demo uses XML configuration for educational purposes. Modern Spring applications typically use Java-based configuration (`@Configuration`, `@Bean`) or annotation-based configuration (`@Component`, `@Autowired`).
