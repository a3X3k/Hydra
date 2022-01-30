```py
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

engine = pyttsx3.init()

voices = engine.getProperty('voices')

engine.setProperty('voice', voices[1].id)

engine.setProperty('rate', 200)

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
        audio = r.listen(source, timeout = 5, phrase_time_limit = 8)

    try:
        print("\nRecognizing... ")
        query = r.recognize_google(audio, language = 'en-in')
        print("\nUser said :", query)

    except Exception as e:

        speak("Say that again please")
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


if __name__ == "__main__":

    wish()

    query = takecommand().lower()

    if 1:

        if "open notepad" in query:

            os.startfile("C:\\Windows\\system32\\notepad.exe")


        elif "open web browser" in query:

            os.startfile("C:\\Program Files\\BraveSoftware\\Brave-Browser-Beta\\Application\\brave.exe")

        
        elif "open command prompt" in query:

            os.system("start cmd") 

        
        elif "open camera" in query:

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

            speak("\nWhat do you want to search for in Wikipedia Sir?")

            query = takecommand().lower()

            if query != "nothing":

                speak("\nSearching in Wikipedia")

                summary = wikipedia.summary(query, sentences = 2)

                speak("\nAccording to Wikipedia, " + summary)

        
        elif "open" and "youtube" in query:

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


        elif "whatsapp" in query:

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
```

