# RestAssured — Comprehensive Cheat Sheet (Interview + Revision)

Purpose
- Fast, focused reference for RestAssured usage in automation.
- Includes setup, common patterns, advanced features, and interview-style exercises.

Table of Contents
1. Setup (Maven / Gradle)
2. Basic GET / POST examples
3. Request / Response Specifications (reuse)
4. Authentication examples (Basic, Bearer, OAuth2)
5. Query params, path params, headers, form params, multipart
6. Assertions and JSONPath
7. Logging and Filters
8. Schema validation
9. Integration with TestNG
10. Common pitfalls and fixes
11. Interview questions and exercises

## 1) Setup

Maven dependency:
```xml
<dependency>
  <groupId>io.rest-assured</groupId>
  <artifactId>rest-assured</artifactId>
  <version>5.3.0</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>io.rest-assured</groupId>
  <artifactId>json-path</artifactId>
  <version>5.3.0</version>
</dependency>
```

Gradle:
```gradle
testImplementation 'io.rest-assured:rest-assured:5.3.0'
```

## 2) Basic Requests

GET example
```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

given()
    .baseUri("https://reqres.in")
.when()
    .get("/api/users/2")
.then()
    .statusCode(200)
    .body("data.first_name", equalTo("Janet"));
```

POST example
```java
String payload = "{"name":"morpheus","job":"leader"}";
given()
    .header("Content-Type", "application/json")
    .body(payload)
.when()
    .post("https://reqres.in/api/users")
.then()
    .statusCode(201)
    .body("name", equalTo("morpheus"))
    .log().body();
```

## 3) RequestSpecification / ResponseSpecification (reuse)

```java
RequestSpecification reqSpec = new RequestSpecBuilder()
    .setBaseUri("https://reqres.in")
    .addHeader("Accept", "application/json")
    .setContentType(ContentType.JSON)
    .build();

ResponseSpecification resSpec = new ResponseSpecBuilder()
    .expectStatusCode(200)
    .expectContentType(ContentType.JSON)
    .build();

given().spec(reqSpec)
.when().get("/api/users/2")
.then().spec(resSpec)
      .body("data.id", equalTo(2));
```

## 4) Authentication

Basic auth
```java
given().auth().preemptive().basic("username", "password")
       .when().get("/private")
       .then().statusCode(200);
```

Bearer token
```java
given().auth().oauth2("TOKEN_HERE")
       .when().get("/secure")
       .then().statusCode(200);
```

OAuth2 (client credentials)
```java
given().auth().oauth2(accessToken)
       .when().get("/resource")
       .then().statusCode(200);
```

## 5) Params, Headers, Multipart

Query params
```java
given().queryParam("page", 2)
       .when().get("/api/users")
       .then().statusCode(200);
```

Path params
```java
given().pathParam("id", 2)
       .when().get("/api/users/{id}")
       .then().statusCode(200);
```

Headers and form params
```java
given().header("X-Custom", "value")
       .formParam("username", "qa")
       .when().post("/form")
       .then().statusCode(200);
```

Multipart (file upload)
```java
given().multiPart("file", new File("path/to/file.png"))
       .when().post("/upload")
       .then().statusCode(200);
```

## 6) Assertions and JSONPath

- Use Hamcrest matchers for readable assertions: equalTo, hasSize, containsString, hasItem
- JSONPath examples:
  - `body("data[0].id", equalTo(1))`
  - `String email = response.path("data[0].email");`

Extracting values
```java
String token = given()
    .body(payload)
.when().post("/login")
.then().statusCode(200)
    .extract().path("token");
```

## 7) Logging and Filters

Log request / response
```java
given().log().all()
       .when().get("/api/users")
       .then().log().all();
```

Use filters for custom logging or reporting (e.g., Allure filter)
```java
RestAssured.filters(new RequestLoggingFilter(), new ResponseLoggingFilter());
```

## 8) Schema Validation

Add JSON schema validator dependency and validate responses
```java
then().assertThat().body(matchesJsonSchemaInClasspath("schemas/user-schema.json"));
```

## 9) Integration with TestNG / Parallel Execution

- Use DataProvider to feed test cases with endpoints and expected outputs.
- Use TestNG parallel="methods" or CI matrix to run API tests in parallel.
- Keep tests independent (no shared mutable state).

Example TestNG method
```java
@Test
public void getUserTest() {
    given().spec(reqSpec)
    .when().get("/api/users/2")
    .then().spec(resSpec);
}
```

## 10) Common Pitfalls and Fixes

- Not setting Content-Type or Accept headers — servers reject or return unexpected formats.
- Relying on fragile JSON paths — assert important fields and sizes.
- Not cleaning up test data — use test DB or delete created resources in teardown.
- Ignoring timeouts — set proper timeouts and assert response time if critical.

## 11) Interview Questions (short answers)

Q: How do you validate JSON schema?  
A: Use JSON schema validator with matchesJsonSchemaInClasspath or external libs.

Q: How to extract a value and reuse it in subsequent requests?  
A: Use `extract().path("token")` or `jsonPath().getString("token")` and pass into next request header.

Q: How to handle authentication in API tests?  
A: Use RestAssured auth() methods for basic, OAuth2, or set Authorization header for bearer tokens.

Q: How to test performance with RestAssured?  
A: RestAssured is not a load testing tool. For response time assertions use `time(lessThan(2000L))`. For real load tests, use JMeter or Gatling.

## 12) Exercises (for interview / revision)

1. Write a test to create a user, validate status 201, extract id and verify the user via GET.  
2. Validate response schema for a list endpoint and assert the list size > 0.  
3. Implement a RequestSpecification with retry logic (filter) that retries on 5xx errors.
4. Mock an external dependency by stubbing the endpoint and verify behavior locally.

--- 
Keep this page handy for quick revision before interviews. Add your own company-specific examples below.
