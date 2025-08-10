# Selenium Locators — Exhaustive Guide

PURPOSE: Help choose the most reliable locator strategy. Includes examples, tips, and XPath/CSS tricks.

## Core locator types
- By.id("id") — fastest and most robust when unique
- By.name("name") — useful for forms
- By.className("class") — good for grouped elements
- By.tagName("tag") — when targeting element types
- By.linkText("link text") — full link text matching
- By.partialLinkText("partial text") — partial match for links
- By.cssSelector("selector") — flexible and fast; recommended over XPath when possible
- By.xpath("xpath") — very powerful for complex DOMs

## CSS selector examples
- `.btn.primary` — element with both classes
- `input[type='submit']` — attribute selector
- `div#main > ul li:nth-child(3)` — child selector
- `a[href^='/products']` — starts-with on attribute
- `a[href$='.pdf']` — ends-with on attribute
- `a[href*='checkout']` — contains on attribute

## XPath examples
- `//button[text()='Login']` — exact text
- `//button[contains(text(),'Log')]` — contains text
- `//div[@class='card']//a[1]` — nested
- `//input[starts-with(@id,'user')]` — starts-with
- `//label[normalize-space()='First name']/following-sibling::input` — sibling traversal

## Advanced techniques
- Use `data-*` attributes in HTML for stable locators, e.g., `By.cssSelector("[data-test='login']")`
- For dynamic IDs: `By.cssSelector("[id^='user_']")` or XPath `starts-with(@id,'user_')`
- Shadow DOM: use `getShadowRoot()` in modern WebDriver or execute JS to reach inside
- Accessibility attributes: `By.cssSelector("[aria-label='Close']")`
- React or Angular: prefer data attributes or use stable parent containers

## Locator selection strategy (priority)
1. ID
2. data-* attribute
3. Name
4. CSS Selector
5. XPath
6. Class or tag (if unique)

## Debugging locators
- Use browser devtools console: `$x("//xpath")` for XPath, `document.querySelectorAll("css")` for CSS
- Validate locators in console before adding to code
- Avoid locators based on CSS order or absolute paths (e.g., `/html/body/...`)
