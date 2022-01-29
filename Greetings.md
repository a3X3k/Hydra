<div align = "center">
  
# Step 3
 
## Greetings
  
</div>

</br>

```py
from datetime import datetime

time = datetime.now()
```

- We have imported `datetime` class from the `datetime` module. 
- Then, we used `now()` method to get a `datetime` object containing current date and time.

### Final Code of Step 3

```py
def wish():

    hour = int(datetime.datetime.now().hour)

    if hour >= 0 and hour < 12:

        speak("Good Morning")

    elif hour >= 12 and hour < 17:

        speak("Good Afternoon")

    else:

        speak("Good Evening")
        
if __name__ == "__main__":

    wish()
```
