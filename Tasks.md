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

-  To open a page in a specific browser, use the `webbrowser.get()` function to specify a particular browser.

