# TestNG Annotations — Lifecycle & Usage

PURPOSE: Describe TestNG lifecycle hooks and show practical examples for test setup and teardown.

| Annotation     | When It Runs                  | Use Case                                 |
|----------------|------------------------------|------------------------------------------|
| @BeforeSuite   | Once before all tests         | Initialize global resources (DB, configs)|
| @BeforeTest    | Before <test> tag in XML      | Setup specific test group configs        |
| @BeforeClass   | Before first method in class  | Setup browser or environment             |
| @BeforeMethod  | Before each test method       | Prepare test data, login, reset states   |
| @Test          | The actual test method        | Test logic here                          |
| @AfterMethod   | After each test method        | Cleanup, logout, reset                   |
| @AfterClass    | After all methods in class    | Close browser or environment             |
| @AfterSuite    | Once after all tests          | Final cleanups                           |

## Example
```java
@BeforeClass
public void setup() {
    // initialize driver, read config
}

@Test
public void testLogin() {
    // test code
}

@AfterClass
public void teardown() {
    // driver.quit()
}
```
