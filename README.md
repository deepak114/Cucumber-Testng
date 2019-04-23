# Cucumber-Testng
Cucumber is a test automation framework which leverages Behavior Driven Development for collaboration in between Business and IT teams. It empowers a user to define an application’s behavior in plain English language which makes it easier for non-programmers to understand the acceptance criteria. The core of cucumber has been developed in Ruby programming language however it supports all the majorly used programming languages for testing such as Java, C#, Python. In this repo, I will be demonstrating automation testing with Selenium, Cucumber and TestNG.

What Is Behavior Driven Development?

Behavior Driven Development is derived from Test Driven Development as a software development methodology. As a part of the Test Driven Development approach, the developer creates tests as a part of the acceptance criteria first. The developer will make sure the test is passed and will commit changes in the code. if required. Test Driven Development is a way to ensure the system meets its requirements by ensuring a 100% test coverage. It provides an edge over other methodologies in terms of finding defects early in the cycle which reduces the cost of finding bugs and refactoring improves the code.
Cons of Test Driven Development are the maintenance of tests created, it is a test-centric methodology, non-programmers might find it hard to understand for performing selenium automation testing. The test or acceptance criteria being targeted makes it hard for team collaboration. To overcome the above trouble heads, Behavior Driven Development was introduced to reduce the time to test, less code with more collaboration.

Advantages Of Using BDD For Automation Testing With Selenium & Cucumber.

Collaborative Approach: Bridges the communication gap between stakeholder or business teams who can’t easily understand or read the code. This problem is addressed by defining the behavior of application under test in a ubiquitous language i.e. easily understandable.
Focuses more in terms of end-user experience or inclined more towards behavior specifications while compared to that of traditional Test Driven methodology. Tests are written more in end user’s point of view.
which provides an easier understanding for performing Selenium automation testing.

How Cucumber Leverages BDD For Selenium Automation Testing?

As discussed earlier, Cucumber is a test automation tool that supports Behavior Driven Development. It makes use of user-defined specifications to validate the application under test. Before we step into performing automation testing with Selenium & Cucumber, let me tell you about the three major parts of the cucumber framework i.e. Feature file, Step Definitions, and Test Runner file.

Feature File would enable the user to define the behavior of the application in plain English text with help of Gherkin Language. Gherkin is used to define executable specifications with the help of a predefined set of contextual keywords. Keywords involved are demonstrated with the help of the below example:

Feature: High-level description of a software feature or behavior of application under test.

Scenario: Feature file can contain more than one scenario which acts as a test case derived from test scenarios/behaviors. It also symbolizes and acts as one or more user perspectives involved.

Annotations: Keywords which hold a specific meaning and would help and defined the meaning of a scenario. Sample keywords involved are GIVEN, WHEN, THEN & AND.

GIVEN: Define pre-requisites of the application.
WHEN: Trigger point for a scenario execution can be related more towards steps to be executed.
THEN: Defined an outcome more like the expected result.
AND: Acts as a logical bridge AND in between two statements.
Scenario Outline: It’s a template provided to carry out scenario execution, test data table provided in the Examples section would replace variables/arguments created making each individual row in a table as a unique scenario.

Tags: It paves the way to organize your tests based on your tag definition.
Feature file example:

Feature: Place order on the Amazon website.
@SmokeTest
Scenario: Validate if the guest user is able to add a product to cart.
GIVEN user is logged onto the Amazon website as a guest user.
WHEN user searches a product on the homepage.
THEN user should be able to view product information related to product searched.
AND user click on add to cart button
THEN user verifies if the product is added to cart
 
Scenario Outline: 
Validate if a registered user is able to place an order.
	GIVEN user is logged onto the Amazon website as a registered user.
	WHEN user logs in with <username> and <password>
	THEN user should be able to view homepage.
WHEN user searches for <productID>
THEN user should be on the product information page.
AND user tried to add the product to cart
THEN product should be added to cart.
WHEN user navigates to order confirmation page via express checkout option.
THEN order should be placed successfully along with order confirmation id being generated. 
  
Step Definition file 

created would be consisting of a code which defines the steps for annotations created in feature file. An annotation followed by step defined in patterns with the help of regular expression would help in linking the step definition file to steps in feature file. Sample step definition code sample for above code is defined as above.

@Given("^user is logged onto Amazon website as a guest user $")
public void user_is_on_Home_Page() throws Throwable {
driver = new FirefoxDriver();
driver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);
driver.get("http://www.amazon.in");
}
@When("^user searches a product on homepage $")
public void user_searches_a_product() throws Throwable {
driver.findElement(By.xpath(".//*[@id='account']/a")).click();
}

@Given("^user is logged onto Amazon website as a guest user $")
public void user_is_on_Home_Page() throws Throwable {
driver = new FirefoxDriver();
driver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);
driver.get("http://www.amazon.in");
}
@When("^user searches a product on homepage $")
public void user_searches_a_product() throws Throwable {
driver.findElement(By.xpath(".//*[@id='account']/a")).click();
}  
  
 Test Runner file 
  Defined the location of step definition and primarily provides all the metadata information required for test execution. It makes use of ‘@RunWith()’ annotation from JUnit framework for execution. Secondarily you would be making use of ‘@CucumberOptions’ annotation to define the location of feature files, step definitions location through glue, what reporting integrations to use etc.

Below is the sample of feature file created.
    
import org.junit.runner.RunWith;
import cucumber.api.CucumberOptions;
import cucumber.api.junit.Cucumber;
 
@RunWith(Cucumber.class)
@CucumberOptions(
		features = "src/test/Feature"
		,glue={"src/main/stepDefinition"}
		)
 
public class TestRunner {
 
}

