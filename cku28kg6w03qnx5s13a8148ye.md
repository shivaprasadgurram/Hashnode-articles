## How to add location header to Spring MVC's POST Response?

# Problem Statement
Let's assume you are working on a User Management backend application in Spring boot. There is a requirement from client saying you have to return the location of newly created user. How you will achieve it? Let's discuss in this article.

For demo purpose I'm storing every user in a static List instead of connecting with database.

We can use **ServletUriComponentsBuilder** class to create links based on the current HttpServletRequest.

## **Code**

User.java


```
public class User {
	
	private Integer id;
	private String name;
	private Date birthDate;
	
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public Date getBirthDate() {
		return birthDate;
	}
	public void setBirthDate(Date birthDate) {
		this.birthDate = birthDate;
	}
	
	@Override
	public String toString() {
		return "User [id=" + id + ", name=" + name + ", birthDate=" + birthDate + "]";
	}
	
	public User(Integer id, String name, Date birthDate) {
		super();
		this.id = id;
		this.name = name;
		this.birthDate = birthDate;
	}

}

``` 

UserDaoService.java

```
@Component
public class UserDaoService {
	
	private static List<User> users = new ArrayList<>();
	
	private static int usersCount = 3;
	
	static
	{
		users.add(new User(1,"Shiva",new Date()));
		users.add(new User(2,"Prasad",new Date()));
		users.add(new User(3,"Gurram",new Date()));
	}
	
	
    // To return all the users
	public List<User> findAll()
	{
		return users;
	}
	
   // To create a new user and return it
	public User save(User user)
	{
		if(user.getId() == null)
		{
			user.setId(++usersCount);
		}
		users.add(user);
		return user;
	}
	
    //To find a user in List
	public User findOne(int id)
	{
		for(User user:users)
		{
			if(user.getId() == id )
				return user;
		}
		return null;
	}
	
}
``` 

UserController.java

```
@RestController
public class UserController {
	
	@Autowired
	private UserDaoService service;

	@PostMapping("/users")
	public ResponseEntity<Object> createUser(@RequestBody User user)
	{
		User savedUser = service.save(user);
		
		URI location = ServletUriComponentsBuilder
				.fromCurrentRequest()
				.path("/{id}")
				.buildAndExpand(savedUser.getId()).toUri();
		
		return ResponseEntity.created(location).build();
	}
}

``` 

## **Testing**

Go to any API Client like Postman. send below payload to "http://localhost:8080/users".

Note: Your application should run on port 8080, otherwise replace port in above URL with your current application running port.

payload:

```
{
    "name": "Smith",
    "birthDate": "2021-09-27T05:08:52.032+00:00"
}
``` 

In return you can observe **status should be 201 Created** and inside **Headers** you can observe a key called "**Location**" and value will be "http://localhost:8080/users/4".

This is how you can send location back to client in Headers as a part of POST response.

Thanks for reading :)

You can follow me at  [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/)

Ref: in28Minutes Udemy course. 



