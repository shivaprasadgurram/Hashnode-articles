## Most Frequently asked Java Streams coding answers - Part 1 - Numbers

Hey Guys,

Welcome back to my blog.

In my last article I shared list of questions and in this article I'm going to share answers for **Input - 1 ** questions. In subsequent articles I will share answers for **Input - 2** questions.

Questions link :  [Most Frequently asked Java Streams coding questions - Part 1](https://shivaprasadgurram.hashnode.dev/most-frequently-asked-java-streams-coding-questions-part-1) 

## Input - 1
Assume you are given a list of numbers like {1,7,8,9,5,2,36,4,78,222,24,9}

```
List<Integer> list = Arrays.asList(1,7,8,9,5,2,36,4,78,222,24,9);
``` 

## Answers

 **1) Given a list of numbers, return the sum of all numbers**.

**Approach**: We can use **reduce()** method whenever we want to produce a single resultant value as output for example, maximum, minimum, sum, product, etc.

You can refer  [Stream.reduce](https://www.geeksforgeeks.org/stream-reduce-java-examples/) for more details. 


```
Optional<Integer> sum = list.stream().reduce((a, b) -> a+b);
System.out.println("sum is: "+sum.get());
``` 

output

```
sum is: 405
``` 

**2) Given a list of numbers, return the average of all numbers** 

**Approach**: We can use **mapToInt()** followed by **average()** whenever we want to perform an average on list of integers.


```
double avg = list.stream().mapToInt(a->a).average().orElse(0);
System.out.println("average is: "+avg);
``` 

output

```
average is: 33.75
``` 

**3) Given a list of numbers, square them and filter the numbers which are greater 100 and then find the average of them**

**Approach**: Here we need to do 3 things

- We need to square each number ( We can use **map()**)
- Filter whose value is greater than 100 (we can use **filter()**)
- Find average of those (we can use **mapToInt()** and **average()** together)

```
double avg1 = list.stream().map(a->a*a).filter(a -> a>100).mapToInt(a->a).average().orElse(0);
System.out.println("average is: "+avg1);
``` 

If we look at the numbers, only **36, 78, 222, 24** squares are greater than **100**.

-  **(1296 + 6084 + 49284 + 576)/4 = 14310.0**

output

```
average is: 14310.0
``` 

**4) Given a list of numbers, return the even and odd numbers separately**

**Approach**: We can use **filter()** and **Collectors.toList()** to get both even and odd numbers as two separate lists.

**Even Numbers:**

```
List<Integer> evens = list.stream().filter(num->num%2==0).collect(Collectors.toList());
System.out.println("evens: "+ evens);
``` 

output

```
evens: [8, 2, 36, 4, 78, 222, 24]
``` 

**Odd Numbers**


```
List<Integer> odds = list.stream().filter(num -> num%2!=0).collect(Collectors.toList());
System.out.println("odds: "+ odds);
``` 

output

```
odds: [1, 7, 9, 5, 9]
``` 

**5) Given a list of numbers, find out all the numbers starting with 2**

**Approach**: Here we need to do 4 things

- Convert Integer to String to perform startsWith operation on it
- Filter the strings that starts with **2**
- Convert String to Integer on filtered data
- Collect the final Integers as List and store 

```
List<Integer> startsWith2 = list.stream().map(num -> String.valueOf(num)).filter(n -> n.startsWith("2")).map(Integer::valueOf).collect(Collectors.toList());
System.out.println("startsWith2: "+startsWith2);

``` 

output

```
startsWith2: [2, 222, 24]
``` 

**6) Given a list of numbers, print the duplicate numbers**

**Approach 1**: Using **frequency()** method of **Collections** class. It counts the frequency of the specified element in the given list. If count > 1 then that element is duplicate one.

```
Set<Integer> duplicates = list.stream().filter(num -> Collections.frequency(list,num) > 1).collect(Collectors.toSet());
System.out.println("duplicates: "+duplicates);
``` 

output

```
duplicates: [9]
``` 

**Approach 2**: Using **Set **to collect only duplicates.

```
Set<Integer> duplicates1 = new HashSet<>();
Set<Integer> dup = list.stream().filter(num -> !duplicates1.add(num)).collect(Collectors.toSet());
System.out.println("duplicates: "+dup);
``` 

output

```
duplicates: [9]
``` 

**7) Given a list of numbers, print the maximum and minimum values**

**Approach**: Using **max()** and **min()** we can get maximum and minimum values from a list along with **Comparator.comparing()**.

**Maximum Value:** 

```
int max = list.stream().max(Comparator.comparing(Integer::valueOf)).get();
System.out.println("Maximum Value: "+max);
``` 

output

```
Maximum Value: 222
``` 

**Minimum Value:**

```
int min = list.stream().min(Comparator.comparing(Integer::valueOf)).get();
System.out.println("Minimum Value: "+min);
``` 

output

```
Minimum Value: 1
``` 

**8) Given a list of numbers, sort them in ASC and DESC order and print**

**Approach:** Using **sorted()**, We can sort a list in **ASC** or **DESC** order.

**ASC Order**

```
List<Integer> asc_order = list.stream().sorted().collect(Collectors.toList());
System.out.println("ASC Order: "+asc_order);
``` 

output

```
ASC Order: [1, 2, 4, 5, 7, 8, 9, 9, 24, 36, 78, 222]
``` 

**DESC Order**

```
List<Integer> desc_order = list.stream().sorted(Collections.reverseOrder()).collect(Collectors.toList());
System.out.println("DESC Order: "+desc_order);
``` 

output

```
DESC Order: [222, 78, 36, 24, 9, 9, 8, 7, 5, 4, 2, 1]
``` 

**9) Given a list of numbers, return the first 5 elements and their sum**

**Approach**: We can use **limit()** followed by **reduce().**

**First 5 Elements**

```
List<Integer> first5elements = list.stream().limit(5).collect(Collectors.toList());
System.out.println("first5elements: "+first5elements);
``` 

output

```
first5elements: [1, 7, 8, 9, 5]
``` 

**First 5 Elements Sum**

```
int first5sum = list.stream().limit(5).reduce((a,b) -> a+b).get();
System.out.println("first5elementsSum: "+first5sum);
``` 

output

```
first5elementsSum: 30
``` 

**10) Given a list of numbers, skip first 5 numbers and return the sum of remaining numbers**

**Approach:** We can use **skip()** to skip first n numbers in a list.


```
int sum1 = list.stream().skip(5).reduce((a,b) -> a+b).get();
System.out.println("Sum after first 5 elements skip: "+sum1);
``` 

output

```
Sum after first 5 elements skip: 375
``` 

**11) Given a list of numbers, return the cube of each number**

**Approach: ** We can use **map()** here.


```
List<Integer> cubes = list.stream().map(num -> num*num*num).collect(Collectors.toList());
System.out.println("Cubes: "+cubes);
``` 

output

```
Cubes: [1, 343, 512, 729, 125, 8, 46656, 64, 474552, 10941048, 13824, 729]
``` 


Note: Keep in mind about Integer overflow.


You can follow me at  [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/) 

Thanks for reading :)
Happy coding :)
















