<div align = "center">
  
# Step 4
 
## Open Files 
  
</div>

</br>

## Open Apps

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

## Open Command Prompt

```
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

```
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






