```java
@Component
public class CallRestService implements CommandLineRunner{

	private static void CallRestService()
	{
		String GET_URL="http://localhost:8080/user/111";
		RestTemplate restTemplate= new RestTemplate();
		//public User(Long userid, String name, String phone, List<Contact> contacts)
		///List<Contact> contacts = new ArrayList<>();
		///Contact c1= new Contact(1789L, "181818", "Zullu", 116L);
		//contacts.add(c1);
		
		//User user1 = new User(116L,"Rohit","1111",contacts);
		//ResponseEntity<User> user2 = restTemplate.postForEntity(url,user , User.class)
		
		User user= restTemplate.getForObject(GET_URL, User.class);
		System.out.println(user.getName());
		
		
	
	}
  
  ```java
