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
