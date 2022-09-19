## How to create our own custom ArrayList?

# Introduction

We know ArrayList stores list of objects along with duplicates. In this article we are going to create our own custom ArrayList to stop allowing duplicates.

## Steps

- Custom class should extends ArrayList class

- It should override **add(T t)** of ArrayList class

- We have to write our own logic to deny duplicates.

## Code

```
import java.util.ArrayList;

public class CustomArrayList extends ArrayList<Integer>{
	
	@Override
	public boolean add(Integer e) {
		
		if(this.contains(e))
		{
			return true;
		}
		else
		{
			return super.add(e);
		}
	}

	public static void main(String[] args) {
		
		CustomArrayList c = new CustomArrayList();
		c.add(1);
		c.add(4);
		c.add(1);
		c.add(8);
		c.add(4);
		c.add(5);
		c.add(8);
		
		System.out.println(c);

	}
}
``` 

### Output

```
[1, 4, 8, 5]
``` 


Thanks for reading :)

You can follow me at  [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/) 
