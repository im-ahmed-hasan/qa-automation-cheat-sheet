# Selenium Waits — Patterns & Examples

PURPOSE: Explain different waiting strategies, why they exist, and pragmatic examples.

## Why waits matter
Web apps are asynchronous. Elements may appear after XHRs, animations, or lazy loading. Proper waits reduce flakiness.

## Implicit Wait
```java
// Sets a default wait for findElement calls. Use sparingly.
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
```

## Explicit Wait (Recommended)
```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
WebElement el = wait.until(ExpectedConditions.elementToBeClickable(By.id("submit")));
```

## Fluent Wait
```java
Wait<WebDriver> wait = new FluentWait<>(driver)
    .withTimeout(Duration.ofSeconds(30))
    .pollingEvery(Duration.ofSeconds(2))
    .ignoring(NoSuchElementException.class);
WebElement el = wait.until(driver -> driver.findElement(By.cssSelector(".ready")));
```

## ExpectedConditions common list
- visibilityOfElementLocated
- elementToBeClickable
- presenceOfElementLocated
- textToBePresentInElement
- frameToBeAvailableAndSwitchToIt

## Anti-patterns
- Avoid long implicit waits + explicit waits together
- Avoid Thread.sleep() except for debugging
