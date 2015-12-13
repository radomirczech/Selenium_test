__author__ = 'Radomir Czech'

# This is a Selenium test based on a specific scenario made as a pre-technical interview.
# -*- coding: utf-8 -*-

from selenium import selenium
import unittest, time, re

class RemoteControl(unittest.TestCase):
    def setUp(self):
        self.verificationErrors = []
        self.selenium = selenium("localhost", 4444, "*chrome", "http://rst.com.pl/")
        self.selenium.start()
    
    def test_remote_control(self):
        sel = self.selenium
        sel.open("http://demo.opencart.com/")
        sel.click("//form[@id='currency']/div/button")
        sel.click("name=GBP")
        sel.wait_for_page_to_load("30000")
        sel.type("name=search", "iPod")
        sel.click("xpath=(//button[@type='button'])[4]")
        sel.wait_for_page_to_load("30000")

        # 4 lines below could be coded in a more intelligent way.
        # (In the loop or by somehow finding and clicking all adding buttons on the web page)
        sel.click("xpath=(//button[@type='button'])[11]")
        sel.click("xpath=(//button[@type='button'])[15]")
        sel.click("xpath=(//button[@type='button'])[18]")
        sel.click("xpath=(//button[@type='button'])[21]")
        sel.click("id=compare-total")
        sel.wait_for_page_to_load("30000")

        # Removal could be solved better too probably. Unfortunately I don't know how to connect "Out of stock"
        # text line with removal button on a specific product.
        sel.click("link=Remove")
        sel.wait_for_page_to_load("30000")
        the_price = sel.get_text("//div[@id='content']/table/tbody/tr[3]/td[2]")
        sel.click("//input[@value='Add to Cart']")
        sel.click("//div[@id='top-links']/ul/li[4]/a/span")
        sel.wait_for_page_to_load("30000")
        try: self.assertEqual(the_price, sel.get_text("//div[@id='content']/div[2]/div/table/tbody/tr[4]/td[2]"))

        # I know, this is the Python 2 code, but again - I don't know how it can be changed.
        # Btw. Why doesn't Selenium IDE support Python 3? :)
        except AssertionError, e: self.verificationErrors.append(str(e))
    
    def tearDown(self):
        self.selenium.stop()
        self.assertEqual([], self.verificationErrors)

if __name__ == "__main__":
    unittest.main()
