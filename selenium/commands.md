# Selenium WebDriver — Commands & Best Practices

PURPOSE: Quick reference for browser control and common WebDriver interactions,
with practical notes for when to use each API.

## Setup (example)
```java
// Purpose: Create browser instance with desired options
WebDriverManager.chromedriver().setup();
ChromeOptions options = new ChromeOptions();
options.addArguments("--start-maximized");
WebDriver driver = new ChromeDriver(options);
```

## Browser Control
```java
// Purpose: Basic navigation and session control
driver.get("https://example.com");               // open URL
driver.navigate().to("https://google.com");      // navigate
driver.navigate().back();                        // back
driver.navigate().forward();                     // forward
driver.navigate().refresh();                     // refresh

driver.close(); // Closes current window (useful in multi-window tests)
driver.quit();  // Quits the whole driver session and closes all windows
```

## Window & Frame Handling
```java
// Purpose: Work with multiple windows or frames
String main = driver.getWindowHandle();
Set<String> all = driver.getWindowHandles();
for (String handle : all) {
    if (!handle.equals(main)) {
        driver.switchTo().window(handle);
        // perform actions
    }
}
driver.switchTo().defaultContent(); // back to main frame
```

## Element Interactions
```java
WebElement el = driver.findElement(By.id("username"));
el.clear();
el.sendKeys("admin");
el.click();
```

## Keyboard & Mouse
```java
// Keyboard actions
el.sendKeys(Keys.ENTER);

// Advanced user interactions
Actions actions = new Actions(driver);
actions.moveToElement(el).click().perform();
```

## File Upload (input[type=file])
```java
WebElement upload = driver.findElement(By.cssSelector("input[type='file']"));
upload.sendKeys("/path/to/file.png"); // no Robot needed if input exists
```

## Notes & Best Practices
- Prefer explicit waits instead of Thread.sleep().
- Use driver.close() when you need to close a single tab/window but keep the session.
- Always call driver.quit() in teardown to avoid lingering browser processes.
- Wrap driver operations with try/catch in teardown to ensure quit runs even on failure.
