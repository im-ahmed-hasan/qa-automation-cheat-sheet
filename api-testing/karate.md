# Karate — Practical Cheat Sheet (Interview + Revision)

Purpose
- Focused guide to writing BDD-style API tests with Karate.
- Includes setup, patterns, data-driven tests, mocks, and interview questions.

Table of Contents
1. Setup (Maven plugin)
2. Basic feature syntax
3. Configuration and karate-config.js
4. Data-driven tests (Scenario Outline, Examples)
5. Calling Java code and JS functions
6. Mocking (API stubs) and mocks in CI
7. Assertions, matchers, and JSON path
8. Parallel execution and reporting
9. Common pitfalls
10. Interview questions and exercises

## 1) Setup (Maven)
Add Karate plugin to your pom:
```xml
<plugin>
  <groupId>com.intuit.karate</groupId>
  <artifactId>karate-maven-plugin</artifactId>
  <version>1.3.0</version>
  <executions>
    <execution>
      <id>test</id>
      <goals>
        <goal>test</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

## 2) Basic Feature Syntax

Example feature file `get-user.feature`:
```cucumber
Feature: User API

  Scenario: Get user by id
    Given url 'https://reqres.in/api/users/2'
    When method get
    Then status 200
    And match $.data.first_name == 'Janet'
```

## 3) karate-config.js
- Central place for environment config, baseUrl, and variables.
Example:
```javascript
function() {
  var config = {};
  config.baseUrl = 'https://reqres.in';
  return config;
}
```

## 4) Data-driven tests

Scenario Outline and Examples
```cucumber
Scenario Outline: Check user exists
  Given url baseUrl + '/api/users/<id>'
  When method get
  Then status 200
  And match $.data.id == <id>

Examples:
  | id |
  | 1  |
  | 2  |
```

Or use `call` with data files:
```cucumber
* def users = read('users.json')
* for(var u in users) karate.log(u.id)
```

## 5) Java & JS interop

- You can call Java utility classes from Karate.
- You can write reusable JS functions in `karate-config.js` or separate JS files and call them.

Example calling JS function:
```cucumber
* def gen = function(x){ return x + '-id' }
* def id = gen('user')
```

## 6) Mock server (stubs)
Karate can run as a mock server to simulate external services.
- Create a `mock.feature` that listens and returns canned responses.
- Useful for CI to avoid external flakiness.

## 7) Assertions and Matchers

Common matchers
- `match response == { id: 1, name: 'John' }`
- `match response.data contains { email: '#regex .+@.+\..+' }`
- `match response.data[0].id == 1`
- `match response contains { data: '#[]' }` // list assertion

Schema validation: use JSON schema files and `match response == read('schema.json')` patterns.

## 8) Parallel execution & Reporting

- Karate plugin runs tests in parallel by default for faster feedback.
- Use `karate.output.dir` or plugin config to collect HTML reports.
- In CI, publish the generated HTML or convert to JUnit XML for GitHub Actions.

## 9) Common pitfalls

- Overusing `karate.log` in large runs — excessive logs slow performance.
- Relying on external services without mocks — flakiness.
- Mixing too much Java code into features — prefer readable feature files.

## 10) Interview Questions (short answers)

Q: What is Karate?  
A: Karate is a BDD-style test framework for API, UI, and performance testing that uses Gherkin syntax and includes HTTP client and assertion support.

Q: How do you do data-driven tests in Karate?  
A: Use Scenario Outline with Examples, or read data files (JSON/CSV) and iterate.

Q: How to mock an external service?  
A: Use Karate's mock server feature: create a feature that listens and returns canned responses during tests.

Q: How to call Java code from Karate?  
A: Place Java utility classes on the classpath and call them using `java` interop in feature files.

## Exercises (practice)

1. Create a Karate feature that POSTs a new user, asserts 201, then GETs the user and verifies fields.  
2. Create a mock for an external payment provider and write tests that consume the mock.  
3. Use a JSON schema to validate a complex response structure.

---
Keep this page as your interview pocket reference for Karate.
