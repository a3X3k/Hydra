<a href="https://github.com/404"><img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%"></a>

<div align = "center">

# [Hydra](#)
  
</div>
  
<a href="https://github.com/404"><img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%"></a>

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




