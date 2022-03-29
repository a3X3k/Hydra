<div align = "center">

# Step 1
 
## Text-To-Speech using Pyttsx3 
  
</div>

</br>

- `pyttsx3` is a text-to-speech conversion library in Python. 
- Unlike alternative libraries, it works offline and is compatible with both Python 2 and 3. 
- An application invokes the `pyttsx3.init()` factory function to get a reference to a pyttsx3 engine instance. 
- The pyttsx3 module supports two voices first is female and the second is male which is provided by **sapi5** for windows.
- It supports three TTS engines, 

  - **sapi5** – SAPI5 on Windows
  - **nsss** – NSSpeechSynthesizer on Mac OS X
  - **espeak** – eSpeak on every other platform

```py
pip install pyttsx3
```

- This will install the `pyttsx3` library.

- Import the `pyttsx3` package that we’ve installed using the pip. 

```py
import pyttsx3
```

- Next step is to initialize the pyttsx3 package. 

```py
engine = pyttsx3.init()
```

- The Instance of the initialized pyttsx3 package is stored in the **engine** variable. 
- We are calling the variable engine as it works as the engine and converts Text-To-Speech whenever execute the functions from the package.

- There is a built-in `say()` function in the pyttsx3 package that takes a string value and speaks it out.

```py
engine.say("Hello")
```

- Next step is to start the conversion. 

```py
engine.runAndWait()
```

- `runAndWait()` function keeps track when the engine starts converting text to speech and waits for that much time, and do not allow the engine to close. 
- It also synchronizes the processes.

- After all the processes are over, we shall shut down the engine by calling the `stop()` function.

```py
engine.stop()
```

- We can also change the voice of the engine, the default is the voice of a male named David.
- To change the voice of the pyttsx3 engine, first, we will have to get the list of objects of voices.

```py
voices = engine.getProperty('voices')
```

- The `getProperty()` function of the pyttsx3 package takes a string as a parameter and returns an object matching the string.
- When we print the voices, we get a list that contains two objects.

  - voices[0] – Male Voice (Default) - Microsoft David Desktop
  - voices[1] – Female Voice - Microsoft Zira Desktop

- `setProperty()` function is used to set property based on a string.

```py
engine.setProperty('voice', voices[0].id)
engine.setProperty('voice', voices[1].id)
```

- We can also change the Speed of the Speech Engine.
- Get the Speed Rate of the engine using the `getProperty()` function and print it.

```py
rate = engine.getProperty('rate')
print (rate)
```

- The Default Speed Rate of the Speech Engine is 200.
- If we set the Speed below 200 the voice will speak slowly and above 200 will increase the speed rate of the engine.

```py
engine.setProperty('rate', 100) # Decrease the Speed Rate x2

engine.setProperty('rate', 250) # Increase the Speed Rate x1.25
```

### Final Code of Step 1

```py
import pyttsx3

engine = pyttsx3.init()

voices = engine.getProperty('voices')

engine.setProperty('voice', voices[1].id)

engine.setProperty('rate', 140)

def speak(audio):

    print(audio)
    engine.say(audio)
    engine.runAndWait()

if __name__ == "__main__":

    speak("Hello Hydra!")
```    

<div align = "center">
  
# Step 2
 
## Speech Recognition
  
</div>

</br>

- Speech recognition is the process of converting spoken words to text. 
- Python supports many speech recognition engines and APIs, including Google Speech Engine, Google Cloud Speech API, Microsoft Bing Voice Recognition and IBM Speech to Text.
- **Speech Recognition** is a library for performing speech recognition, with support for several engines and APIs, online and offline.
- The SpeechRecognition module depends on pyaudio. 

```py
pip install SpeechRecognition
```

- This will install the `SpeechRecognition` library.

```py
import speech_recognition as sr
```

- This will import the `SpeechRecognition` package that we’ve installed using the pip. 

```py
r = sr.Recognizer()
```

- `Recognizer()` is a class of speech_recognition library. 
- It contains methods that help us to recognize the voice of a particular format.
- Recognizer() class contains the methods for speech recognition APIs.
- APIs available for Speech Recognition,
  - recognize_bing()
  - recognize_google()
  - recognize_google_cloud()
  - recognize_houndify()
  - recognize_ibm()
  - recognize_sphinx()
  - recognize_wit() 

```py
with sr.Microphone() as source:         
```

- This uses the default Microphone as the audio source. 

```
r.adjust_for_ambient_noise(source)
```

- Listen for 1 second to calibrate the energy threshold for ambient noise levels.

```py
r.energy_threshold = 300
```

- Represents the energy level threshold for sounds. 
- Values below this threshold are considered silence, and values above this threshold are considered speech. 

```py
r.pause_threshold = 0.8
```

- This represents the minimum length of silence (in seconds) that will register as the end of a phrase.
- Smaller values result in the recognition completing more quickly, but might result in slower speakers being cut off.


```py
audio = r.listen(source, timeout = 1, phrase_time_limit = 5)
```

- This records a single phrase from source (an AudioSource instance) into an AudioData instance, which it returns.
- This is done by waiting until the audio has an energy above `r.energy_threshold` (the user has started speaking), and then recording until it encounters `r.pause_threshold` seconds of silence or there is no more audio input. 
- The ending silence is not included.
- The timeout parameter is the maximum number of seconds that it will wait for a phrase to start before giving up and throwing an OSError exception. 
- If None, it will wait indefinitely.
- The `phrase_time_limit parameter` is the maximum number of seconds that this will allow a phrase to continue before stopping and returning the part of the phrase processed before the time limit was reached. 
- The resulting audio will be the phrase cut off at the time limit. 
- If `phrase_timeout` is None, there will be no phrase time limit.

```py
r.recognize_google(audio_data, key = None, language = "en-US", show_all = False)
```

- Performs speech recognition on `audio_data` (an AudioData instance), using the Google Speech Recognition API.
- The recognition language is determined by language, an IETF language tag like **en-US** or **en-GB**, defaulting to US English. 
- Returns the most likely transcription if `show_all` is false (the default), else returns the raw API response as a JSON dictionary.

```py
try:

    r.recognize_google(audio, language='en-in')
        
except Exception as e:

    speak("Say that again please")
    return "Nothing"

except sr.UnknownValueError:

    print("Could not understand audio")
    return "Nothing"

except sr.RequestError as e:

    print("Could not request results; {0}".format(e))
    return "Nothing"
```

- Raises a `speech_recognition.UnknownValueError` exception if the speech is unintelligible. 
- Raises a `speech_recognition.RequestError` exception if the key isn’t valid, the quota for the key is maxed out, or there is no internet connection.

### Final Code of Step 2

```py
import speech_recognition as sr

def takecommand():

    r = sr.Recognizer()

    with sr.Microphone() as source:    

        r.adjust_for_ambient_noise(source)     

        print("Listening... ") 
        r.pause_threshold = 1
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

    takecommand()
```

<div align = "center">
  
# Step 3
 
## Greetings
  
</div>

</br>

```py
from datetime import datetime

time = datetime.now()
```

- We have imported `datetime` class from the `datetime` module. 
- Then, we used `now()` method to get a `datetime` object containing current date and time.

### Final Code of Step 3

```py
def wish():

    hour = int(datetime.datetime.now().hour)

    if hour >= 0 and hour < 12:

        speak("Good Morning")

    elif hour >= 12 and hour < 17:

        speak("Good Afternoon")

    else:

        speak("Good Evening")
        
if __name__ == "__main__":

    wish()
```

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

## Reservation of Bus, Train, Flight, Cab & Food

```py
Bus Reservation - webbrowser.open("https://www.makemytrip.com/bus-tickets/")

Train Reservation - webbrowser.open("https://www.makemytrip.com/railways/")
            
PNR Status - webbrowser.open("https://www.confirmtkt.com/pnr-status/" + <PNR Number> + "?")

Live Train Status - webbrowser.open("https://www.makemytrip.com/railways/liveStatus/")

Flight Reservation - webbrowser.open("https://www.makemytrip.com/flights/")

Ola Cab - webbrowser.open("https://book.olacabs.com/")

Uber Cab - webbrowser.open("https://www.uber.com/in/en/")

Zomato - webbrowser.open("https://www.zomato.com/" + <Place> + "/order-food-online")

Swiggy - webbrowser.open("https://www.swiggy.com/restaurants")

Amazon - webbrowser.open("https://www.amazon.in/%22" + <Item Name>)

Indian Hotel - webbrowser.open("https://www.goibibo.com/hotels/hotels-in-" + <Destination> +"-ct/")

International Hotel - webbrowser.open("https://www.goibibo.com/hotels-international/hotels-in-" + <Destination> + "-ct/")
```    

## Running Python Scripts

- We shall open **python scripts** present in our system using `SubProcess` Module.
- The `Subprocess` Module allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.
- The path query told by the user is stored in the file name and the cmd variable stores the file name as present in the system.
- Python subprocess Popen is used to execute a child program in a new process which can be used to run some shell commands.
- Popen creates a pipe between the calling program and the executed command, and returns a pointer to a stream that can be used to either read from or write to the pipe.

```py
query = takecommand().lower()

cmd = 'python '+ query + '.py'

p = subprocess.Popen(cmd, shell=True)

out, error = p.communicate()

print(error)

print(out)
```

- `communicate()` used to read input and the output forom the process itself.
- `communicate()` returns a tuple (stdout_data, stderr_data)
- The data will be **strings** if streams are opened in text mode, otherwise **Bytes**.

## Locating Files in the System

- Python has a cool built-in function in the OS module that is called `os.walk()`.
- To traverse the directories in Python, use the `os.walk()` function. 
- The `os.walk()` function in Python generates the file names in the file index tree by walking a tree either top-down or bottom-up. 
- For each directory in the tree rooted at the directory top, it generates a **3-tuple**, which are 
  - Directory Path
  - Directory Name
  - File Name
- By default, python will walk the directory tree in a **top-down** order ( a directory will be passed to you for the processing ), and then python will descend into any sub-directories.
- When **topdown** is **True**, the caller can modify the dirnames list in-place ( perhaps using del or slice assignment ), and `walk()` will only recurse into the subdirectories whose names remain in dirnames.
- This can be used to prune the search, impose a specific order of visiting, or even to inform `walk()` about directories the caller creates or renames before it resumes `walk()` again.
- Modifying dirnames when **topdown** is **False** is ineffective because in **bottom-up** mode, the directories in dirnames are generated before dirpath itself is generated.

```py
for Root, Dir, File in os.walk("C://"):

    print Root
    
    print Dir
    
    print File
```

- Root

    - It prints out directories only from what you specified. 
    - Meaning you need to specify the path suggesting where it should start walking and printing.

- Dir

    - It prints out sub-directories from the root.

- File 

    - It prints out all files from root and directories.

## Running a Script inside a Script

- Subprocess in Python is a module used to run new codes and applications by creating new processes. 
- It lets you start new applications right from the Python program you are currently writing. 
- So, if you want to run external programs from a git repository or codes from C or C++ programs, you can use subprocess in Python.
- You can also get exit codes and input, output, or error pipes using subprocess in Python.
- The subprocess module allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.
- `subprocess.getoutput(cmd)` returns the output (stdout and stderr) of executing cmd in a shell.
- Like `getstatusoutput()`, except the exit code is ignored and the return value is a string containing the command's output.

```py
subprocess.getoutput('ls /home')
```

## Get System Information

- The platform module in Python allows us to access the underlying platform’s data.

  - Computer network name
  - Machine type
  - Processor type
  - Platform type
  - Operating system
  - Operating system release
  - Operating system version

- Python library `platform` allows us to get the System Information.

```py
import platform
```

```py
print(f"Computer network name: {platform.node()}")

print(f"Machine type: {platform.machine()}")

print(f"Processor type: {platform.processor()}")

print(f"Platform type: {platform.platform()}")

print(f"Operating system: {platform.system()}")

print(f"Operating system release: {platform.release()}")

print(f"Operating system version: {platform.version()}")

bt = datetime.fromtimestamp(psutil.boot_time())

print(f"Boot Time: {bt.year}/{bt.month}/{bt.day} {bt.hour}:{bt.minute}:{bt.second}")
```

## Get CPU Usage

- Python library psutil allows us to get the stats of our CPU.

  - Number of physical and logical cores
  - Get CPU frequency
  - Get CPU utilization Percentage

```py
import psutil
```

- `cpu_count()` function returns number of cores.
- `cpu_freq()` function returns CPU frequency as a namedtuple including current, min, and max frequency expressed in Mhz, you can set percpu=True to get per CPU frequency.
- `cpu_percent()` method returns a float representing the current CPU utilization as a percentage, setting interval to 1 (seconds) will compare system CPU times elapsed before and after a second, we set percpu to True in order to get CPU usage of each core.

#### Number of physical and logical cores

- A logical core is the number of physical cores multiplied by the number of threads that can run on each physical core. 

```py
print(f"Number of physical cores: {psutil.cpu_count(logical=False)}")

print(f"Number of logical cores: {psutil.cpu_count(logical=True)}")
```

#### CPU frequency

```py
print(f"Current CPU frequency: {psutil.cpu_freq().current}")

print(f"Min CPU frequency: {psutil.cpu_freq().min}")

print(f"Max CPU frequency: {psutil.cpu_freq().max}")
```

#### CPU utilization Percentage

- The most interesting information is the utilization of your CPU. 
- As the processes that run on your computer change, the utilization is dynamic and changes constantly.

```py
print(f"Current CPU utilization: {psutil.cpu_percent(interval=1)}")

print("CPU Usage Per Core:")

for i, percentage in enumerate(psutil.cpu_percent(percpu=True, interval=1)):

    print(f"Core {i}: {percentage}%")
    
print(f"Total CPU Usage: {psutil.cpu_percent()}%")
```

## Memory Usage

```py
def get_size(bytes, suffix="B"):

    factor = 1024
    
    for unit in ["", "K", "M", "G", "T", "P"]:
    
        if bytes < factor:
        
            return f"{bytes:.2f}{unit}{suffix}"
            
        bytes /= factor
```

```py
svmem = psutil.virtual_memory()

print(f"Total: {get_size(svmem.total)}")

print(f"Available: {get_size(svmem.available)}")

print(f"Used: {get_size(svmem.used)}")

print(f"Percentage: {svmem.percent}%")
```

- `virtual_memory()` method returns stats about system memory usage as a namedtuple, including fields such as total (total physical memory available), available (available memory, i.e not used), used and percent (i.e percentage). 
- `get_size()` function prints values in a scaled manner, as these statistics are expressed in bytes.

```py
swap = psutil.swap_memory()

print(f"Total: {get_size(swap.total)}")

print(f"Free: {get_size(swap.free)}")

print(f"Used: {get_size(swap.used)}")

print(f"Percentage: {swap.percent}%")
```

- Swap space is a space on a hard disk that is a substitute for physical memory whenever our computer runs short of physical memory.
- Swap space helps the computer’s operating system in pretending that it has more RAM than it actually has. 
- Virtual memory is a combination of RAM and disk space that running processes can use. 
- Swap space is the portion of virtual memory that is on the hard disk, used when RAM is full. 
- `swap_memory()` method returns stats about swap memory usage.

## Disk Usage

```py
partitions = psutil.disk_partitions()

for partition in partitions:

    print(f"Device : {partition.device}")
    
    print(f"Mountpoint : {partition.mountpoint}")
    
    print(f"File system type : {partition.fstype}")
    
    try:
    
        partition_usage = psutil.disk_usage(partition.mountpoint)
    
    except PermissionError:

        continue
        
    print(f"Total Size : {get_size(partition_usage.total)}")
    
    print(f"Used : {get_size(partition_usage.used)}")
    
    print(f"Free : {get_size(partition_usage.free)}")
    
    print(f"Percentage : {partition_usage.percent}%")

disk_io = psutil.disk_io_counters()

print(f"Total read : {get_size(disk_io.read_bytes)}")

print(f"Total write : {get_size(disk_io.write_bytes)}")
```

- `disk_usage()` function return disk usage statistics as a namedtuple, including total, used and free space expressed in bytes.

## Network Stats

```py
if_addrs = psutil.net_if_addrs()

for interface_name, interface_addresses in if_addrs.items():

    for address in interface_addresses:
    
        print(f"=== Interface: {interface_name} ===")
        
        if str(address.family) == 'AddressFamily.AF_INET':
        
            print(f"  IP Address: {address.address}")
            
            print(f"  Netmask: {address.netmask}")
            
            print(f"  Broadcast IP: {address.broadcast}")
            
        elif str(address.family) == 'AddressFamily.AF_PACKET':
        
            print(f"  MAC Address: {address.address}")
            
            print(f"  Netmask: {address.netmask}")
            
            print(f"  Broadcast MAC: {address.broadcast}")
            
net_io = psutil.net_io_counters()

print(f"Total Bytes Sent: {get_size(net_io.bytes_sent)}")

print(f"Total Bytes Received: {get_size(net_io.bytes_recv)}")
```

- `net_if_addrs()` function returns the addresses associated with each network interface card installed on the system.
