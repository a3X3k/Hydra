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
