using OpenQA.Selenium;
using OpenQA.Selenium.Chrome;
using System;

namespace SeleniumTest
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize ChromeDriver (make sure chromedriver.exe is in your PATH)
            using (IWebDriver driver = new ChromeDriver())
            {
                try
                {
                    // Navigate to a website
                    driver.Navigate().GoToUrl("https://www.example.com");

                    // Find an element by its tag name and output its text
                    IWebElement header = driver.FindElement(By.TagName("h1"));
                    Console.WriteLine("Header text: " + header.Text);

                    // Find an element by its name attribute and enter text
                    IWebElement searchBox = driver.FindElement(By.Name("q"));
                    searchBox.SendKeys("Selenium");

                    // Submit the search form
                    searchBox.Submit();

                    // Wait for a few seconds to see the result
                    System.Threading.Thread.Sleep(2000);

                    // Verify the title of the resulting page
                    string pageTitle = driver.Title;
                    Console.WriteLine("Page title: " + pageTitle);
                }
                catch (NoSuchElementException e)
                {
                    Console.WriteLine("Element not found: " + e.Message);
                }
                catch (Exception e)
                {
                    Console.WriteLine("An error occurred: " + e.Message);
                }
                finally
                {
                    // Close the browser
                    driver.Quit();
                }
            }
        }
    }
}
