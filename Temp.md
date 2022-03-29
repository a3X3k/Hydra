```py
def Discord(): 

#conda install -c anaconda requests install before running
#https://discord.com/api/v9/channels/938752936232763404/messages

    query = takecommand().lower()
    
    payload =  {
        "content" : query
    }

    header = {
        'authorization': 'NzU0MDQ1MTkwOTI2MzY4ODQ4.YYDTig.4HIzVR5OHwqH0l4YWRI8q7GEEWY'
    }
    
    r = requests.post("https://discord.com/api/v9/channels/938752936232763404/messages", data=payload,headers = header)
```
   
```py
Battery_percent = psutil.sensors_battery().percent
```

```py
Speak("Do you want to shutdown your computer sir?")
while True:
    command = take_commands()
    if "no" in command:
        Speak("Thank u sir I will not shut down the computer")
        break
    if "yes" in command:
        # Shutting down
        Speak("Shutting the computer")
        os.system("shutdown /s /t 30")
        break
    Speak("Say that again sir")
```
