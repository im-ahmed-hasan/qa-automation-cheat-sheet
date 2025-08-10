# JavaScript Executor — When WebDriver Isn't Enough

PURPOSE: Use JS for actions WebDriver struggles with, like interacting with shadow DOM, scrolling, or forcing clicks.

## Basic executor
```java
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("return document.title;");
```

## Scroll into view
```java
js.executeScript("arguments[0].scrollIntoView(true);", element);
```

## Click when WebDriver can't
```java
js.executeScript("arguments[0].click();", element);
```

## Set value directly
```java
js.executeScript("arguments[0].value = 'test@example.com';", element);
```

## Accessing Shadow DOM (example approach)
```java
// Purpose: Get element inside shadow root using JS and return it to WebDriver
WebElement shadowHost = driver.findElement(By.cssSelector("my-component"));
WebElement inner = (WebElement) ((JavascriptExecutor)driver)
    .executeScript("return arguments[0].shadowRoot.querySelector('button')", shadowHost);
inner.click();
```

## Notes
- JS execution can bypass application behavior, so use judiciously.
- Prefer proper locators or framework hooks before relying on JS.
