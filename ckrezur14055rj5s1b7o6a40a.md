## Different ways of iterating an ArrayList in Java

When working with ArrayList in Java, most of the time we encounter a situation where we need to iterate through an each element. In this article I'm going to demonstrate the different ways in which we can iterate through an ArrayList elements.

//Defining an ArrayList
```
ArrayList<Integer> arr = new ArrayList<Integer>();
arr.add(10);
arr.add(20);
arr.add(30);
arr.add(40);
arr.add(50);
``` 


### Using normal for loop
This method is useful when you also need index of the elements along with the elements itself. Using this method, you can also iterate a part of an ArrayList.
```
for(int i=0;i<arr.size();i++)
{
	System.out.print(arr.get(i)+" ");
}
``` 
Output: 10 20 30 40 50

### Using enhanced for loop
This method is useful when you don’t need indexes of elements and you just want to access the elements without removing them or modifying them.
```
for(int i : arr)
{
	  System.out.print(i+" ");
}
``` 
Output: 10 20 30 40 50

### Using Iterator
This method is useful when you want to remove the elements as you iterate through an ArrayList.
You can use : it.remove();

```
Iterator<Integer> it = arr.iterator();
while(it.hasNext())
{
	System.out.print(it.next()+" ");
}
``` 
Output: 10 20 30 40 50

### Using Lambda
This method is a syntactic sugar which reduces the lines of code. Lambda introduced in Java 8.
```
arr.forEach(elem -> System.out.print(elem+" "));
``` 
Output: 10 20 30 40 50

### Using Streams with Lambda
Streams also introduced in Java 8.
```
arr.stream().forEach((element) -> System.out.print(element+" "));
``` 
Output: 10 20 30 40 50

### Using ListIterator
This method is useful when you want to iterate in both directions forward and backward. You can use hasPrevious() and previous() also.

```
ListIterator<Integer> li= arr.listIterator();
while(li.hasNext())
{
	System.out.print(li.next()+" ");
}
``` 


For more stuff like this follow me at  [https://www.linkedin.com/in/shivaprasadgurram/](Link) 










