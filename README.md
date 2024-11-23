1.	Navigate to the FitPeo Homepage:
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class FitPeoNavigation {
    public static void main(String[] args) {
        System.setProperty("webdriver.chrome.driver", "C:\SeleniumTestNG\chromedriver");  

        WebDriver driver = new ChromeDriver();
        driver.get("https://www.fitpeo.com");  
        driver.manage().window().maximize();
        try {
            Thread.sleep(5000);  
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        driver.quit();
    }
}

2.	Navigate to the Revenue Calculator Page:

WebElement revenueCalculatorLink = driver.findElement(By.linkText("Revenue Calculator"));

revenueCalculatorLink.click();

Thread.sleep(5000);


3.	Scroll Down to the Slider section:
WebElement sliderElement = driver.findElement(By.id("revenue-calculator-slider"));
JavascriptExecutor js = (JavascriptExecutor) driver;
js.executeScript("arguments[0].scrollIntoView(true);", sliderElement);
Thread.sleep(5000);
4.	Adjust the Slider:
// Locate the slider element WebElement slider = driver.findElement(By.id("revenue-calculator-slider")); 
// Adjust locator as needed // Locate the text field that shows the value of the slider 

WebElement textField = driver.findElement(By.id("slider-value-textfield")); 
// Adjust locator as needed // Create an Actions instance for dragging the slider 
Actions actions = new Actions(driver); // Get the current position of the slider (optional for dynamic adjustment) 
int initialX = slider.getLocation().getX(); // Get the X position of the slider
 int initialY = slider.getLocation().getY(); // Get the Y position of the slider

5.	Update the Text Field:

WebDriverWait wait = new WebDriverWait(driver, 10); wait.until(ExpectedConditions.attributeToBe(textField, "value", "560"));

6.	Validate Slider Value:

WebElement textField = driver.findElement(By.id("slider-value-textfield"));
WebElement slider = driver.findElement(By.id("revenue-calculator-slider"));
textField.click(); textField.clear();
 // Clear any existing value
 textField.sendKeys("560"); // Enter the value 560
 textField.sendKeys(Keys.ENTER);
Point sliderPosition = slider.getLocation(); 
int sliderX = sliderPosition.getX();
int sliderWidth = slider.getSize().getWidth();
int expectedSliderX = (int) (560 * (sliderWidth / 1000.0));

System.out.println("Slider X position: " + sliderX); 
System.out.println("Expected X position for value 560: " + expectedSliderX);
if (Math.abs(sliderX - expectedSliderX) < 10) { 
System.out.println("Slider position is correctly updated to reflect the value 560.");
 } else {
 System.out.println("Slider position did not update correctly.");
 }
