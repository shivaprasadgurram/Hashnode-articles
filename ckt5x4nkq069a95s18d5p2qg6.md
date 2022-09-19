## Spring boot RabbitMQ Food Ordering application

RabbitMQ is a open source messaging broker that implements Advanced Messaging Queuing Protocol(AMQP). AMQP standardizes messaging using Producers, Broker and Consumers.

To perform message queuing we need 3 key components

1. Producer -> Responsible to publish a  message.

2. Broker -> Holds the message and put into appropriate queue.

3. Consumer -> Responsible to consume a message.


**AMQP Characteristics**

**Security**:  Supports authentication, authorization, LDAP and TLS via RabbitMQ plugins.

**Reliability**: Confirms the message was successfully delivered to the broker and confirms that message was successfully processed by the consumer.

**Interoperability**: Message is transfer as stream of bytes over the network, so any clients can operate on it irrespective of any languages.

Producer can be developed using Java.
Consumer can be developed using Node.

**How it works?**

1) Producer will publish a message to an Exchange with a routingKey which is used to identify the Queue.

2) Exchange will hold the published message and routingKey and it will push message into the appropriate queue based on routingKey.

3) Consumer will consumes the message based on queue which is assigned to it.

Please refer the below diagram for better understanding.

![rabbitMQ-flow.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630763527284/9uexTyHCW.png)














Note: We have to bind the Exchange and Queue with a routingKey.

## Implementation

I created a spring boot project which consists both producer and consumer functionalities.

Application: **Food Ordering** (Producer publishes the order status and Consumer consumes it)

**Producer:** Publishes the Order status like Order(orderId, name, quantity and price), status and message to an exchange with a routingKey.

**Exchange**: Will put this Order status in to appropriate queue based on routingKey which we provided while publishing the message.

**Consumer**: Will consumes based on queue.

**Setting up RabbitMQ in windows**

1. Download and install ERlang  [http://erlang.org/download/otp_win64_22.3.exe](http://erlang.org/download/otp_win64_22.3.exe) 

2. Downlaod and install RabbitMQ  [https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.8.8/rabbitmq-server-3.8.8.exe](https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.8.8/rabbitmq-server-3.8.8.exe) 

3. Go to RabbitMQ Server install Directory C:\Program Files\RabbitMQ Server\rabbitmq_server-3.8.3\sbin

4. Run command rabbitmq-plugins enable rabbitmq_management

5. Open browser and enter  [http://localhost:15672/ ](http://localhost:15672/ )  to redirect to RabbitMQ Dashboard

6. Also we can Open it with IP Address  [http://127.0.0.1:15672](http://127.0.0.1:15672) 

7. Login page default username and password is guest

8. After successfully login you should see RabbitMQ Home page

Note: After successful login you have to create a Queue(from Queues tab), exchange(from Exchanges tab) and you have to **bind **queue and exchange with a Routing Key.


- Queue name: test-queue
- Exchange name: test-exchange
- Routing key: test

## Coding

1) Create a spring boot project with following dependencies

- Spring Web
- Spring for RabbitMQ

2) Create Order class which holds orderId, name, quantity and price like below.

**Order.java**
```
public class Order {
	
	private String orderId;
	private String name;
	private int quantity;
	private double price;
	
	public Order()
	{
		
	}
	public Order(String orderId, String name, int quantity, double price) {
		super();
		this.orderId = orderId;
		this.name = name;
		this.quantity = quantity;
		this.price = price;
	}
	public String getOrderId() {
		return orderId;
	}
	public void setOrderId(String orderId) {
		this.orderId = orderId;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getQuantity() {
		return quantity;
	}
	public void setQuantity(int quantity) {
		this.quantity = quantity;
	}
	public double getPrice() {
		return price;
	}
	public void setPrice(double price) {
		this.price = price;
	}
	@Override
	public String toString() {
		return "Order [orderId=" + orderId + ", name=" + name + ", quantity=" + quantity + ", price=" + price + "]";
	}
}
``` 

3) Create OrderStatus class which holds Order(above created), status and message.

**OrderStatus.java**

```
public class OrderStatus {
	
	private Order order;
	private String status;
	private String message;
	
	public OrderStatus()
	{
		
	}
	public OrderStatus(Order order, String status, String message) {
		super();
		this.order = order;
		this.status = status;
		this.message = message;
	}
	public Order getOrder() {
		return order;
	}
	public void setOrder(Order order) {
		this.order = order;
	}
	public String getStatus() {
		return status;
	}
	public void setStatus(String status) {
		this.status = status;
	}
	public String getMessage() {
		return message;
	}
	public void setMessage(String message) {
		this.message = message;
	}
	
	@Override
	public String toString() {
		return "OrderStatus [order=" + order + ", status=" + status + ", message=" + message + "]";
	}
}
``` 

4) Create a config file which configs Queue, Exchange and binds together with a routingKey.

**MessagingConfig.java**

```
@Configuration
public class MessagingConfig {
	
	public static final String QUEUE = "test-queue";
	public static final String EXCHANGE = "test-exchange";
	public static final String ROUTING_KEY = "test";
	
	@Bean
	public Queue queue()
	{
		return new Queue(QUEUE);
	}
	
	@Bean
	public TopicExchange exchange()
	{
		return new TopicExchange(EXCHANGE);
	}
	
	@Bean
	public Binding binding(Queue queue,TopicExchange exhange)
	{
		return BindingBuilder.bind(queue).to(exhange).with(ROUTING_KEY);
	}
	
	@Bean
	public MessageConverter converter()
	{
		return new Jackson2JsonMessageConverter();
	}
	
	@Bean
    public AmqpTemplate template(ConnectionFactory connectionFactory) {
        final RabbitTemplate rabbitTemplate = new RabbitTemplate(connectionFactory);
        rabbitTemplate.setMessageConverter(converter());
        return rabbitTemplate;
    }
}
``` 

5) Create OrderPublisher class to publish a message.

**OrderPublisher.java**

```
@RestController
@RequestMapping("/order")
public class OrderPublisher {
	
	@Autowired
	private RabbitTemplate rabbitTemplate;
	
	@PostMapping("/{restuarentName}")
	public String bookOrder(@RequestBody Order order,@PathVariable String restuarentName)
	{
		order.setOrderId(UUID.randomUUID().toString());
		OrderStatus orderStatus = new OrderStatus(order,"PROCESS","order placed successfully in "+restuarentName);
		rabbitTemplate.convertAndSend(MessagingConfig.EXCHANGE, MessagingConfig.ROUTING_KEY, orderStatus);
		return "success!!";
	}

}
``` 

6) Create OrderConsumer class to consume the message from a Queue.

**OrderConsumer.java**


```
@Component
public class OrderConsumer{
	
	@RabbitListener(queues = MessagingConfig.QUEUE)
	public void consumeMessageFromQueue(OrderStatus orderStatus)
	{
		System.out.println("Message Received from queue: " + orderStatus);
	}

}
``` 

# Testing

Open any REST client like postman and place an order like below.

- URL: http://localhost:9292/order/cakeWala
- Method: POST

Input (JSON):

```
{
  "name": "Chicken Pizza",
  "quantity": 2,
  "price": 180
}
``` 

Immediately in application console you can able to see like below(Which consumed from the queue)

```
Message Received from queue: OrderStatus [order=Order [orderId=2314f1e3-2f34-4156-83cc-a1e7c1b3c9ec, name=Chicken Pizza, quantity=2, price=180.0], status=PROCESS, message=order placed successfully in cakeWala]

``` 

You can check everything from RabbitMQ dashboard also.

This is a basic demonstration of how RabbitMQ works with a spring boot application, In future I will be coming with a complex use case where we will be using microservices.


Thanks for reading.

You can follow me at  [LinkedIn](https://www.linkedin.com/in/shivaprasadgurram/)

Reference:  [Youtube](https://www.youtube.com/watch?v=o4qCdBR4gUM)




