## How to sort a Map using streams in Java?

**Only Code Snippet**

In our day-to-day life we may encounter a situation where we want to sort our map based on either key or value. Lets see how we can achieve it using Java streams.

Below code can be used to sort a map based on it's key and value in both orders i.e, ascending and descending.

# Code

```
public class SortMapUsingStreams {

	public static void main(String[] args) {
		
		Map<Integer, String> languages = new HashMap<>();
		languages.put(1, "Java");
		languages.put(45, "JavaScript");
		languages.put(3, "Python");
		languages.put(40, "C");
		languages.put(5, "SQL");
		languages.put(8, "Go");

		System.out.println("Sorted map based on key in ASC order");
		languages.entrySet().stream().sorted(Map.Entry.comparingByKey()).forEach(System.out::println);
		
		System.out.println("\nSorted map based on value in ASC order");
		languages.entrySet().stream().sorted(Map.Entry.comparingByValue()).forEach(System.out::println);
		
		System.out.println("\nSorted map based on key in DSC order");
		languages.entrySet().stream().sorted(Map.Entry.<Integer,String>comparingByKey().reversed()).forEach(System.out::println);
		
		System.out.println("\nSorted map based on value in DSC order");
		languages.entrySet().stream().sorted(Map.Entry.<Integer,String>comparingByValue().reversed()).forEach(System.out::println);
		
	}

}
``` 

**Output**

```
Sorted map based on key in ASC order
1=Java
3=Python
5=SQL
8=Go
40=C
45=JavaScript

Sorted map based on value in ASC order
40=C
8=Go
1=Java
45=JavaScript
3=Python
5=SQL

Sorted map based on key in DSC order
45=JavaScript
40=C
8=Go
5=SQL
3=Python
1=Java

Sorted map based on value in DSC order
5=SQL
3=Python
45=JavaScript
1=Java
8=Go
40=C

``` 

Thanks for reading :)

You can follow me at  [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/)