```py
from curses import window
from email.message import Message
import sys
from tkinter import Y
import pyttsx3
import speech_recognition as sr
import datetime
import os
import cv2
import random
import socket
import wikipedia
import webbrowser
import pywhatkit as kit
import smtplib
import yagmail
import pyautogui
import time
import pygetwindow as gw
import subprocess
import win32api
from PyQt5 import QtWidgets, QtCore, QtGui
from PyQt5.QtCore import QTimer, QTime, QDate, Qt
from PyQt5.QtGui import QMovie
from PyQt5.QtCore import *
from PyQt5.QtGui import *
from PyQt5.QtWidgets import *
from PyQt5.uic import loadUiType
from JarvisUI import Ui_JarvisUI

engine = pyttsx3.init()

voices = engine.getProperty('voices')

engine.setProperty('voice', voices[1].id)

engine.setProperty('rate', 175)


def speak(audio):

    print(audio)
    engine.say(audio)
    engine.runAndWait()


def takecommand():

    r = sr.Recognizer()

    with sr.Microphone() as source:    

        r.adjust_for_ambient_noise(source)     

        print("\nListening... ") 
        r.pause_threshold = 1
        audio = r.listen(source, timeout = 8, phrase_time_limit = 10)

    try:
        print("\nRecognizing... ")
        query = r.recognize_google(audio, language = 'en-in')
        print("\nUser said :", query)

    except Exception as e:

        return "Nothing"

    except sr.UnknownValueError:

        print("\nCould not understand audio")
        return "Nothing"

    except sr.RequestError as e:

        print("\nCould not request results; {0}".format(e))
        return "Nothing"

    return query


def date():

    try:

        date = datetime.datetime.now().strftime("%b %d %Y")

    except Exception as e:

        print(e)

    return date


def time():

    try:

        time = datetime.datetime.now().strftime("%H:%M:%S")

    except Exception as e:

        print(e)
        
    return time


def wish():

    hour = int(datetime.datetime.now().hour)

    if hour >= 0 and hour < 12:

        speak("\nHellow, this is Hydra! Good Morning...")

    elif hour >= 12 and hour < 17:

        speak("\nHellow, this is Hydra! Good Afternoon...")

    else:

        speak("\nHellow, this is Hydra! Good Evening...")

        speak(f"\nCurrently its {time()}")


emails = {

    "abhishek outlook": "abhishekabi2002@outlook.com",
    "abhishek gmail": "shek1harley@gmail.com",
}


def Mail():

    speak("\nTo whom do you want to send the mail Sir?")

    Mail_ID = takecommand().lower()

    if Mail_ID not in emails:

        speak("\nSorry Sir! The Recipient's Mail ID is not there in the Database.")

        speak("\nDo you want to add details to the Database Sir?")

        if "yes" in takecommand().lower():

            speak("\nPlease tell the Recipient's Name Sir. Remember that the same name has to be used for future references...")

            name = takecommand().lower()

            speak("\nPlease spell the domain name before @ Sir...")

            ID = takecommand().lower()

            speak("\nWhich Email provider does this ID belongs to Sir?")

            provider = takecommand().lower()

            emailID = ID.replace(" ","") + "@" + provider + ".com"

            emails[name] = emailID

            speak("\nInformation has been updated Sir. Please try again to send the Email...")
                
    else:

        server = smtplib.SMTP_SSL('smtp.gmail.com', 465)

        speak("\nWhat do you want to send Sir?")

        Message = takecommand()

        speak("\nDo you want to include any attachments Sir?")

        if "yes" in takecommand().lower():

            yag = yagmail.SMTP('abhishekabi2002@gmail.com', '')

            contents = [Message]

            speak("\nPlease provide the full path of the attachment Sir and also make sure that you use the forward slash as a file separator and not the backward slash.")

            path = input()

            contents.append(path)

            speak("\nWhat should be the Subject of the Mail Sir?")

            subject = takecommand()

            yag.send(emails[Mail_ID], subject, contents)

            speak("\nMail has been sent successfully Sir!")

            yag.quit()
                
        else:
                    
            server.login('abhishekabi2002@gmail.com', '')

            server.sendmail('abhishekabi2002@gmail.com', emails[Mail_ID], Message)

            speak("\nMail has been sent successfully Sir!")

            server.quit()


Formats = ['Image', 'Audio', 'Video', 'Programming', 'Word', 'Presentation', 'Spreadsheet', 'Compression', 'Executable', 'Disc', 'Database', 'Email']

Image = ['.jpeg', '.jpg', '.png', '.gif', '.bmp', '.ico', '.ai', '.ps', '.psd', '.svg', '.tif', '.tiff']

Audio = ['.mp3',  '.wav', '.aif', '.ogg',  '.wma',  '.wpl',  '.cda', '.mpa', '.mid',  '.midi']

Video = ['.mp4', '.mov', '.mkv', '.mpg', '.mpeg', '.wmv', '.3g2' , '.3gp', '.avi', '.flv', '.h264', '.m4v', '.rm', '.swf', '.vob']

Programming = ['.py', '.c', '.cpp', '.class', '.cs', '.h', '.java', '.sh', '.swift', '.vb', '.java','.html', 'htm', '.css', '.js', '.jsp',  '.php', '.part', '.rss', '.xhtml', '.cgi', '.pl', '.cfm', '.cer', '.asp', '.aspx']

Word = ['.doc', '.docx', '.pdf', '.txt', '.odt', '.rtf', '.tex', '.wpd']

Presentation = ['.ppt', '.pptx', '.pps', '.odp', '.key']

Spreadsheet = ['.xls', '.xlsx', '.xlsm', '.ods']

Compression = ['.zip', '.7z', '.rar', '.arj', '.deb', '.pkg', '.rpm', '.z']

Executable = ['.apk', '.bat', '.bin', '.cgi', '.com', '.exe', '.gadget', '.jar', '.msi', '.wsf']

Disc = ['.bin', '.iso', '.dmg', '.toast', '.vcd']

Database = ['.csv', '.dat', '.tar', '.xml', '.db', '.dbf', '.log', '.mdb', '.sav', '.sql']

Email = ['.vcf', '.email', '.eml', '.emlx', '.msg', '.oft', '.ost', '.pst', '.vcf']


def Directory():

    drives = win32api.GetLogicalDriveStrings()

    return drives.split('\000')[:-1]


def Extension(List):

    speak("\nPlease select the file format from this Sir...")

    for i in List:

        speak(f"\n{i}")

        speak("\nIs this your file format Sir...")

        query = takecommand().lower()

        if "yes" in query:

            return i


def Category(List):

    if List == "Audio":

        return Extension(Audio)

    elif List == "Image":

        return Extension(Image)

    elif List == "Video":

        return Extension(Video)

    elif List == "Programming":

        return Extension(Programming)

    elif List == "Word":

        return Extension(Word)

    elif List == "Presentation":

        return Extension(Presentation)

    elif List == "Spreadsheet":

        return Extension(Spreadsheet)

    elif List == "Compression":

        return Extension(Compression)

    elif List == "Executable":

        return Extension(Executable)

    elif List == "Disc":

        return Extension(Disc)

    elif List == "Database":

        return Extension(Database)

    elif List == "Email":

        return Extension(Email)
 

def Locate():

    Dir = Directory()

    speak("\nPlease tell the name of the file without extension Sir!")

    fname = takecommand().lower()

    speak("\nDo you know the extension of the file Sir?")

    query = takecommand().lower()

    fileformat = ""
        
    if "yes" in query:

        speak("\nAlright... There are hundreds of different file extensions and file types available and it would be easy for me if you select the right file type Sir.")

        speak("\nPlease tell me if your file comes under these categories...")

        f_format = ""

        for i in Formats:

            speak(f"\n{i}")

            speak("\nDoes your file comes under this category Sir?")

            query = takecommand().lower()
            
            if "yes" in query:

                f_format = Category(i) 

                break

        file_name = fname + f_format

        speak(f"\nIs this the file you want to Search Sir? - {file_name}")

        query = takecommand().lower()

        if "yes" in query:

            speak("\nSearching for your file Sir. This may take a while...")

            for i in Dir:

                temp = i.replace("\\", "").replace(":", "")

                speak(f"\nStart Searching in {temp} Drive...")

                c = 1

                for r, d, f in os.walk(i):

                    for file in f:

                        if file_name in file:

                            speak(f"\nFile {c} - {os.path.join(r, file)}")

                            c += 1

        else:

            Locate()

    else:

        speak("\nSearching for your file Sir. This may take a while...")

        for i in Dir:

            for r, d, f in os.walk(i):

                for file in f:

                    if fname + type in file:

                        speak(os.path.join(r, file))


def Camera():

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


def Wiki():

    speak("\nWhat do you want to search for in Wikipedia Sir?")

    query = takecommand().lower()

    if query != "nothing":

        speak("\nSearching in Wikipedia")

        summary = wikipedia.summary(query, sentences = 2)

        speak("\nAccording to Wikipedia, " + summary)

    else:

        speak("\nOh no, I didn't get proper query Sir. Redirecting you to Hydra's Features...")


def YouTube_Songs():

    speak("\nWhich song do you want me to play Sir?")

    song = takecommand()

    song = song.replace("play", "")

    speak("\nHere you go....")

    kit.playonyt(song)


def Google_Search():

    speak("\nWhat do I need to search on Google Sir?")

    query = takecommand().lower()

    if "tell me about" in query:

        query = query.replace("tell me about", "")

        print(query)

        summary = wikipedia.summary(query, sentences = 2)

        speak("\nAccording to Wikipedia, " + summary)

    elif query != "nothing":
                
        speak("\nSearching on Google Sir")

        query = query.replace("search for", "")

        webbrowser.open("https://www.google.com/search?q=" + query)

    else:

        speak("\nOh no, I didn't get proper query Sir. Redirecting you to Hydra's Features...")


def Whatsapp():

    speak("\nPlease tell the number to which you wish to message Sir")

    num = takecommand()

    num = "+91" + num

    num = num.replace(" ", "")

    speak("\nPlease tell your message Sir")

    message = takecommand().lower()

    speak("\nWhen do you want to send a message Sir? Please tell me some time after 4 minutes from now!")

    speak("\nFor Example, you can tell as 5")

    time = takecommand().lower()

    hour = datetime.datetime.now().hour

    minutes = datetime.datetime.now().minute

    kit.sendwhatmsg(num, message, hour, minutes + int(time))


def Switch_Window():

    a = gw.getAllTitles()

    a = [i for i in a if i]

    window = []

    [window.append(x) for x in a if x not in window]

    system_apps = ["Settings", "Microsoft Text Input Application", "Program Manager"]
 
    window = [i for i in window if i not in system_apps]

    return window


def Navigate():
	
    speak("\nWhere do you wish to navigate Sir?")
	
    query = takecommand().lower()
	
    query = query.replace("navigate to","")
		
    speak(f"Opening the Navigator to{query} Sir.")
		
    webbrowser.open('https://www.google.com/maps/place/' + query)


def Play_Movie():

    speak("\nWhich OTT Platform do you want me to open Sir? Is it Netflix or Prime or Hotstar?")
	
    query = takecommand().lower()

    if "prime" in query:

        speak("\nOpening Amazon Prime Video...")

        webbrowser.open("https://www.primevideo.com/")

    elif "netflix" in query:

        speak("\nOpening Amazon Netflix...")

        webbrowser.open("https://www.netflix.com/in/")

    elif "hotstar" in query:

        speak("\nOpening Hotstar...")

        webbrowser.open("https://www.hotstar.com/in")
    
    else:

        speak("\nOh no, I didn't get proper query Sir. Redirecting you to Hydra's Features...")


def Amazon():

    speak("\nOpening Amazon Sir...")

    webbrowser.open("https://www.amazon.in/") 


def Food():

    speak("\nWhere would you like to order Sir? Zomato or Swiggy. Don't forget to make sure that food delivery is available in your area.")

    query = takecommand().lower()

    if "zomato" in query:

        speak("\nWhere do you live Sir?")

        place = takecommand().lower()

        speak(f"\nSearching for restaurants in {place} Sir...")

        webbrowser.open("https://www.zomato.com/"+ place +"/order-food-online")

    elif "swiggy" in query:

        speak("\nSearching for restaurants Sir...")

        webbrowser.open("https://www.swiggy.com/restaurants")

    else:

        speak("\nOh no, I didn't get proper query Sir. Redirecting you to Hydra's Features...")


def Book_Movie():

    speak("\nWhich city are you in Sir? Kindly Make sure that Book My Show is available in your City!")

    query = takecommand().lower()

    speak(f"\nSearching for movies in {query} Sir. Enjoy Your Movie... Have fun...")

    webbrowser.open("https://in.bookmyshow.com/explore/home/"+ query)


def Plan_My_Trip():
    
    speak("\nAlright... What do you want me to look for Sir? Cab, Hotels, Bus, Train or Flight?")

    query = takecommand().lower()

    if "cab" in query:
        
        speak("\nOla or Uber Sir?")

        query = takecommand().lower()

        if "ola" in query:

            speak("\nRedirecting you to Ola Booking Page... Have a safe Journey Sir...")

            webbrowser.open("https://book.olacabs.com/")

        elif "uber" in query:

            speak("\nRedirecting you to Uber Booking Page... Have a safe Journey Sir...")

            webbrowser.open("https://www.uber.com/in/en/")
        
        else:

            speak("\nOh no, I didn't get proper query Sir. Redirecting you to Hydra's Features...")

    elif "train" in query:
        
        speak("\nDo you want me to Check PNR status or Check Live train status or Book Train ticket Sir?")
        
        query = takecommand().lower()

        if "book" in query:
            
            speak("\nRedirecting you to Train Booking Page... Have a safe Journey Sir...")

            webbrowser.open("https://www.makemytrip.com/railways/")
            
        elif "pnr" in query:

            speak("\nWhat is your PNR Number Sir?")

            query = takecommand()
            
            speak("\nRedirecting you to PNR Status Page Sir...")

            query = query.replace(" ", "")

            webbrowser.open("https://www.confirmtkt.com/pnr-status/"+ query + "?")

        elif "live" in query:

            speak("\nRedirecting you to Live Train Status Page Sir...")

            webbrowser.open("https://www.makemytrip.com/railways/liveStatus/")

        else:

            speak("\nOh no, I didn't get proper query Sir. Redirecting you to Hydra's Features...")
            
    elif query == "bus":

        speak("\nRedirecting you to Bus Booking Page... Have a safe Journey Sir...")

        webbrowser.open("https://www.makemytrip.com/bus-tickets/")
        
        
    elif query == "flight":

        speak("\nRedirecting you to Flight Booking Page... Have a safe Journey Sir...")

        webbrowser.open("https://www.makemytrip.com/flights/")

    elif "hotel" in query:

        speak("\nDo you want me to look for Indian Hotels or International Hotels Sir?")

        query = takecommand().lower()

        if "india" in query :

            speak("\nTell me the place where you want me to look for hotels Sir!")

            query = takecommand().lower()

            speak("\nRedirecting you to Booking Page Sir...")

            webbrowser.open("https://www.goibibo.com/hotels/hotels-in-" + query + "-ct/")

        elif "international" in query:

            speak("\nTell me the place where you want me to look for hotels Sir!")

            query = takecommand().lower()

            speak("\nRedirecting you to Booking Page Sir...")

            webbrowser.open("https://www.goibibo.com/hotels-international/hotels-in-" + query + "-ct/")

        else:

            speak("\nOh no, I didn't get proper query Sir. Redirecting you to Hydra's Features...")

    else:

        speak("\nOh no, I didn't get proper query Sir. Redirecting you to Hydra's Features...")


def News():

    from gnewsclient import gnewsclient

    client = gnewsclient.NewsClient(language = 'english')

    speak("\nThese are the categories available Sir!")
 
    speak(client.topics)

    speak("\nWhich category of news are you interested in Sir?")

    choice = takecommand().lower()

    if "top" in choice:

        speak("\nAlright, here is the Top Stories Sir!")

        client = gnewsclient.NewsClient(language = 'english', max_results = 5)

        news_list = client.get_news()
 
        for item in news_list:

            speak(item['title'])

        speak("\nThat's it Sir!")


    elif "world" in choice:

        speak("\nAlright, here is the World News Sir!")

        client = gnewsclient.NewsClient(language = 'english', location='india', topic = 'World', max_results = 5)
 
        for item in client.get_news():

            speak(item['title'])

        speak("\nThat's it Sir!")


    elif "nation" in choice:

        speak("\nAlright, here is the Nation News Sir!")

        client = gnewsclient.NewsClient(language = 'english', location='india', topic = 'Nation', max_results = 5)
 
        for item in client.get_news():

            speak(item['title'])

        speak("\nThat's it Sir!")

            
    elif "business" in choice:

        speak("\nAlright, here is the Business News Sir!")

        client = gnewsclient.NewsClient(language = 'english', location='india', topic = 'Business', max_results = 5)
 
        for item in client.get_news():

            speak(item['title'])

        speak("\nThat's it Sir!")

            
    elif "technology" in choice:

        speak("\nAlright, here is the Technology News Sir!")

        client = gnewsclient.NewsClient(language = 'english', location='india', topic = 'Technology', max_results = 5)
 
        for item in client.get_news():

            speak(item['title'])

        speak("\nThat's it Sir!")

            
    elif "entertainment" in choice:

        speak("\nAlright, here is the Entertainment News Sir!")

        client = gnewsclient.NewsClient(language = 'english', location='india', topic = 'Entertainment', max_results = 5)
 
        for item in client.get_news():

            speak(item['title'])

        speak("\nThat's it Sir!")


    elif "sports" in choice:

        speak("\nAlright, here is the Sports News Sir!")

        client = gnewsclient.NewsClient(language = 'english', location='india', topic = 'Sports', max_results = 5)
 
        for item in client.get_news():

            speak(item['title'])

        speak("\nThat's it Sir!")


    elif "science" in choice:

        speak("\nAlright, here is the Science News Sir!")

        client = gnewsclient.NewsClient(language = 'english', location='india', topic = 'Science', max_results = 5)
 
        for item in client.get_news():

            speak(item['title'])

        speak("\nThat's it Sir!")


    elif "health" in choice:

        speak("\nAlright, here is the Health News Sir!")

        client = gnewsclient.NewsClient(language = 'english', location='india', topic = 'Health', max_results = 5)
 
        for item in client.get_news():

            speak(item['title'])

        speak("\nThat's it Sir!")

    else:

        speak("\nOh No, there is no such category. So I am telling you today's top headlines Sir!")

        client = gnewsclient.NewsClient(language = 'english', max_results = 5)

        news_list = client.get_news()
 
        for item in news_list:

            speak(item['title'])

        speak("\nThat's it Sir!")

            
    speak("\nDo you want to read all these News in brief? I can do it for you Sir. Please tell me Yes or No.")

    y_or_n = takecommand().lower()

    if "yes" in y_or_n:

        speak("\nRedirecting you to the Source, have a good read Sir.")

        for item in client.get_news():
                    
            webbrowser.open(item['link'])


def Script():

    speak("\nIs the file present in this directory Sir?")

    query = takecommand().lower()

    if "yes" in query:

        speak("\nTell the file name Sir...")

        speak(f"\nThe output is {subprocess.getoutput('python '+ takecommand() +'.py')}")

    else:

        speak("\nPlease tell the file name Sir...")

        fname = takecommand().lower()

        fname = fname + ".py"
       
        Dir = Directory()

        speak("\nSearching for your file Sir. This may take a while...")

        for i in Dir:

            temp = i.replace("\\", "").replace(":", "")

            speak(f"\nStart Searching in {temp} Drive...")

            for r, d, f in os.walk(i):

                for file in f:

                    if fname in file:

                        speak(f"\n{os.path.join(r, file)}")

                        speak("\nIs this the file you wanna run Sir?")

                        query = takecommand().lower()

                        if "yes" in query:

                            target = '"' + os.path.join(r, file) + '"'

                            speak(f"\nThe output is {subprocess.getoutput('python '+ target)}")

class MainThread(QThread):

    def __init__(self):

        super(MainThread, self).__init__()

    def run(self):

        self.TaskExecution()


    def TaskExecution(self):

        wish()

        speak("\nWhat can I do for you Sir?")

        while(1):

            query = takecommand().lower()

            if "nothing" in query:

                continue

            elif "open notepad" in query:

                os.system("start notepad.exe")

            elif "close notepad" in query:

                os.system("taskkill /im notepad.exe /f")

            elif "open web browser" in query:

                os.system("start brave.exe")

            elif "close" and "browser" in query:

                os.system("taskkill /im brave.exe /f")

            elif "open command prompt" in query:

                os.system("start cmd") 

            elif "close command prompt" in query:

                os.system("taskkill /im cmd.exe /f")

            
            elif "open camera" in query:

                Camera()

            
            elif "play music" in query: 

                music_directory = "F:\Songs" 

                songs = os.listdir(music_directory)

                os.startfile(os.path.join(music_directory, random.choice(songs)))

            
            elif "ip " in query: 

                host = socket.gethostname()

                IP = socket.gethostbyname(host)

                speak("Your Host Name is : " + host)

                speak("Your Computer IP Address is : " + IP)

            
            elif "wikipedia" in query:

                Wiki()

            
            elif "open youtube" in query:

                speak("\nOpening Youtube Sir...")

                webbrowser.open("www.youtube.com")

            
            elif "open" and "facebook" in query:

                speak("\nOpening Facebook Sir...")

                webbrowser.open("www.facebook.com")

            
            elif "open" and "instagram" in query:

                speak("\nOpening Instagram Sir...")

                webbrowser.open("www.instagram.com")

            
            elif "open" and "linkedin" in query:

                speak("\nOpening LinkedIn Sir...")

                webbrowser.open("www.linkedin.com")

            
            elif "open" and "twitter" in query:

                speak("\nOpening Twitter Sir...")

                webbrowser.open("www.twitter.com")

            
            elif "open" and "instagram" in query:

                speak("\nOpening Twitter Sir...")

                webbrowser.open("www.twitter.com")

            
            elif "search" and "google" in query:

                Google_Search()


            elif "whatsapp" in query:

                Whatsapp()


            elif "songs" and "youtube" in query:

                YouTube_Songs()

            
            elif "send" and "mail" in query:

                Mail()

            
            elif "switch" in query:

                window = Switch_Window()

                speak(f"\nThere are totally {len(window)} windows open Sir!")

                k = 0

                for i in window:

                    speak(f"\nWindow {k + 1} : {window[k]}") 

                    k += 1

                speak("\nPlease tell the window name which you want me to Open Sir!")

                window_to_open = takecommand().lower()

                win_num = 0

                window = Switch_Window()

                pyautogui.keyDown("alt")

                for i in range(len(window)):

                    if window_to_open in window[i].lower():

                        break

                    else: 

                        pyautogui.press("tab")

                time.sleep(1)

                pyautogui.keyUp("alt")


            elif "navigate" in query:

                Navigate()


            elif "news" in query:

                News()


            elif "play movie" in query:

                Play_Movie()


            elif "amazon" in query:

                Amazon()

            
            elif "food" in query:

                Food()

            
            elif "book" and "movie" in query:

                Book_Movie()


            elif "plan my trip" in query:

                Plan_My_Trip()


            elif "locate" in query:

                Locate()


            elif "python" in query:

                Script()

            
            elif "quit" in query:

                speak("\nDo you really wanna quit Sir?")

                if "yes" in takecommand().lower():

                    speak("\nThankyou for using me Sir!")

                    break

                else:

                    continue


startExecution = MainThread()

class Main(QMainWindow):

    def __init__(self):

        super().__init__()

        self.ui = Ui_JarvisUI()

        self.ui.setupUi(self)

        self.ui.pushButton.clicked.connect(self.startTask)

        self.ui.pushButton_2.clicked.connect(self.close)

    def startTask(self):

        self.ui.movie = QtGui.QMovie("Source/0.gif")

        self.ui.label.setMovie(self.ui.movie)

        self.ui.movie.start()

        self.ui.movie = QtGui.QMovie("Source/1.gif")

        self.ui.label_2.setMovie(self.ui.movie)

        self.ui.movie.start()

        self.ui.movie = QtGui.QMovie("Source/2.gif")

        self.ui.label_3.setMovie(self.ui.movie)

        self.ui.movie.start()

        self.ui.movie = QtGui.QMovie("Source/3.gif")

        self.ui.label_4.setMovie(self.ui.movie)

        self.ui.movie.start()

        self.ui.movie = QtGui.QMovie("Source/3.gif")

        self.ui.label_5.setMovie(self.ui.movie)

        self.ui.movie.start()

        timer = QTimer(self)

        timer.start(1000)

        startExecution.start()

app = QApplication(sys.argv)

jarvis = Main()

jarvis.show()

exit(app.exec_())
```
