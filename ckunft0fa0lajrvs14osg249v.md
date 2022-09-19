## Difference between PathVariable and RequestParam In Spring Boot

# Introduction

@PathVariable and @RequestParam are annotations in Spring MVC, these are used to capture the dynamic data which client send to our RESTful web service via a request URI.

@PathVariable captures values from URI path itself like below

```
http://localhost:8080/sayHi/Shiva
``` 

here **Shiva** is a path variable and which we are going to capture in below method.

```
@GetMapping(path = "/sayHi/{name}")
	public String pathVariableDemo(@PathVariable String name)
	{
		return "Hi "+name;
	}
``` 

**output**

```
Hi Shiva
``` 

@RequestParam captures values from query string like below

```
http://localhost:8080/sayHello?name=prasad
``` 

here **name** is a query param and which we are going to capture in below method


```
@GetMapping(path = "/sayHello")
	public String requestParamDemo(@RequestParam String name)
	{
		return "Hello "+name;
	}
``` 

**output**

```
Hello prasad
``` 

Note: You can use like @PathVariable("YYY") and @RequestParam("YYY"), if your URI element names and method parameter names are different. Here YYY is your URI element name.

Example:

```
http://localhost:8080/sayHello?name=prasad
``` 

I want to use name like "userName" in my code,


```
@GetMapping(path = "/sayHello")
	public String queryParam(@RequestParam("name") String userName)
	{
		return "Hello "+userName;
	}
``` 

## Encoding

Because @PathVariable is extracting values from the URI path, it’s not encoded. On the other hand, @RequestParam is encoded.

Using the previous example, ab+c will return as-is:

```
http://localhost:8080/sayHi/ab+c
----
name: ab+c
``` 

But for a @RequestParam request, the parameter is URL decoded:

```
http://localhost:8080/sayHello?name=ab+c
----
name: ab c
``` 

We can use **required** attribute for both annotations to make optional.


```
public String pathVariableDemo(@PathVariable(required=false) String name)
``` 

```
public String requestParamDemo(@RequestParam(required=false) String name)
``` 

 
Thanks for reading :)

You can follow me at  [LinkedIn](Link) 
