# TestNG DataProvider — Data-Driven Testing

PURPOSE: Run a test multiple times with different inputs without duplicating code.

## Simple example
```java
@DataProvider(name = "loginData")
public Object[][] getData() {
    return new Object[][] {
        {"admin", "pass123"},
        {"user", "pass456"}
    };
}

@Test(dataProvider = "loginData")
public void loginTest(String username, String password) {
    // test steps
}
```

## Using external CSV/JSON for DataProvider
- Read CSV and parse into Object[][]
- Use Jackson or Gson to load JSON arrays into objects
- Keep test data under src/test/resources/data

## Tips
- Use descriptive test names with `@Test(dataProvider = "x", description = "case")`
- Use TestNG parameters along with DataProvider for environment-specific runs
