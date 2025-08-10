# Faker — Dynamic Test Data

PURPOSE: Generate realistic, random test data to improve test coverage and reduce brittle assertions.

## Basic usage
```java
Faker faker = new Faker();
String name = faker.name().fullName();
String email = faker.internet().emailAddress();
```

## Use cases
- Creating unique users for registration tests
- Generating realistic addresses and phone numbers
- Combining with DataProvider for lots of randomized scenarios

## Tips
- Seed faker for reproducible test data if needed: `new Faker(new Random(42))`
- Keep large generated data out of test assertions when values can vary
