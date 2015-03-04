# Java

## Class

### Layout

Methods and fields should be organized as below:

```java
class MySuperbClass {
	// Fields
	
	// Constructors
	
	// Private & protected methods
	
	// Public methods
}
```

### Indentation

Standard indentation should be **4 spaces (no tabs)**. When a carriage return is needed, keep same indentation.

```java
class AnotherAmazingClass {
    public void aMethod() {
        anotherMethod(
            firstArg,
            secondArg,
            thirdArg,
            // ...
        );
        
        stillAnotherMethod();
    }
}
```

### Names

Class and method names should be the most limpid as possible. Do not worry about having a long class name. Auto-completion and refactor tools are there for helping you.

Prefer `sortUsersByNameAsc` to `getUsers`.

### Case

In Java world, methods and vars should use **camel case**: `myFantasticMethod` . Class should be **pascal cased**: `FriendlyClass`.

Besides, it is a good practice to prefix private and protected methods and fields **by an underscore**. In no time at all, you can easily spot the access of your field/method.

```java
public class User {
    private String _name;
    
    private String _engineString(String value) {
        // ...
    }
    
    public String getName() {
        // ...
    }
}
```

## Interface

### Name

Interface name should start with a capital `I` to make distinction easier with classes.

## Performances

### For loops

Use **foreach** loop as much as possible, for it is optimized. Otherwise, when using a classic **for** loop, save size of browsable element before running:

```java
// DO

int size = list.size();
for (int i = 0; i < size; i++) {
    // ...
}

// OR
for (int i = 0, size = list.size(); i < size; i++) {
}

// DO NOT

for (int i = 0; i < list.size(); i++) {
    // ...
}
```

Do not assume size access is constant.

### Variable declarations

Variables should be declared at the top of each block. This process may increase performances for it avoids calling memory allocator and garbage collector again. However, it is a good practice for it keeps your code ordered. 

```java
public void myMethod() {
    int a;
    
    // ...
    
    if (myBool) {
        int b;
        // Do not declare b in upper block if current scope is enough        
        
        // ...
    }
}
```

## Unit testing

### AAA pattern

Try to match **AAA pattern** as much as possible. It makes your unit tests easy to debug and maintain.

```java
public void testMethod() {
    // Arrange
    // Prepare here all vars you will need
    
    // Act
    // Run the method you want to test
    
    // Assert
    // Check what happened
}
```

### Run a single action by test

You should run a single action by test. Do not test multiple expectations in a single test method. It avoids your test code to be messy. 

Suppose you have a `getLength()` method that returns the length of a string. You should have tree different test methods:

1. For a random string, such as `foobar`
2. For an empty one
3. A null argument

Do not run these tree tests in a single method.

### Name

You test suite should be named `MyClassTest`.

About test method, name should include purpose (tested method) and context (aka situation, such as null input), if any.

Then, name depends on your test tool (especially its output format). You can use either `myMethodNullInputTest` or `myClassMyMethodNullInputTest`. Second one may be useful is our tool does not group test methods by class.

## Extra

### Variable initialization

Variable initialization should be done as soon var is declared except if value needs any computation.

```java
// DO NOT
int i;
Foo f = super.getContext().getDefault().getFoo(), g;

i = 0;

// DO
int i = 0;
Foo f, g;

f = super.getContext().getDefault().getFoo();
``` 

### Chained calls

Prefer breaking line when having chained calls. Also, indent them.

```java
myUser
    .setFirstName("Gabriel")
    .setLastName("Byrne")
    .setMovies(myMovieList);
```

### Break endless lines

Avoid long code lines. Longer a line is, more painful to read it is. You should limit your line to 90 chars.

```java
// DO NOT
MyEngine.run(firstArg, secondArg, thirdArg, fourthArg, /** ... */);

// DO
MyEngine.run(
    firstArg,
    secondArg,
    thirdArg,
    fourthArg,
    // ...
);

```
