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
def convert_size(size_bytes):
   if size_bytes == 0:
       return "0B"
   size_name = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
   i = int(math.floor(math.log(size_bytes, 1024)))
   p = math.pow(1024, i)
   s = round(size_bytes / p, 2)
   print("%s %s" % (s, size_name[i]))
   return "%s %s" % (s, size_name[i])
```

   
```py
def system_stats():
    cpu_stats = str(psutil.cpu_percent())
    battery_percent = psutil.sensors_battery().percent
    memory_in_use = convert_size(psutil.virtual_memory().used)
    total_memory = convert_size(psutil.virtual_memory().total)
    final_res = f"Currently {cpu_stats} percent of CPU, {memory_in_use} of RAM out of total {total_memory}  is being used and battery level is at {battery_percent} percent"
    return final_res
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
