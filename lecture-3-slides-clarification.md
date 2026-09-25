### Name lookup rules
- ***Overriding*** method lookup is dynamic: 
    - It uses the actual object's type, i.e., the object before the dot, not the runtime type of an argument.
    - For ***overridable*** instance methods, if the method exists in the reference's declared type, the JVM looks for an overridden version.
        - ***Step 1:*** At compile time, Java selects a method signature using the declared types of the receiver (the object before the dot) and arguments.
        - ***Step 2:*** At runtime, it selects the most specific override for the receiver's actual type.
            - The receiver's actual type determines which override of that selected signature runs. 
            - The arguments' runtime types do ***NOT*** change the overload.
        - To understand why Step 1 is needed: 
            - Compile time selects a method signature; runtime dispatch chooses an overriding implementation of that method without reconsidering the overloads.
            - See  [[My CSC207H Mistakes#Common issues#Example A]] . 
    - If the receiver's actual class does not override the method selected at compile time, the nearest inherited implementation runs.
- Field lookup is static: it uses the reference's declared type.
> A field is a variable declared in a class that stores data about an object or the class itself.
- Overloading chooses the method signature statically (at compile time).
- Overriding chooses the implementation dynamically (at runtime).
#### Example A
```java
class A {
    void show(Object x) { System.out.println("Object"); }
    void show(String x) { System.out.println("String"); }
}

Object x = "hello";
new A().show(x);
```

Output:

```text
Object
```

Although the actual object in `x` is a `String`, its declared type is `Object`, so the compiler selects `show(Object)`. Runtime does not reconsider the `show(String)` overload.
