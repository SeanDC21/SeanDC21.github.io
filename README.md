# Sean Cancel
**Cybersecurity & IT Professional Portfolio**

## About Me
I am a college student at Northern Kentucky University studying within the School of Computing and Analytics, with an expected graduation in May 2027. My long-term career ambition is to lead enterprise security strategy as a Chief Information Security Officer (CISO). Currently, I serve as a Resident Assistant, which allows me to develop community leadership skills alongside my technical focus on areas like digital forensics, infrastructure as code, and threat hunting. 

## Resume
[Click here to view my updated Resume (PDF)](Sean_Cancel_Resume.pdf)

## Academic Work & Professional Development

### Industry Exposure: Fifth Third Bank Commercial Banking Experience
I recently participated in the Resolute Man Commercial Banking Experience hosted by Theta Chi Fraternity. During this program, we visited the Fifth Third Bank headquarters and learned directly from professionals in banking and technology operations. We discussed future career opportunities within the organization and focused heavily on core leadership values, including effective communication, active listening, and what it means to lead responsibly.

### Homelab & Independent Learning: System Automation

**Residence Hall Access Provisioning Script**  
*Technologies used: Python, Selenium WebDriver*

To streamline administrative tasks during my Resident Assistant tenure, I developed a Python script utilizing Selenium to automate the manual, repetitive process of provisioning swipe cards in the university's web-based access control system. The script handles iframe switching, DOM element interactions, and includes a global hotkey kill switch as a fail-safe in case the web portal's UI changes during execution.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver import ActionChains
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time
import keyboard
import os

# Kill switch in case the portal UI changes during execution
def emergency_quit():
    print("\n[!] Script aborted.")
    os._exit(1)

keyboard.add_hotkey('`', emergency_quit)

# Setup driver and navigate to portal
driver = webdriver.Chrome()
driver.get("https://rs2.hh.nku.edu/AIUniversal/Main/Cardholders.aspx")

# Wait for manual SSO login and portal load
print("Awaiting manual login... (30s timeout)")
time.sleep(30) 

# Batch list of cards to provision
card_numbers = ["2069", "1317"]

for card in card_numbers:
    print(f"Provisioning card: {card} (Press ` to abort)")
    
    # Open new card dialog
    driver.find_element(By.XPATH, "//span[@title='New Card']").click()
    
    # Wait for and switch to the modal iframe
    WebDriverWait(driver, 10).until(
        EC.frame_to_be_available_and_switch_to_it((By.TAG_NAME, "iframe"))
    )
    
    # Input card details
    card_input = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.ID, "txtCardNumber"))
    )
    card_input.send_keys(card)
    driver.find_element(By.ID, "txtFacilityCode").send_keys("-1")
    
    # Switch to Access Levels tab
    driver.find_element(By.XPATH, "//span[text()='Access Levels']").click()
    time.sleep(1) # wait for DOM update
    
    # Assign specific building access
    new_res_hall = driver.find_element(By.XPATH, "//li[contains(., 'New Residence Hall')]")
    ActionChains(driver).double_click(new_res_hall).perform()
    time.sleep(1) 
    
    # Save and close
    driver.find_element(By.XPATH, "//span[@title='Save']").click()
    time.sleep(3) # wait for backend processing
    
    # Reset context to main page for the next iteration
    driver.switch_to.default_content()

print("Provisioning complete.")
driver.quit()
'''
## Internship Content

### GE Aerospace
**Digital Technology Project Analyst Intern** | *May 2026 – August 2026*

During my internship, I focused on analyzing and optimizing Corporate Affairs tools and processes to drive efficiency and reduce technical debt. My work centered on bridging the gap between business needs and digital solutions.

*   **Software Consolidation & Cost Mitigation:** Analyzed historical contracts and presented business cases for consolidating Digital Asset Management and Philanthropy tools, projecting over $140K in cost savings for the upcoming budget cycle.
*   **Documentation & Standardization:** Established official "Standard Work" practices to guide future documentation. I authored over 30 Confluence pages and implemented a universal product overview template to streamline knowledge transfer.
*   **Stakeholder & Vendor Coordination:** Orchestrated user testing and vendor outreach for new software platforms, coordinating strategic calls to align external partners with internal Corporate Affairs stakeholders.

