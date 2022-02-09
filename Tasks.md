<div align = "center">
  
# Step 4
 
## Open Files 
  
</div>

</br>

- OS module in Python provides functions for interacting with the operating system. 
- OS comes under Python’s standard utility modules. 
- This module provides a portable way of using operating system dependent functionality. 
- `os.path` module is sub-module of OS module in Python used for common pathname manipulation.

## Open Apps

```py
import os
os.startfile("Path")
```

- This opens any app installed in the system.

```py
import pyttsx3
import speech_recognition as sr
import os

def takecommand():

    r = sr.Recognizer()

    with sr.Microphone() as source:    

        r.adjust_for_ambient_noise(source)     

        print("Listening... ") 
        r.pause_threshold = 0.8
        audio = r.listen(source, timeout = 1, phrase_time_limit = 5)

    try:
        print("Recognizing... ")
        query = r.recognize_google(audio, language = 'en-in')
        print("User said :", query)

    except Exception as e:

        speak("Say that again please")
        return "Nothing"

    except sr.UnknownValueError:

        print("Could not understand audio")
        return "Nothing"

    except sr.RequestError as e:

        print("Could not request results; {0}".format(e))
        return "Nothing"

    return query
    

if __name__ == "__main__":

    query = takecommand().lower()

    if "open notepad" in query:

        os.startfile("C:\\Windows\\system32\\notepad.exe")
        
    if "open web browser" in query:

        os.startfile("C:\\Program Files\\BraveSoftware\\Brave-Browser-Beta\\Application\\brave.exe")
```

## Open Command Prompt

```py
import os
os.system("start cmd") 
```

## Open Camera

- We can build very interesting applications using the live video stream from the webcam. 
- **OpenCV** provides a video capture object which handles everything related to opening and closing of the webcam. 
- All we need to do is create that object and keep reading frames from it.
- The following code will open the webcam, capture the frames, scale them down by a factor of 2, and then display them in a window. 
- You can press the Esc key to exit.
- We shall use OpenCV's VideoCapture function to create the video capture object cap. 
- Once it's created, we start an infinite loop and keep reading frames from the webcam until we encounter a keyboard interrupt.

```py
ret, frame = cap.read()
```

- Here, `ret` is a Boolean value returned by the `read` function, and it indicates whether or not the frame was captured successfully. 
- If the frame is captured correctly, it's stored in the variable frame. 
- This loop will keep running until we press the Esc key. 
- So we keep checking for a keyboard interrupt.

```py
if c == 27:
```

- The ASCII value of Esc is 27 and once we encounter it, we break the loop and release the video capture object. 
- The line `cap.release()` is important because it gracefully closes the webcam.
- `destroyAllWindows()` destroy's all the windows. 

```py
import cv2

cap = cv2.VideoCapture(0)

if not cap.isOpened():
    raise IOError("Cannot open webcam")

while True:
    ret, frame = cap.read()
    frame = cv2.resize(frame, None, fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA)
    cv2.imshow('Input', frame)

    c = cv2.waitKey(1)
    if c == 27:
        break

cap.release()
cv2.destroyAllWindows()
```


## Play Music

- `os.path.join()` method in Python join one or more path components intelligently. 
- This method concatenates various path components with exactly one directory separator (‘/’) following each non-empty part except the last path component. 
- If the last path component to be joined is empty then a directory separator (‘/’) is put at the end. 
- If a path component represents an absolute path, then all previous components joined are discarded and joining continues from the absolute path component.

```py
import random

music_directory = "Songs Directory" 
songs = os.listdir(music_directory)
os.startfile(os.path.join(music_directory, songs[random.randint(0, <No of Songs>)]))
```

## Get IP Information

- To get the IP address in Python of your computer we need to import the socket library, and then we can find the IP address of the computer, laptop, etc and they have their unique IP address.
- First, import the socket module and then get the **host name** using the `socket.gethostname()`.
- The **IP address** can be found by passing the **host name** as an argument to the `socket.gethostbyname()`.


```py
import socket

host = socket.gethostname()

IP = socket.gethostbyname(host)

print("Host Name is:" + host)

print("Computer IP Address is:" + IP)
```

## Get Summary from Wikipedia

- We will be using the **Wikipedia API** to retrieve data from Wikipedia. 
- Data scraping has seen a rapid surge owing to the increasing use of data analytics and machine learning tools. 
- The Internet is the single largest source of information, and therefore it is important to know how to fetch data from various sources. 
- And with Wikipedia being one of the largest and most popular sources for information on the Internet, this is a natural place to start.
- In order to extract data from Wikipedia, we must first install the Python Wikipedia library, which wraps the official Wikipedia API. 

```py
pip install wikipedia
```

- Once the installation is done, we can use the Wikipedia API in Python to extract information from Wikipedia. 
- In order to call the methods of the Wikipedia module in Python, we need to import it using the `import` command.

```py
import wikipedia
```

- We can extract the summary of a Wikipedia article using the `summary()` method. 
- The article for which the summary needs to be extracted is passed as a parameter to this method.

```py
print(wikipedia.summary(""))
```

- The whole summary will be printed in the output. 
- We can customize the number of sentences in the summary text to be displayed by configuring the sentences argument of the method.

```py
print(wikipedia.summary("", sentences=2))
```

- `wikipedia.summary` will raise a **disambiguation error** if the page does not exist or the page is disambiguous.
- So we have to specify most specifically to get the correct summary.

## Launch a Web Browser

- The `webbrowser` module is a convenient web browser controller. 
- It provides a high-level interface that allows displaying Web-based documents to users. 
- `webbrowser` can also be used as a CLI tool. 
- It accepts a URL as the argument with the other optional parameters like, 
  - -n Opens the URL in a new browser window
  - -t Opens the URL in a new browser tab

```py
import webbrowser

webbrowser.open('http://www.google.com')
```

- This opens the requested page using the default browser.

```py
webbrowser.open_new('http://www.google.com')
```

- This will try to open the page in a new browser window or tab, if possible and supported by the browser. 

```py
search = webbrowser.get('chrome')

search.open('http://www.google.com')
```

- To open a page in a specific browser, use the `webbrowser.get()` function to specify a particular browser.


## Send a WhatsApp Message

- We can automate WhatsApp to send messages using the `pywhatkit` module which utilizes the **web.whatsapp.com** webpage to automate message sending to any number on WhatsApp.
- To install the pywhatkit module, we can use the pip command.

```py
pip install pywhatkit
```

- This command will download the pywhatkit module.
- To use this python module to send message automatically on WhatsApp at a set time, we need browser and you must have your WhatsApp logged into **web.whatsapp.com** website.

 ```py
import pywhatkit as kit

kit.sendwhatmsg("+91**", "Message", 18, 21)
```

- In the above code, we have specified the mobile number on which we want to send the message, then the message, and then the time at which the message has to be sent. 
- This module follows the 24 hrs time format, hence the time 18:21 is 06:21 PM.
- Also, you should provide atleast 4-5 minutes future time from the current time while running the script, because if you will set the time 1-2 minute from current time, then the module will give error.

## Play Song on YouTube 

- Function `pywhatkit.playonyt()`, opens the YouTube in your default program and plays the video you referenced in the capacity. 
- In the event that you pass the point name as a boundary, it plays the arbitrary video on that subject. 
- On passing the URL of the video as the boundary, it open that precise video. 

```py
kit.playonyt("Song Name")
```

## Send Email

- Python, being a powerful language don’t need any external library to import and offers a native library to send emails `SMTP lib`.
- This library is the most popular one when it comes to sending email with Python. 
- `smtplib` creates a Simple Mail Transfer Protocol client session object which is used to send emails to any valid email id on the internet. 
- We use port numbers to send mails and different websites use different port numbers.
- Gmail uses the Port number **587**.

> :warning: Before sending an email using this module, you need to [**enable access to less secure apps**](https://support.google.com/accounts/answer/6010255#zippy=%2Cif-less-secure-app-access-is-on-for-your-account) in the email you will be using as the sender.

```py
s = smtplib.SMTP('smtp.gmail.com', 587)
```

- Here we are creating a session to use its instance SMTP to encapsulate an SMTP connection.
- In this, you need to pass the first parameter of the server location and the second parameter of the port to use. 
- For security reasons, now put the SMTP connection in the TLS mode which encrypts all the SMTP commands. 

```py
server.login('youremail@gmail.com', 'Password')
```

- For security and authentication, you need to pass your Gmail account credentials in the login instance.
- The compiler will show an authentication error if you enter invalid email id or password.

```py
server.sendmail('youremail@gmail.com','receiver_adress@outlook.com', 'Hello')
```

- Using the `sendmail()` instance, send your message. 
- `sendmail()` uses three parameters, 
  - sender_email_id
  - receiver_email_id and 
  - message_to_be_sent 
- The parameters need to be in the same sequence in order to send the email from your account. 
- After completion terminate the **SMTP** session by using `quit()`.

```py
import smtplib

server = smtplib.SMTP_SSL('smtp.gmail.com', 465)

server.login('youremail@gmail.com', 'Password')

server.sendmail('youremail@gmail.com','receiver_adress@outlook.com', 'Hello')

server.quit()
```

- If you need to send the same message to different people, you can insert a **loop** between the initialization and termination of the SMTP session. 
- Loop will initialize turn by turn and after sending the email, SMTP session will be terminated.

```py
import smtplib
  
list_of_email = ["xxxxx@gmail.com", "yyyyy@gmail.com"]
  
for dest in list_of_email:

    s = smtplib.SMTP('smtp.gmail.com', 587)
    
    s.starttls()
    
    s.login("sender_email_id", "sender_email_id_password")
    
    message = "Message"
    
    s.sendmail("sender_email_id", dest, message)
    
    s.quit()
```

- One of the other alternatives is **Yagmail** which is a **GMAIL** client that aims at making it even more simple to send emails.
- It is extremely easy to add things to the email (attachments, subject, links, etc) while it is not as straighforward when using **SMTPLIB**.

```py
import yagmail

yag = yagmail.SMTP('youremail@gmail.com', 'Password')

contents = ['Testing', 'Files are also attached', '<Full Path>']

yag.send('receiver@outlook.com', 'Demo', contents)
```

- In this **test** is actually the subject of the email while in contents, you can add the message and attachments (images, word document, audio file, etc).


## Switch Windows

- `PyGetWindow` is a simple, cross-platform module for obtaining GUI information on and controlling application's windows.

```py
pip install pygetwindow
```

- `PyGetWindow` has functions for obtaining Window objects from a place on the screen, from the window title, or just getting all windows.
- Window objects can be **minimized/maximized/restored/activated/resized/moved/closed** and also have attributes for their current position, size, and state.

```py
a = gw.getAllTitles()
```

-  `getAllWindows()` Returns a list of Window objects for every visible window on the screen.

```py
a = [i for i in a if i]
```

- This removes all blank windows.

```py
[window.append(x) for x in a if x not in window]
```

- This removes all duplicate windows. 

```py
system_apps = ["Settings", "Microsoft Text Input Application", "Program Manager"]
 
window = [i for i in window if i not in system_apps]
```

- In this `system_apps` is the list which contains all inbuilt system apps which are running in background.
- Since they are not required, it can be removed from the list.

> **Alt + Tab** lets you switch between open windows. Just press **Alt + Tab**, hold the **Alt** key down, and then keep pressing the **Tab** key to scroll through your open windows. Release the **Alt** key when you see an outline around the window you want.

- `keyDown()` function is same as **Holding the Key**.
- `press()` function is same as **Pressing the Key**.
- `keyUp()` function is same as **Releasing the Key**.

```py
pyautogui.keyDown("alt")

pyautogui.press("tab")

pyautogui.keyUp("alt")
```

## Booking tickets for Train, Flight and Bus
- We can book Train, Bus or Flight tickets using MakeMyTrip.
- First, the User specifies which mode of transport he prefers. 
- If the choice is train, the user can choose whether he needs to book a ticket, check PNR status or to check the Live Train Status
- The command prompt will open the website based on the User's choice
- If the choice is bus, the User will be re-directed to the Bus Booking Page
- If the choice is Flight, the User will be re-directed to the Flight Booking Page

```py

def makemytrip():

    speak("Train, bus or flight")

    query = takecommand().lower()

    if query == "train":

        speak("book train ticket or check pnr status or check live train status")

        query1= takecommand().lower()

        if "book" or "ticket" in query1:

            print("Redirecting to Booking Page")

            webbrowser.open("https://www.makemytrip.com/railways/%22)

        elif "pnr" in query1:

            speak("What is Your Pnr number")

            no = takecommand()

            print("Redirecting to pnr status page")

            webbrowser.open("https://www.makemytrip.com/railways/pnrsearch/?pnr=%22+no)

        else:

            print("redirecting to live train status page")

            webbrowser.open("https://www.makemytrip.com/railways/liveStatus/%22)

    elif query == "bus":

        print("Redirecting to Bus Booking")

        webbrowser.open("https://www.makemytrip.com/bus-tickets/%22)


    elif query == "flight":

        print("redirecting to Flight Booking")

        webbrowser.open("https://www.makemytrip.com/flights/%22)
```
