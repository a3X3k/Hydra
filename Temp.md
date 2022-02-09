```py
#____________________Send Messages on Discord Server_______

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
