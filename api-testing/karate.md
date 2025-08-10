# Karate — BDD-style API Testing

PURPOSE: Combine readable scenarios with powerful HTTP and assertion features.

## Simple Feature
```cucumber
Feature: User API Tests

Scenario: Get User Details
  Given url 'https://reqres.in/api/users/2'
  When method get
  Then status 200
  And match $.data.first_name == 'Ahmed'
```

## Tips
- Use `Examples` or `Scenario Outline` for data-driven scenarios
- Karate can read CSV/JSON for data-driven tests
