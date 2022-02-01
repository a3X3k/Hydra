```py
from curses import window
from email.message import Message
import pyttsx3
import speech_recognition as sr
import datetime
import os
import cv2
import random
import socket
import wikipedia
import webbrowser
import wolframalpha
import pywhatkit as kit
import smtplib
import yagmail
import pyautogui
import time
import pygetwindow as gw

engine = pyttsx3.init()

voices = engine.getProperty('voices')

engine.setProperty('voice', voices[1].id)

engine.setProperty('rate', 200)


emails = {

    "abhishek outlook": "abhishekabi2002@outlook.com",
}

def computational_intelligence(question):
    try:
        client = wolframalpha.Client(app_id)
        answer = client.query(question)
        answer = next(answer.results).text
        print(answer)
        return answer
    except:
        speak("Sorry sir I couldn't fetch your question's answer. Please try again ")
        return None




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

        speak("\nSay that again please")
        return "Nothing"

    except sr.UnknownValueError:

        print("\nCould not understand audio")
        return "Nothing"

    except sr.RequestError as e:

        print("\nCould not request results; {0}".format(e))
        return "Nothing"

    return query


def wish():

    hour = int(datetime.datetime.now().hour)

    if hour >= 0 and hour < 12:

        speak("Good Morning Sir")

    elif hour >= 12 and hour < 17:

        speak("Good Afternoon Sir")

    else:

        speak("Good Evening Sir")


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


def Wikipedia():

    speak("\nWhat do you want to search for in Wikipedia Sir?")

    query = takecommand().lower()

    if query != "nothing":

        speak("\nSearching in Wikipedia")

        summary = wikipedia.summary(query, sentences = 2)

        speak("\nAccording to Wikipedia, " + summary)


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


def Email():

    speak("\nTo whom do you want to send the mail Sir?")

    Mail_ID = takecommand().lower()

    if Mail_ID not in emails:

        speak("\nSorry Sir! The Recipient's Mail ID is not there in the Database.")

        speak("\nDo you want to add details to the Database Sir?")

        if "yes" in takecommand().lower():

            speak("\nPlease type the Recipient's Name Sir. Remember that the same name has to be used for future references.")

            name = input()

            speak("\nPlease type the Mail ID Sir.")

            ID = input()

            emails[name] = ID

            speak("\nInformation has been updated Sir. Please try again to send the Email.")
                
    else:

        server = smtplib.SMTP_SSL('smtp.gmail.com', 465)

        speak("\nWhat do you want to send Sir?")

        Message = takecommand()

        speak("\nDo you want to include any attachments Sir?")

        if "yes" in takecommand().lower():

            yag = yagmail.SMTP('x@gmail.com', 'xyz')

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
                    
            server.login('x@gmail.com', 'xyz')

            server.sendmail('x@gmail.com', emails[Mail_ID], Message)

            speak("\nMail has been sent successfully Sir!")

            server.quit()


def Switch_Window():

    a = gw.getAllTitles()

    a = [i for i in a if i]

    window = []

    [window.append(x) for x in a if x not in window]

    system_apps = ["Settings", "Microsoft Text Input Application", "Program Manager"]
 
    window = [i for i in window if i not in system_apps]

    return window


if __name__ == "__main__":

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

        elif "close web browser" in query:

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

            wikipedia()

        
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

        
        elif "send email" in query:

            Email()

        
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
        

        elif "quit" in query:

            speak("\nDo you really wanna quit Sir?")

            if "yes" in takecommand().lower():

                speak("\nThankyou for using me Sir!")

                break

            else:

                continue

        else:

            time.sleep(10)
```
