## Applying TDD with Spring Boot REST Services
### The basic of TDD is to write the test first, then we implement the feature so it can pass the test, the second step is reapeated until we have an implementation that passes the test. After that, we can consider that the feature is implemented correctly (if you write the test with a good coverage of the feature)
### Wrapping the REST service around tests will ensure that the service complies with the requirements and also will give more reliability to insert new changes. 

#### Spring boot provides some outstanding features to help with this task.
#### 1) First thing to do is to add the following dependency to you pom.xml (make sure you use test scope to avoid using unecessary dependencies on the final build).
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-test</artifactId>
	<scope>test</scope>
</dependency>
```

#### 2) Create the test class under /src/test/java (this will let maven run this test during the build process). Also, its a good practice to use the same name of the Rest class with the sufix 'Test'.

#### 3) Now, in your test class use the following annotations:
```
@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = Application.class)
@WebIntegrationTest
public class JournalServiceTest 
```
  - The first annotation (@RunWith) indicate to spring boot that this is a test class.
  - The second annotation (@SpringApplicationConfiguration) is to load the configuration that we have set up in the application (in my case I want to access the server port). Then you can access any property or custom configuration that you made for the application.
  You can also create a new application.properties for testing. Be aware that in this case if you make changes to the main application.properties you will need to update the test application.properties file. 
  - The third annotation (@WebIntegrationTest) will let spring run the REST service before it executes the tests. This is good as we want to execute the tests on the real server. Also, this annotation let you inject a repository or any bean using @Autowired.

#### 4) Now you can write the test, lets us say that we want to test a POST to the REST service. For the sake of this example I placed all code in the same method, however it will be good to place the test object, the insert operation, and other values in variables/methods so it can be reused thru the other tests.

```
  @Test
	public void testAddTransaction() {
	  //Spring utility class that helps with the requests to the server
	  RestTemplate template = new TestRestTemplate();
	  //First we define the request header, we will send a JSON content type 
	  HttpHeaders requestHeaders = new HttpHeaders();
	  requestHeaders.setContentType(MediaType.APPLICATION_JSON);
		// Lets create the request body entity
		FinancialTransaction testObj = new FinancialTransaction("000023989", "766", "10", "2015");
		//Wrap the header and the entity in a HttpEntity
		HttpEntity<String> httpEntity = new HttpEntity<String>(JSONConverter.getJSONAsString(testObj), requestHeaders);
    //Use the RESTTemplate to make post and get the response
		ResponseEntity<FinancialTransaction> returned = template.postForEntity(uri.toString(), httpEntity,
				FinancialTransaction.class, requestHeaders);
		//Make the assertions
		//Is a sucess response
		assertTrue(returned.getStatusCode().is2xxSuccessful());
		//It came with a body
		assertNotNull(returned.getBody());
		//It came with ID (this is what we expect from the server to insert this entity in the database and return the same entity with the new generated ID)
		assertThat(returned.getBody().getId(), IsNot.not(IsEmptyString.isEmptyOrNullString()));
	}
```
#### 5) As a last step it is good to include the test cycle in the maven build process. This will guarantee that the build will be a success if we pass all tests. For that, include the following plugin on the project's pom.xml file.
To execute the test verification run maven with the 'verify' goal: mvn verify
```
  	<plugin>
	<artifactId>maven-failsafe-plugin</artifactId>
		<executions>
			<execution>
				<goals>
					<goal>integration-test</goal>
					<goal>verify</goal>
				</goals>
			</execution>
		</executions>
	</plugin>
```
#### With this config you can run any test in a box, just do a regular Run as -> JUnit Test. Spring will start your service automatically before it start the tests. And the server will be shut down once the tests finish.

#### For a more detailed example: https://github.com/asdcamargo/fpts/tree/master/fpts-samples
