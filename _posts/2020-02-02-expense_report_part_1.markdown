---
layout: post
title:      "Expense Report Part 1"
date:       2020-02-02 20:52:20 +0000
permalink:  expense_report_part_1
---

Now that I have a clear path forward I started the development of the project. Step 1 is to ensure the selenium web driver is working properly, which it was. From there I navigated to each site, first PNC and Chase. PNC did not give me any problems whatsoever accessing the html and css selectors to use Selenium to click on the correct inputs(password/username) and then submit. The one road block I did face was figuring out how to ensure my passwords were safe in a secrets file. More on that to come!

On the other hand the Chase website has a very secure login process where the html/css selectors decide not to work. For some reason selenium is not able to pick up any of the html. I have tried multiple times and different methods to access the inputs. At one point it did in fact work and I was able to input my Username and Password. For some reason it stopped working again. I am going to research online to get to the bottom of this, but at least I have my PNC portion all coded and ready to go. Now to talk about the secrets roadblock.

Secrets secrets are no fun unless you tell everyone, but in this case we want to keep our passwords very much so a secret. With the help of google and my old Flatiron instructor I was able to create a secrets file. This was brand new to me as I never had to use credentials for accessing any portion of any project I did. It honestly went quite smoothly. I created a secrets file on my desktop and inside of the folder I created a json file with the credentials. From there I used some nifty code from an old Flatiron lesson to open the json file and read it into the jupyter notebook. From there I stored it in a keys variable and then easily access the different credentials by using the dictionary like system of a json file like so, keys['chase_username]. This would return our username and can be used to send through selenium to log into our banks. This way you never actually see my username and or password and everything is safe and sound.
 

