# Selenium

### What is the Differenec between WebDriverManager and ThreadGuard Protect? Which one is best to create webdrivers.

| Feature                      | **ThreadGuard-Protected ChromeDriver**                                                                                     | **WebDriverManager**                                                                                                         |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **Purpose**                  | Ensures thread safety for WebDriver instances in multi-threaded test scenarios.                                             | Simplifies management of browser driver binaries (e.g., ChromeDriver, GeckoDriver) for Selenium.                            |
| **Mechanism**                | Uses `ThreadLocal` to create isolated WebDriver instances for each thread, preventing conflicts in parallel tests.          | Automatically downloads and configures the correct WebDriver binary based on the installed browser version.                 |
| **Usage**                    | Combined with `ThreadLocal` to manage isolated drivers per thread.                                                          | Single line setup (`WebDriverManager.chromedriver().setup();`) downloads and sets up the driver if needed.                  |
| **Benefits**                 | Ideal for parallel testing, ensuring each thread has its own WebDriver, reducing driver conflicts.                          | Minimizes manual setup and driver management; ideal for CI/CD pipelines due to automatic driver handling.                  |
| **Downsides**                | Requires manual driver binary management and may need additional configuration for multi-threading.                        | Lacks inherent thread safety; requires additional setup (e.g., `ThreadLocal`) to manage driver instances in multi-threaded tests. |
| **Best Use Cases**           | Best for multi-threaded applications where driver conflicts could occur.                                                    | Suitable for ease of driver management, especially in CI/CD environments and when managing browser driver compatibility.    |
| **Conclusion**               | Preferred for thread safety; prevents driver conflicts in parallel execution.                                              | Provides simpler driver management; use with `ThreadLocal` to achieve both automation and thread safety.                    |

Simple example of using **WebDriverManager** with **ThreadLocal** in Java to manage ChromeDriver instances for multi-threaded test execution.

This setup ensures that each thread gets its own instance of ChromeDriver, which avoids conflicts when running tests in parallel.

### Example Code

1. **Set up WebDriverManager with ThreadLocal**
   - In this example, each test thread will have its own WebDriver instance, managed by ThreadLocal.

```java
import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class WebDriverThreadLocalExample {

    // ThreadLocal for holding WebDriver instances
    private static ThreadLocal<WebDriver> driverThreadLocal = new ThreadLocal<>();

    // Initialize WebDriver for each thread
    public static void initializeDriver() {
        WebDriverManager.chromedriver().setup();  // WebDriverManager handles driver binary management
        driverThreadLocal.set(new ChromeDriver()); // Assign new ChromeDriver instance to each thread
    }

    // Get the WebDriver instance for the current thread
    public static WebDriver getDriver() {
        return driverThreadLocal.get();
    }

    // Quit and remove WebDriver instance for the current thread
    public static void quitDriver() {
        if (driverThreadLocal.get() != null) {
            driverThreadLocal.get().quit();
            driverThreadLocal.remove();
        }
    }
}
```

2. **Using the WebDriver in Tests**
   - Here's how you can use `WebDriverThreadLocalExample` in your test methods.

```java
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class ParallelTests {

    @BeforeEach
    public void setUp() {
        WebDriverThreadLocalExample.initializeDriver();
    }

    @Test
    public void test1() {
        WebDriver driver = WebDriverThreadLocalExample.getDriver();
        driver.get("https://example.com");
        System.out.println("Title in test1: " + driver.getTitle());
    }

    @Test
    public void test2() {
        WebDriver driver = WebDriverThreadLocalExample.getDriver();
        driver.get("https://example.com");
        System.out.println("Title in test2: " + driver.getTitle());
    }

    @AfterEach
    public void tearDown() {
        WebDriverThreadLocalExample.quitDriver();
    }
}
```

### Explanation

- **`initializeDriver()`**: Sets up a new ChromeDriver instance for each test thread and stores it in `ThreadLocal`.
- **`getDriver()`**: Retrieves the WebDriver instance specific to the current thread.
- **`quitDriver()`**: Closes and cleans up the WebDriver instance at the end of each test.

This setup ensures thread-safe management of WebDriver instances when running tests in parallel.