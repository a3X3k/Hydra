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

- This will install the `pyttsx3` library. 

### Text-To-Speech using Pyttsx3

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










