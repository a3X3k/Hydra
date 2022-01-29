<div align = "center">
  
# Step 4
 
## Open Files 
  
</div>

</br>

```
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
