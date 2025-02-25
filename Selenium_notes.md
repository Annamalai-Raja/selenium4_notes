# selenium4_notes
## **Selenium Architecture – Detailed Explanation**

Selenium is an open-source automation framework used to test web applications across multiple browsers and platforms. Selenium 4 adopts the **W3C WebDriver protocol**, which improves stability and standardization. Below is a deep dive into Selenium's architecture.

---

## **1. Components of Selenium**

Selenium consists of four key components:

### **🔹 Selenium IDE**
- A **record and playback** tool for quick test script creation.
- Primarily used for **prototyping and small tests**.
- Supports **exporting scripts** in various programming languages.

### **🔹 Selenium WebDriver** (Core of Selenium)
- Automates browsers using the **W3C WebDriver Protocol**.
- Supports multiple languages: **Java, Python, C#, JavaScript, Ruby, PHP**.
- Directly interacts with browsers without requiring an intermediate server.

### **🔹 Selenium Grid**
- Used for **parallel execution** of tests on multiple browsers and machines.
- Uses a **Hub-Node architecture** (Selenium 3) and a **fully distributed model** (Selenium 4).

### **🔹 Selenium RC (Deprecated)**
- Was used before WebDriver; replaced due to performance issues.

---

## **2. Selenium 4 Architecture**

Selenium 4 **completely removes JSON Wire Protocol** and communicates **directly with browsers** using the **W3C WebDriver Protocol**.

### **🔹 Selenium Architecture Diagram**
```
Test Script (Java/Python/C#)  
       ↓  
Selenium WebDriver  
       ↓  
Browser Driver (ChromeDriver, GeckoDriver, etc.)  
       ↓  
Browser (Chrome, Firefox, Edge, etc.)
```

### **🔹 Step-by-Step Workflow**
1️⃣ **Test script** (Java, Python, C#, etc.) sends commands to Selenium WebDriver.  
2️⃣ **WebDriver** translates commands into HTTP requests based on the **W3C WebDriver Protocol**.  
3️⃣ The corresponding **browser driver** (e.g., ChromeDriver, GeckoDriver) receives and executes the commands.  
4️⃣ The **browser performs actions** (click, type, navigate, etc.).  
5️⃣ The browser sends the response back to WebDriver, which is then relayed to the test script.

---

## **3. Key Components in Detail**

### **🔹 Selenium WebDriver**
- The core component that allows interaction with browsers.
- Communicates **directly with browser drivers**.
- Uses **RESTful HTTP calls** for sending commands.

### **🔹 Browser Drivers**
- Browser-specific executables that enable communication between WebDriver and the browser.
- Examples:
    - **ChromeDriver** → Chrome
    - **GeckoDriver** → Firefox
    - **EdgeDriver** → Edge
    - **SafariDriver** → Safari

**Example of WebDriver Usage (Java):**
```java
WebDriver driver = new ChromeDriver();  
driver.get("https://www.google.com");  
System.out.println(driver.getTitle());  
driver.quit();
```

---

## **4. Selenium Grid Architecture (Parallel Testing)**

### **🔹 Selenium 3 Grid (Hub-Node Architecture)**
- **Hub**: The central server that receives test execution requests.
- **Nodes**: Machines that execute tests on different browsers/platforms.

```
Test Script → Hub → Multiple Nodes (Chrome, Firefox, Edge)
```

### **🔹 Selenium 4 Grid (Distributed Architecture)**
- No **Hub-Node dependency** – every component can run independently.
- Supports **Docker & Kubernetes** for scalable test execution.
- Uses **GraphQL API** for better test monitoring.

**Run Selenium Grid in Docker:**
```sh
docker run -d -p 4444:4444 --name selenium-grid selenium/standalone-chrome
```

**Connect to Selenium Grid from Java:**
```java
WebDriver driver = new RemoteWebDriver(new URL("http://localhost:4444"), new ChromeOptions());
```

---

## **5. Advantages of Selenium 4 Architecture**
✅ **Standardized with W3C WebDriver** (no JSON Wire Protocol).  
✅ **Faster and more stable** execution.  
✅ **Better parallel testing** with Grid 4.  
✅ **Improved browser compatibility** and **DevTools support**.

Would you like help with **implementing Selenium 4 Grid or writing scalable test scripts**? 🚀## **Selenium 4 Complete Guide**

Selenium 4 is a significant update to the Selenium automation framework, bringing several improvements and new features. Below is a comprehensive guide covering all aspects of Selenium 4.

---

### **6. Key Changes in Selenium 4**
#### 🔹 **W3C WebDriver Protocol**
- Selenium 3 used both the **JSON Wire Protocol** and W3C WebDriver.
- Selenium 4 **fully adopts W3C WebDriver**, making it more stable and compatible with modern browsers.
- **Benefits**:
    - Better browser automation consistency.
    - No additional encoding/decoding between Selenium and browsers.
    - Improved performance and stability.

#### 🔹 **Improved Browser Window & Tab Handling**
- **New Methods**:
    - `driver.switchTo().newWindow(WindowType.WINDOW);` → Opens a new browser window.
    - `driver.switchTo().newWindow(WindowType.TAB);` → Opens a new tab.

#### 🔹 **Relative Locators (Friendly Locators)**
- Helps locate elements **based on their position relative to another element**.
- Available locators:
    - `above(element)`
    - `below(element)`
    - `toLeftOf(element)`
    - `toRightOf(element)`
    - `near(element)`

**Example**:
```java
WebElement password = driver.findElement(By.id("password"));
WebElement loginButton = driver.findElement(with(By.tagName("button")).below(password));
loginButton.click();
```

#### 🔹 **Better Screenshots & Logging**
- **Take full-page screenshots** (available for Firefox).
- Capture screenshots of elements and sections.
- **Example**:
```java
File screenshot = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
FileUtils.copyFile(screenshot, new File("fullpage.png"));
```

#### 🔹 **Enhanced Selenium Grid**
- **Improved architecture**: No need for a separate Hub and Node.
- Supports **Docker & Kubernetes**.
- Uses **GraphQL API** for better querying.

#### 🔹 **Improved Selenium IDE**
- Revamped **Selenium IDE** with better recording and exporting capabilities.
- Can be integrated with CI/CD tools.

#### 🔹 **Chrome DevTools Protocol (CDP) Support**
- Enables interaction with browser developer tools.
- Useful for network interception, performance monitoring, and console logs.

**Example: Capturing Network Logs**
```java
DevTools devTools = ((ChromeDriver) driver).getDevTools();
devTools.createSession();
devTools.send(Network.enable(Optional.empty(), Optional.empty(), Optional.empty()));
devTools.addListener(Network.responseReceived(), response -> {
    System.out.println("Response URL: " + response.getResponse().getUrl());
});
```

---

### **7. Setting Up Selenium 4**
#### **📌 Prerequisites**
- **Java 11+ (Java 21 recommended)**
- Maven or Gradle for dependency management
- WebDriver Manager for automatic driver handling

#### **📌 Add Selenium 4 Dependencies (Maven)**
```xml
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>4.10.0</version>
</dependency>
```

#### **📌 Install WebDriver Manager (Optional)**
```xml
<dependency>
    <groupId>io.github.bonigarcia</groupId>
    <artifactId>webdrivermanager</artifactId>
    <version>5.5.0</version>
</dependency>
```
### **Complete List of Selenium WebDriver Methods**

---

## **1. WebDriver Interface Methods**
These methods are used for browser-level operations.

| **Method** | **Description** |
|------------|---------------|
| `get(String url)` | Opens the specified URL. |
| `getTitle()` | Returns the title of the current webpage. |
| `getCurrentUrl()` | Returns the URL of the current page. |
| `getPageSource()` | Returns the page source (HTML) of the current webpage. |
| `close()` | Closes the current browser window. |
| `quit()` | Closes all browser windows and ends the WebDriver session. |
| `navigate().to(String url)` | Navigates to a given URL. |
| `navigate().back()` | Navigates back in browser history. |
| `navigate().forward()` | Moves forward in browser history. |
| `navigate().refresh()` | Refreshes the current page. |

**Example:**
```java
WebDriver driver = new ChromeDriver();
driver.get("https://www.google.com");
System.out.println(driver.getTitle());
driver.quit();
```

---

## **2. WebElement Methods**
These methods allow interaction with web elements.

| **Method** | **Description** |
|------------|---------------|
| `findElement(By locator)` | Finds a single web element. |
| `findElements(By locator)` | Finds multiple web elements. |
| `click()` | Clicks an element. |
| `sendKeys(String text)` | Types text into an input field. |
| `clear()` | Clears the text from an input field. |
| `getText()` | Retrieves text from an element. |
| `getTagName()` | Gets the tag name of the element. |
| `getAttribute(String name)` | Fetches the value of an attribute. |
| `isDisplayed()` | Checks if the element is visible. |
| `isEnabled()` | Checks if the element is enabled. |
| `isSelected()` | Checks if the element is selected. |
| `submit()` | Submits a form. |

**Example:**
```java
WebElement searchBox = driver.findElement(By.name("q"));
searchBox.sendKeys("Selenium WebDriver");
searchBox.submit();
```

---

## **3. Locators in Selenium**
Selenium supports multiple locator strategies.

| **Locator** | **Example** |
|------------|------------|
| `By.id("id")` | `driver.findElement(By.id("username"));` |
| `By.name("name")` | `driver.findElement(By.name("password"));` |
| `By.className("class")` | `driver.findElement(By.className("btn-primary"));` |
| `By.tagName("tag")` | `driver.findElement(By.tagName("input"));` |
| `By.linkText("text")` | `driver.findElement(By.linkText("Click Here"));` |
| `By.partialLinkText("partial text")` | `driver.findElement(By.partialLinkText("Click"));` |
| `By.cssSelector("css")` | `driver.findElement(By.cssSelector(".login-button"));` |
| `By.xpath("xpath")` | `driver.findElement(By.xpath("//input[@name='q']"));` |

---

## **4. Handling Alerts, Frames & Windows**
### **🔹 Alert Handling**
| **Method** | **Description** |
|------------|---------------|
| `switchTo().alert()` | Switches to an alert. |
| `accept()` | Clicks **OK** on an alert. |
| `dismiss()` | Clicks **Cancel** on an alert. |
| `getText()` | Retrieves alert message text. |
| `sendKeys("text")` | Enters text into a prompt alert. |

**Example:**
```java
Alert alert = driver.switchTo().alert();
System.out.println(alert.getText());
alert.accept();
```

### **🔹 Handling Frames**
| **Method** | **Description** |
|------------|---------------|
| `switchTo().frame(int index)` | Switches to a frame using its index. |
| `switchTo().frame(String nameOrId)` | Switches to a frame using its name or ID. |
| `switchTo().frame(WebElement frameElement)` | Switches to a frame using a WebElement. |
| `switchTo().defaultContent()` | Switches back to the main page. |

**Example:**
```java
driver.switchTo().frame("frame1");
driver.findElement(By.id("submit")).click();
driver.switchTo().defaultContent();
```

### **🔹 Handling Multiple Windows**
| **Method** | **Description** |
|------------|---------------|
| `getWindowHandle()` | Retrieves the current window handle. |
| `getWindowHandles()` | Retrieves all window handles. |
| `switchTo().window(String windowHandle)` | Switches to a specified window. |

**Example:**
```java
String mainWindow = driver.getWindowHandle();
for (String handle : driver.getWindowHandles()) {
    driver.switchTo().window(handle);
}
driver.switchTo().window(mainWindow);
```

---

## **5. Waits in Selenium**
### **🔹 Implicit Wait**
- **Applies globally** to all elements.
- **Waits for a specified time** before throwing `NoSuchElementException`.

```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
```

### **🔹 Explicit Wait**
- **Applies to a specific element**.
- **Uses ExpectedConditions**.

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
WebElement element = wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("username")));
```

### **🔹 Fluent Wait**
- **Allows polling intervals** and **ignores exceptions**.

```java
Wait<WebDriver> fluentWait = new FluentWait<>(driver)
    .withTimeout(Duration.ofSeconds(10))
    .pollingEvery(Duration.ofSeconds(1))
    .ignoring(NoSuchElementException.class);

WebElement element = fluentWait.until(driver -> driver.findElement(By.id("username")));
```

---

## **6. Actions Class (Mouse & Keyboard)**
| **Method** | **Description** |
|------------|---------------|
| `moveToElement(WebElement)` | Moves the mouse over an element. |
| `clickAndHold(WebElement)` | Clicks and holds an element. |
| `doubleClick(WebElement)` | Double-clicks an element. |
| `contextClick(WebElement)` | Performs a right-click. |
| `dragAndDrop(WebElement source, WebElement target)` | Drags and drops an element. |
| `sendKeys(Keys key)` | Sends keyboard inputs. |

**Example:**
```java
Actions actions = new Actions(driver);
WebElement element = driver.findElement(By.id("button"));
actions.moveToElement(element).click().perform();
```

---

## **7. Taking Screenshots**
| **Method** | **Description** |
|------------|---------------|
| `getScreenshotAs(OutputType.FILE)` | Captures a screenshot. |

**Example:**
```java
File screenshot = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
FileUtils.copyFile(screenshot, new File("screenshot.png"));
```

---

## **8. Selenium Grid & RemoteWebDriver**
### **Running Tests in Selenium Grid**
```java
WebDriver driver = new RemoteWebDriver(new URL("http://localhost:4444"), new ChromeOptions());
```

---

## **Conclusion**
This guide covers all essential **Selenium WebDriver methods**, categorized for easy reference. 🚀

Would you like **hands-on exercises** or **real-world scenarios** to practice these methods? Let me know! 😊
#### **📌 Sample Code (Basic Setup)**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import io.github.bonigarcia.wdm.WebDriverManager;

public class Selenium4Demo {
    public static void main(String[] args) {
        WebDriverManager.chromedriver().setup();
        WebDriver driver = new ChromeDriver();
        
        driver.get("https://www.google.com");
        System.out.println("Title: " + driver.getTitle());
        
        driver.quit();
    }
}
```

---

### **8. Selenium 4 with TestNG**
#### **TestNG Integration**
```xml
<dependency>
    <groupId>org.testng</groupId>
    <artifactId>testng</artifactId>
    <version>7.6.1</version>
    <scope>test</scope>
</dependency>
```

#### **Sample TestNG Script**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import io.github.bonigarcia.wdm.WebDriverManager;
import org.testng.annotations.*;

public class TestNGDemo {
    WebDriver driver;

    @BeforeClass
    public void setup() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
    }

    @Test
    public void googleTest() {
        driver.get("https://www.google.com");
        assert driver.getTitle().contains("Google");
    }

    @AfterClass
    public void teardown() {
        driver.quit();
    }
}
```

---

### **9. Selenium 4 with Cucumber**
#### **Dependencies**
```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>7.14.0</version>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-testng</artifactId>
    <version>7.14.0</version>
</dependency>
```

#### **Feature File (GoogleSearch.feature)**
```gherkin
Feature: Google Search
  Scenario: Search in Google
    Given I open Google homepage
    When I search for "Selenium 4"
    Then I should see results related to Selenium 4
```

#### **Step Definitions (GoogleSearchSteps.java)**
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import io.github.bonigarcia.wdm.WebDriverManager;
import io.cucumber.java.en.*;

public class GoogleSearchSteps {
    WebDriver driver;

    @Given("I open Google homepage")
    public void i_open_google_homepage() {
        driver = new ChromeDriver();
        driver.get("https://www.google.com");
    }

    @When("I search for {string}")
    public void i_search_for(String query) {
        driver.findElement(By.name("q")).sendKeys(query + Keys.ENTER);
    }

    @Then("I should see results related to Selenium 4")
    public void i_should_see_results_related_to_selenium_4() {
        assert driver.getTitle().contains("Selenium 4");
        driver.quit();
    }
}
```

---

### **10. Running Selenium 4 in Docker**
- Run Selenium Grid in Docker:
```sh
docker run -d -p 4444:4444 --name selenium-grid selenium/standalone-chrome
```

- **Use RemoteWebDriver**:
```java
WebDriver driver = new RemoteWebDriver(new URL("http://localhost:4444"), new ChromeOptions());
```

---

### *11. Selenium 4 Best Practices** 
✅ Prefer **W3C WebDriver** over deprecated JSON Wire Protocol methods.  
✅ Leverage **relative locators** for dynamic elements.  
✅ Use **explicit waits** instead of `Thread.sleep()`.  
✅ Implement **Page Object Model (POM)** for maintainable tests.

---
