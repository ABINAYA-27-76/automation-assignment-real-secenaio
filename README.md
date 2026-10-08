# automation-assignment-real-secenaio

### Real-time scenario
Imagine an online student registration form.

1.The automation must:

2.Open the registration page.

3.Enter student name.

4.Enter password.

5.Enter additional information.

6.Select dropdown.

7.Select checkbox.

8.Select radio button.

9.Click Submit.

10.Verify successful submission.
 
### TC	Real-time task	XPath concept
1. TC01	Open student registration page	get()
2. TC02	Locate username	Attribute XPath
3. TC03	Enter password	Attribute XPath
4. TC04	Locate Submit	text()
5. TC05	Locate textbox dynamically	contains()
6. TC06	Locate element with prefix	starts-with()
7. TC07	Find input using two attributes	and
8. TC08	Find element using alternatives	or
9. TC09	Find parent form	parent
10. TC10	Find form from input	ancestor
11. TC11	Find child inputs	child
12.TC12	Find next element	following
13.TC13	Find checkbox	Attribute + XPath
14.TC14	Find radio button	Attribute + XPath
15.TC15	Select dropdown	XPath + Select
16. TC16	Find second textbox	XPath index
17.TC17	Verify submitted message	text()
18.TC18	Find all input fields	find_elements()
19.TC19	Find dynamic element	contains()
20.TC20	Complete registration automation	Multiple XPath concepts
### coding 
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import Select
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

driver = webdriver.Chrome()
driver.maximize_window()

wait = WebDriverWait(driver, 10)

url = "https://www.selenium.dev/selenium/web/web-form.html"

driver.get(url)

print(" PASS - Web form opened")

time.sleep(1)
username = driver.find_element(
    By.XPATH,
    "//input[@id='my-text-id']"
)

username.send_keys("Abinaya")

print(" PASS - Username entered")

password = driver.find_element(
    By.XPATH,
    "//input[@name='my-password']"
)

password.send_keys("Abinaya@123")

print("PASS - Password entered")

submit_text = driver.find_element(
    By.XPATH,
    "//button[text()='Submit']"
)

print(
    "TC04 PASS - Submit located:",
    submit_text.text
)

dynamic_textbox = driver.find_element(
    By.XPATH,
    "//input[contains(@id,'text')]"
)

print(
    " PASS - Dynamic textbox found:",
    dynamic_textbox.get_attribute("id")
)
prefix_element = driver.find_element(
    By.XPATH,
    "//input[starts-with(@id,'my-text')]"
)

print(
    "PASS - Prefix element found:",
    prefix_element.get_attribute("id")
)
username_two_attributes = driver.find_element(
    By.XPATH,
    "//input[@id='my-text-id' and @name='my-text']"
)

print(
    " PASS - Found using AND:",
    username_two_attributes.get_attribute("id")
)
alternative_element = driver.find_element(
    By.XPATH,
    "//input[@id='my-text-id' or @name='my-text']"
)

print(
    " PASS - Found using OR:",
    alternative_element.get_attribute("id")
)

parent = username.find_element(
    By.XPATH,
    "./parent::*"
)

print(
    " PASS - Parent found:",
    parent.tag_name
)

form = username.find_element(
    By.XPATH,
    "./ancestor::form"
)

print(
    " PASS - Form found:",
    form.tag_name
)

child_inputs = form.find_elements(
    By.XPATH,
    ".//child::input"
)

print(
    "PASS - Child inputs found:",
    len(child_inputs)
)


following_element = driver.find_element(
    By.XPATH,
    "//input[@id='my-text-id']/following::input[1]"
)

print(
    "PASS - Following element:",
    following_element.get_attribute("id")
)



checkbox = driver.find_element(
    By.XPATH,
    "//input[@id='my-check-2' and @type='checkbox']"
)

if not checkbox.is_selected():
    checkbox.click()

print(" PASS - Checkbox selected")


radio = driver.find_element(
    By.XPATH,
    "//input[@id='my-radio-2' and @type='radio']"
)

radio.click()

print("PASS - Radio button selected")

dropdown = driver.find_element(
    By.XPATH,
    "//select[@name='my-select']"
)

select = Select(dropdown)
select.select_by_visible_text("Two")

print(
    "PASS - Dropdown selected:",
    select.first_selected_option.text
)


textboxes = driver.find_elements(
    By.XPATH,
    "//input[@type='text']"
)

if len(textboxes) >= 2:

    second_textbox = driver.find_element(
        By.XPATH,
        "(//input[@type='text'])[2]"
    )

    print(
        "PASS - Second textbox:",
        second_textbox.get_attribute("id")
    )

else:

    print("TC16 - Second textbox not available")


print("Verification will be done after Submit")


all_inputs = driver.find_elements(
    By.XPATH,
    "//input"
)

print(
    "TC18 PASS - Total input fields:",
    len(all_inputs)
)

for i, element in enumerate(all_inputs, start=1):

    print(
        "Input", i,
        "| Type:", element.get_attribute("type"),
        "| Name:", element.get_attribute("name"),
        "| ID:", element.get_attribute("id")
    )


dynamic_password = driver.find_element(
    By.XPATH,
    "//input[contains(@name,'password')]"
)

print(
    "TC19 PASS - Dynamic password found:",
    dynamic_password.get_attribute("name")
)

textarea = driver.find_element(
    By.XPATH,
    "//textarea[@name='my-textarea']"
)

textarea.send_keys(
    "No 10  avadi chennai-72"
)

print("Additional information entered")


driver.execute_script(
    "arguments[0].scrollIntoView({block:'center'});",
    submit_text
)

time.sleep(1)
submit_text.click()

print("TC20 PASS - Submit clicked")


try:

    message = wait.until(
        EC.visibility_of_element_located(
            (By.ID, "message")
        )
    )

    print(
        "Submission message:",
        message.text
    )

    if message.text == "Received!":

        print("PASS - Successful submission verified")

    else:

        print("FAIL - Unexpected message")


except Exception as e:

    print("FAIL - Submission message not found")

    print(e)
time.sleep(5)
driver.quit()
```
### Output
<img width="1617" height="937" alt="Screenshot 2026-10-08 120204" src="https://github.com/user-attachments/assets/8d2f1054-3f2b-4326-9340-e471fca6a9ca" />
<img width="1322" height="900" alt="Screenshot 2026-10-08 120210" src="https://github.com/user-attachments/assets/ffff512a-c30f-4aa5-8c7b-9ae8cfd72528" />
<img width="1221" height="945" alt="image" src="https://github.com/user-attachments/assets/18783e5f-5b9a-4310-ba16-23c33c383c97" />

