# Automation Testing FAQ's:
1. Difference between implicit and explicit waits.
    - implicit
        - Scope - Global (applies to all element lookups).
        - Waits for an element to be found.
        - Less precise control over waiting.
        - Can lead to unnecessary delays.
        - `driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS); `
    - explicit
        - Local (applies to specific conditions).	
        - Waits for a specific condition to be met.
        - More precise control over waiting conditions.
        - More efficient and stable test execution.
        - ```Java
            WebDriverWait wait = new WebDriverWait(driver, 10); 
            wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("myElement")));
            ```

2. Asked to share screen and write XPath for a given element.
    `WebElement form = driver.findElement(By.xpath("//form[@id='loginForm']")); `

3. Use of the Actions class and Select class.
    - Action Class
        - To perform any operations on the web application such as move to element,double-click, selecting drop-down boxes, etc. the **actions** class is required.
        - ```Java 
            Actions action = new Actions(driver);
            action.moveToElement(element).click().perform();
        ```
    - Select Class
        - In Selenium, the Select class provides the implementation of the HTML SELECT tag.The helper methods with select and deselect options.
        - Different Select Class Methods to handle Select Dropdown in Selenium
            - selectByVisibleText :
                - ```Java
                    Select objSelect =new Select(driver.findElement(By.id("search-box")));
                    objSelect.selectByVisibleText("Automation");
                    ```
            - selectByVisibleText
            - selectByValue          

4. Exceptions faced while working with Selenium (Give 5 examples).
5. Difference between findElement() vs findElements().
    - `findElement()` is used to locate and interact with a single element,throwing an exception info Element is matching
    - `findElements()` is used to locate multiple elements, returning an empty list if none are matching.

6. How to handle alerts in Selenium?
    `driver.switchTo().alert()`

7. Difference between Scenario vs Scenario Outline in Cucumber BDD.
    - Both keywords are used to write scenario. But if we want to run a scenario multiple times with different test data, then we use a **Scenario outline**.
        - Example:
            ```java
                Scenario Outline: Eating
                Given there are <start> cucumbers
                When I eat <eat> cucumbers
                Then I should have <left> cucumbers

                Examples:
                    | start | eat | left |
                    |  12   |  5  |  7   |
                    |  20   |  5  |  15  |
            ```

8. What are tags in Cucumber?
    - `@RunWith(Cucumber.class) `
    - ```java 
        @Cucumber.Options(
        features ="classpath:features/regression",
        glue = {"stepdefinitions"}
        format = {"pretty", "html:target/cucumber"}, tags = {"~@SmokeTest"})`
        ```

9. What is BDD & What is TDD?
    - In software development, TDD (Test-Driven Development) and BDD (Behavior-Driven Development) are both methodologies that emphasize testing to improve software quality.
    - Test-Driven Development (TDD)
        - It is about building reliable code, test-first. 
        - Focus:
            - Writing tests before implementing code, ensuring each function works as intended. 
        - Process:
            - Developers write a failing test, then write the code to make the test pass, and finally refactor the code. 
        - Goal:
            - To create reliable and bug-free code by identifying errors early in the development process. 
        - Example:
            - Writing a test for a function that calculates the sum of two numbers before writing the function itself. 
    
    - Behavior-Driven Development (BDD)
        - It is about building software that meets user needs, test-first, and with collaboration. 
        - Focus:
            - Defining and testing the system's behavior from the user's perspective, ensuring the software meets user expectations. 
        - Process:
            - Collaborating with stakeholders to define scenarios and requirements, then using these scenarios to guide development and testing.  
        - Goal:
            - To ensure the software aligns with user requirements and business objectives. 
        - Example:
            - Writing a test scenario using Gherkin syntax that describes how a user would log into the application and what the expected outcome would be. 



