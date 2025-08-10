# Troubleshooting — Common Errors & Fixes

PURPOSE: Quick lookup for common exceptions, root causes, and fixes.

| Error                          | Cause                                | Fix recommendation                    |
|--------------------------------|--------------------------------------|---------------------------------------|
| ElementNotVisibleException     | Element is hidden or offscreen       | Wait for visibility or scroll into view |
| StaleElementReferenceException | DOM changed after locating element   | Re-locate element just before action  |
| TimeoutException               | Waiting period too short             | Increase explicit wait or optimize locator |
| ElementClickInterceptedException | Overlapping element (modal/popups) | Close modal, scroll, or use JS click  |
| NoSuchElementException         | Wrong locator or element removed     | Validate locator in devtools and retry |

## Debugging tips
- Always log request/response for API tests
- Capture screenshots and page source on failure
- Reproduce failing steps manually in browser
- Keep helpful assertions with clear messages
