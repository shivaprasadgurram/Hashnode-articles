## What does mean by public static void main(String args[]) in Java?

Every program we write should have a entry point to start execution. main method is the entry point of a Java program for the Java Virtual Machine(JVM). Let's take below example to understand deeply.


```
class Hello
{
     public static void main(String args[])
     {
        System.out.println("Hello World");
     }
}
``` 

When we run above program **JVM ** will search for main method which is declared as **public**, **static ** and **void**.

### Why main must be declared public?
public is an Access specifier in Java, which specifies from where and who can access the method.

main() must be declared as public because as we know it is invoked by JVM whenever the program execution starts and JVM does not belong to our program package.

In order to access **main ** outside the package we have to declare it as **public**. If we declare it as anything other than public it shows a **Run time Error** but not **Compilation time error.**

### Why main must be declared static?
static is a keyword, main() must be declared as **static** because JVM does not know how to create an object of a class, so it needs a standard way to access the main method which is possible by declaring main() as static.

If a method is declared as static then we can call that method outside the class without creating an object using the syntax **ClassName.methodName();**

### Why main must be declared void?
void is a keyword and used to specify that a method doesn’t return anything. As main() method doesn’t return anything, its return type is void. As soon as the main() method terminates, the java program terminates too. Hence, it doesn’t make any sense to return from main() method as JVM can’t do anything with the return value of it.

### main() 
It is the name of Java main method. It is the identifier that the JVM looks for as the starting point of the java program. It’s not a keyword.

### Why main must have String Array Arguments?
main() must have String arguments as arrays because JVM calls main method by passing command line argument. As they are stored in string array object it is passed as an argument to main().

I hope you liked the article. Thanks for reading.

Follow me at  [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/) 