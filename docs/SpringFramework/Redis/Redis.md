## Redis (Remote Dictionary Server)
Redis is an open source, advanced key-value store and an apt solution for building highperformance, scalable web applications.

1. Redis holds its database entirely in the memory, using the disk only for persistence.
2. Redis has a relatively rich set of data types when compared to many key-value data stores.
3. Redis can replicate data to any number of slaves.

## Install redis
1. https://github.com/microsoftarchive/redis/releases/download/win-3.2.100/Redis-x64-3.2.100.zip
2. unzip it and run redis-server.exe
3. it will show that redis service is up and running on port number 6379

## Create Spring Boot project
1. Create project using https://start.spring.io/
2. Add Dependency Lombok,web,Spring Data Redis
3. Generate the package

## Create Project in Eclipse
1. Open the project in Eclipse
2. Add Dependency

```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>3.3.0</version>
</dependency>

```
3. Create a Product class in entity package

```java
package com.redis.entity;

import org.springframework.data.annotation.Id;
import org.springframework.data.redis.core.RedisHash;

import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@RedisHash("Product")
public class Product {

	@Id
	private int id;
	private String name;
	private int qty;
	private long price;
}

```
4.  Create Redis connection configuration in config package

```java
package com.redis.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisStandaloneConfiguration;
import org.springframework.data.redis.connection.jedis.JedisConnectionFactory;
import org.springframework.data.redis.repository.configuration.EnableRedisRepositories;

@Configuration
@EnableRedisRepositories
public class RedisConfig {

	public JedisConnectionFactory connectionFactory() {
		RedisStandaloneConfiguration configuration = new RedisStandaloneConfiguration();
		configuration.setHostName("localhost");
		configuration.setPort(6379);
		return new JedisConnectionFactory(configuration);
	}
}

```
