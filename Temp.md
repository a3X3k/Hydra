```py
#____________________Send Messages on Discord Server___________________________________________________________________________________________________________

def Discord(): #conda install -c anaconda requests install before running
    #https://discord.com/api/v9/channels/938752936232763404/messages
    query = takecommand().lower()
    payload =  {
        "content" : query
    }

    header = {
        'authorization': 'NzU0MDQ1MTkwOTI2MzY4ODQ4.YYDTig.4HIzVR5OHwqH0l4YWRI8q7GEEWY'
    }
    r = requests.post("https://discord.com/api/v9/channels/938752936232763404/messages", data=payload,headers = header)
    
  #_____________________________________________________________python______________________________________________________

def piii():

    query = takecommand().lower()
    
    cmd = 'python '+query+'.py'
    
    p = subprocess.Popen(cmd,shell=True)

    out,error = p.communicate()

    print(error)

    print(out)


#_______________________________________________________Hotel Booking___________________________________________________________



def hotel():
    
    speak("would You Like to Book Hotels In India or International")

    query = takecommand().lower()

    if query == "india":

        speak("where do you wish to travel")

        destt = takecommand().lower()

        webbrowser.open("https://www.goibibo.com/hotels/hotels-in-"+destt+"-ct/")

    elif query == "international":

        speak("where do you wish to travel")

        dest1 = takecommand().lower()

        webbrowser.open("https://www.goibibo.com/hotels-international/hotels-in-"+dest1+"-ct/")
        
#______________________________________________________________________________________________________________________________

    def movie():

    speak("Where Would You like to Watch Movie ")

    query3 = takecommand().lower()

    speak("Enjoy Your Movie")

    webbrowser.open("https://in.bookmyshow.com/explore/home/"+query3)
```
