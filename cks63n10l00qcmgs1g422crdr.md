## How to read values from application.properties in Spring boot?

When we start working on a spring boot project we may encounter a situation where we have to read values from application.properties in order to perform our business operation. 

## Different ways

- Using @Value annotation

- Using @PropertySource and Environment interface

- Using @ConfigurationProperties annotation

In my application.properties ,I defined below properties

```
myproject.application.appName=Demo application
myproject.application.appVersion=1.1

``` 

### @Value annotation:
This annotation can be used for injecting values into fields in Spring-managed beans, and it can be applied at the field or constructor/method parameter level.


```
@Service
public class StudentService {

	@Value("${myproject.application.appName}")
	private String appName;
	
	@Value("${myproject.application.appVersion}")
	private String appVersion;
	
	public StudentResponse createStudent(Student s)
	{
		System.out.println("AppName: "+ appName);
		System.out.println("AppVersion: "+ appVersion);
		
		//code
		return null;
	}
}
``` 

If I call createStudent method, I can see below output in my console.

```
AppName: Demo application
AppVersion: 1.1
``` 

### Using @PropertySource and Environment interface
Spring @PropertySource annotation is used to provide properties file to Spring Environment. You can have multiple @PropertySource(s).Environment is an interface representing the environment in which the current application is running.


```
@RestController
@PropertySource("classpath:application.properties")
public class StudentController {

	@Autowired
	private Environment env;
	
	@PostMapping("/student")
	private StudentResponse createStudent(@RequestBody Student s)
	{
		System.out.println("AppName: "+ env.getProperty("myproject.application.appName"));
		System.out.println("AppVersion: "+ env.getProperty("myproject.application.appVersion"));
		
		//code
		return null;
	}
}
``` 
If I call createStudent method, I can see below output in my console.

```
AppName: Demo application
AppVersion: 1.1
``` 

### Using @ConfigurationProperties annotation
@ConfigurationProperties works best with hierarchical properties that all have the same prefix, Here in our example I can add a prefix of "myproject.application".

We have to create a POJO to map properties to fields. Spring will automatically bind any property defined in our property file that has the prefix myproject.application and the same name as one of the fields.

As of Spring boot 2.2 , below code works fine.

```
@ConfigurationProperties(prefix = "myproject.application")
public class PropertyReader {
	
	private String appName;
	private String appVersion;
	
	public String getAppName() {
		return appName;
	}
	public void setAppName(String appName) {
		this.appName = appName;
	}
	public String getAppVersion() {
		return appVersion;
	}
	public void setAppVersion(String appVersion) {
		this.appVersion = appVersion;
	}
}
``` 

Accessing values using PropertyReader get methods like below

```
@Service
public class StudentService {

	@Autowired
	private PropertyReader propertyReader;
	
	public StudentResponse createStudent(Student s)
	{
		System.out.println("AppName: " + propertyReader.getAppName());
		System.out.println("AppVersion: " + propertyReader.getAppVersion());
		
		//code
		return null;
	}
}
``` 

In Main class, use below annotation,
@ConfigurationPropertiesScan("package"), package is where your config(POJO) class exists.

If I call createStudent method, I can see below output in my console.

```
AppName: Demo application
AppVersion: 1.1
``` 

That's all about this article.

You can follow me  [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/) 

Thank you :)





 
