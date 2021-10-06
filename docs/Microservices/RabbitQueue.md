RabbitMQ is a message broker: it accepts and forwards messages. You can think about it as a post office: when you put the mail that you want posting in a post box, you can be sure that the letter carrier will eventually deliver the mail to your recipient. In this analogy, RabbitMQ is a post box, a post office, and a letter carrier.

The major difference between RabbitMQ and the post office is that it doesn't deal with paper, instead it accepts, stores, and forwards binary blobs of data ‒ messages.

RabbitMQ, and messaging in general, uses some jargon.

Producing means nothing more than sending. A program that sends messages is a producer :

![image](https://user-images.githubusercontent.com/84008107/136219609-1c5acfa7-acc5-4059-8afa-7e0dcd7cc999.png)


A queue is the name for a post box which lives inside RabbitMQ. Although messages flow through RabbitMQ and your applications, they can only be stored inside a queue. A queue is only bound by the host's memory & disk limits, it's essentially a large message buffer. Many producers can send messages that go to one queue, and many consumers can try to receive data from one queue. This is how we represent a queue:

![image](https://user-images.githubusercontent.com/84008107/136219670-862e7719-7501-4e8e-91f5-07f375a2f352.png)

Consuming has a similar meaning to receiving. A consumer is a program that mostly waits to receive messages:

![image](https://user-images.githubusercontent.com/84008107/136219764-0926408a-0db6-40c7-a4d4-09b1941db036.png)



![image](https://user-images.githubusercontent.com/84008107/136219251-7c3e920d-f74d-4978-b5ec-63fb04ecec5b.png)

### Java Implementation with Microservices

### Config 
```java

package com.rabbitmq.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import org.springframework.amqp.core.*;
import org.springframework.amqp.rabbit.connection.ConnectionFactory;
import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.amqp.support.converter.Jackson2JsonMessageConverter;
import org.springframework.amqp.support.converter.MessageConverter;

@Configuration
public class MessageConfig {
public static final String QUEUE="rabbit_queue";
public static final String EXCHANGE="rabbit_exchange";
public static final String ROUTING_KEY="rabbit_routingkey";

@Bean
public Queue queue() {
	return new Queue(QUEUE);
}
@Bean
public TopicExchange exchange() {
	return new TopicExchange(EXCHANGE);
}
@Bean
public Binding binding(Queue queue,TopicExchange exchange) {
	return BindingBuilder.bind(queue).to(exchange).with(ROUTING_KEY);
}

@Bean
public MessageConverter converter() {
	
	return new Jackson2JsonMessageConverter();
}

@Bean
public AmqpTemplate template(ConnectionFactory connectionfactory)
{
	final RabbitTemplate rabbitTemplate= new RabbitTemplate(connectionfactory);
	rabbitTemplate.setMessageConverter(converter());
	return rabbitTemplate;
}
}

```

### Data Transfer Objects

```java
package com.rabbitmq.dto;

public class Order {
	private String OrderId;
	private String name;
	private int qty;
	private double price;
	public String getOrderId() {
		return OrderId;
	}
	public String getName() {
		return name;
	}
	public int getQty() {
		return qty;
	}
	public double getPrice() {
		return price;
	}
	public void setOrderId(String orderId) {
		OrderId = orderId;
	}
	public void setName(String name) {
		this.name = name;
	}
	public void setQty(int qty) {
		this.qty = qty;
	}
	public void setPrice(double price) {
		this.price = price;
	}
	@Override
	public String toString() {
		return "Order [OrderId=" + OrderId + ", name=" + name + ", qty=" + qty + ", price=" + price + "]";
	}
	public Order(String orderId, String name, int qty, double price) {
		super();
		OrderId = orderId;
		this.name = name;
		this.qty = qty;
		this.price = price;
	}
	public Order() {
		super();
		// TODO Auto-generated constructor stub
	}

}

```

```java
package com.rabbitmq.dto;

public class OrderStatus {
private Order order;
private String status;
private String message;
public Order getOrder() {
	return order;
}
public String getStatus() {
	return status;
}
public String getMessage() {
	return message;
}
public void setOrder(Order order) {
	this.order = order;
}
public OrderStatus(Order order, String status, String message) {
	super();
	this.order = order;
	this.status = status;
	this.message = message;
}
public OrderStatus() {
	super();
	// TODO Auto-generated constructor stub
}
@Override
public String toString() {
	return "OrderStatus [order=" + order + ", status=" + status + ", message=" + message + "]";
}
public void setStatus(String status) {
	this.status = status;
}
public void setMessage(String message) {
	this.message = message;
}
}

```

### Publisher

```java
package com.rabbitmq.publisher;

import java.util.UUID;

import org.springframework.amqp.rabbit.core.RabbitTemplate;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.rabbitmq.config.MessageConfig;
import com.rabbitmq.dto.Order;
import com.rabbitmq.dto.OrderStatus;

@RestController
@RequestMapping("/order")
public class OrderPublisher {

	@Autowired
	private RabbitTemplate template;
	
	@PostMapping("{restaurantname}")
	public String bookOrder(@RequestBody Order order, @PathVariable String restaurantname) {
		order.setOrderId(UUID.randomUUID().toString());
		//restaurantname service get called
		//payment service getting called
		OrderStatus orderstatus= new OrderStatus(order,"PROCESS","order place successfully" + restaurantname);
		template.convertAndSend(MessageConfig.EXCHANGE, MessageConfig.ROUTING_KEY,orderstatus);
		return "Success!!";
	}
	
}

```

### Run the application and Check the Rabbit Queue Status


### Consumer

```java
package com.rabbitmq.consume;
import com.rabbitmq.config.MessageConfig;
import com.rabbitmq.dto.OrderStatus;

import org.springframework.amqp.rabbit.annotation.RabbitListener;
import org.springframework.stereotype.Component;

@Component
public class User {

	@RabbitListener(queues = MessageConfig.QUEUE) 
	public void consumeMessageFromQueue(OrderStatus ordersatus)
	{
	System.out.println("Message recieved from queue: " + ordersatus);	
	}
}
```
### Run the application and Check the Rabbit Queue the message should be consumed.
