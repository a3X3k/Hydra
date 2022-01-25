<a href="https://github.com/404"><img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%"></a>

<div align = "center">

# [Hydra](#)
  
</div>
  
<a href="https://github.com/404"><img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%"></a>

# Step 1 

### Installing Pyttsx3 using pip

```py
pip install pyttsx3
```

- This will install the `pyttsx3` library in your machine or the virtual environment if you are using it.

### Text-To-Speech using Pyttsx3

- Import the `pyttsx3` package that we’ve installed using the pip. 

```py
import pyttsx3
```

- Next step is to initialize the pyttsx3 package. 
- The Instance of the initialized pyttsx3 package is stored in the engine variable. 
- We are calling the variable engine as it works as the engine and converts Text-To-Speech whenever execute the functions from the package.

```py
engine = pyttsx3.init()
```

- There is a built-in `say()` function in the pyttsx3 package that takes a string value and speaks it out.

```py
engine.say("Hello")
```

- `runAndWait()` function keeps track when the engine starts converting text to speech and waits for that much time, and do not allow the engine to close. 
- If we don’t write this code, it may happen that the engine might not work properly as the processes will not be synchronized.

```py
engine.runAndWait()
```

- After all the processes are over, we shut down the engine by calling the stop() function.

```py
engine.stop()
```










