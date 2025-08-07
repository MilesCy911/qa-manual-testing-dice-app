# 🧪 Selenium Automation – Setup & Troubleshooting Log

This log captures the full journey of setting up and troubleshooting Selenium automation using Google Colab for the Dice Roller app:

🔗 Live App: [https://milescy911.github.io/qa-manual-testing-dice-app/](https://milescy911.github.io/qa-manual-testing-dice-app/)

---

## ✅ Objective

Automate a test that:
- Opens the live Dice Roller web app
- Clicks the "Roll" button
- Verifies that the result updates
- Saves a screenshot

---

## 🧱 Initial Setup Attempt

### Tools Used:
- **Google Colab**
- **Python 3.11**
- **Selenium + ChromeDriver**

### First Steps:

```python
!apt-get update
!apt install chromium-browser chromium-chromedriver
!cp /usr/lib/chromium-browser/chromedriver /usr/bin
!pip install selenium

Then ran the testing

from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
...

❌ Error Encountered:

WebDriverException: Message: Service /usr/bin/chromedriver unexpectedly exited.
Status code was: 1

Explanation:
Colab's Chrome and ChromeDriver were out of sync, or Chrome was blocked from launching headless inside the container.

🌀 Attempted Manual Version Match
Installed Chrome 114 + matching ChromeDriver:

!apt install chromium-browser=114.0.5735.90-0ubuntu0.20.04.1
!wget https://chromedriver.storage.googleapis.com/114.0.5735.90/chromedriver_linux64.zip
...

❌ New Error:

Chrome failed to start: exited abnormally.
(DevToolsActivePort file doesn't exist)

Explanation:

Colab's sandbox prevented Chrome from opening a headless session due to container isolation.

Switched to SeleniumBase with uc_driver (Tried using seleniumbase and undetected Chrome mode )

from seleniumbase import Driver
driver = Driver(uc=True, headless=True)

😭 Another Error:

SessionNotCreatedException: cannot connect to chrome at 127.0.0.1:9222

Explanation:
Recent Chrome updates and Colab sandboxing block undetected headless Chrome sessions entirely.

Attempted Installing SeleniumBase Standard Driver

!pip install seleniumbase==4.21.5

Final Script finally executed:

from seleniumbase import SB
from datetime import datetime
import os
from IPython.display import Image, display

os.makedirs("screenshots", exist_ok=True)

with SB(headless=True) as sb:
    sb.open("https://milescy911.github.io/qa-manual-testing-dice-app/")
    
    old_text = sb.get_text("#result")
    sb.click("button")
    sb.sleep(1)
    new_text = sb.get_text("#result")

    assert old_text != new_text, "❌ Result did not change!"

    timestamp = datetime.now().strftime("%Y%m%d-%H%M%S")
    path = f"screenshots/dice_roll_{timestamp}.png"
    sb.save_screenshot(path)
    print(f"✅ Test passed! Screenshot saved at {path}")
    display(Image(filename=path))

    🧠 Key Takeaways
💡 I explored multiple configurations, driver versions, and fallback tools.

🧰 I understood sandbox limits in Colab and adjusted strategies accordingly.

✅ I successfully implemented a cloud-based test that validates real app behavior and logs evidence.

