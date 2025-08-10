# RestAssured — API Testing in Java

PURPOSE: Functional API testing with readable syntax and built-in assertion support.

## Basic GET
```java
given()
    .baseUri("https://reqres.in")
.when()
    .get("/api/users/2")
.then()
    .statusCode(200)
    .body("data.first_name", equalTo("Janet"));
```

## POST with JSON body
```java
String payload = "{"name":"morpheus","job":"leader"}";
given()
    .header("Content-Type", "application/json")
    .body(payload)
.when()
    .post("https://reqres.in/api/users")
.then()
    .statusCode(201)
    .log().body();
```

## Common patterns
- Use `RequestSpecification` and `ResponseSpecification` for reuse
- Authenticate with OAuth2 or tokens via `auth().oauth2(token)`
- Validate response schema with JSON schema validator
