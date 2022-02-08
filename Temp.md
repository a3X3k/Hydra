```py
def Prime():
    speak("Which movie do you wish to watch Sir?")

    query = takecommand().lower()
    query.replace(" ","+")
    print("Ok Sir, Opening Prime Video and Searching for",query)
    webbrowser.open("https://www.primevideo.com/search/ref=atv_nb_sr?phrase="+query+"&ie=UTF8")

def makemytrip():
    
    speak("Train, bus or flight")

    query = takecommand().lower()
    
    if query == "train":
        
        speak("book train ticket or check pnr status or check live train status")
        
        query1= takecommand().lower()

        if "book" or "ticket" in query1:
            
            print("Redirecting to Booking Page")

            webbrowser.open("https://www.makemytrip.com/railways/")
            
        elif "pnr" in query1:

            speak("What is Your Pnr number")

            no = takecommand()
            
            print("Redirecting to pnr status page")

            webbrowser.open("https://www.makemytrip.com/railways/pnrsearch/?pnr="+no)

        else:

            print("redirecting to live train status page")

            webbrowser.open("https://www.makemytrip.com/railways/liveStatus/")

    elif query == "bus":

        print("Redirecting to Bus Booking")

        webbrowser.open("https://www.makemytrip.com/bus-tickets/")
        
        
    elif query == "flight":

        print("redirecting to Flight Booking")

        webbrowser.open("https://www.makemytrip.com/flights/")
    
#______________________________________________________________CAB______________________________________________________________


def Cab():
    
    speak("Sir would You like to book ola or uber")

    query = takecommand().lower()

    if "ola" in query:

        speak("You have choosed ola sir")

        webbrowser.open("https://book.olacabs.com/")

    elif "uber" in query:

        speak("You have choosed uber sir")

        webbrowser.open("https://www.uber.com/in/en/")



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

        # __________________OTT PLATFORMS_____________________
        
        elif "open" and "netflix" in query:

            speak("\nOpening Netflix Sir...")

            webbrowser.open("www.Netflix.com")
            

        elif "open primevidio" in query:

            speak("\nOpening Amazon Prime Vidio Sir...")

            webbrowser.open("www.primevidio.com")
            

        elif "open" and "hotstar" in query:

            speak("\nOpening Disney Plus Hotstar Sir...")

            webbrowser.open("www.Hotstar.com")
            

        
      
    #______________________________________________________
   
   elif "open atom" in query:
            os.system("start atom")
            
     __________________________________________________
     
    def movie():

    speak("Where Would You like to Watch Movie ")

    query3 = takecommand().lower()

    speak("Enjoy Your Movie")

    webbrowser.open("https://in.bookmyshow.com/explore/home/"+query3)
    
    
#_________________________________________________________ONLINE FOOD______________________________________________________

def food():

    speak("Would You Like To Order In Zomato Or swiggy")

    query = takecommand().lower()

    if "zomato" in query:

        speak("Where do you live")

        place = takecommand().lower()

        webbrowser.open("https://www.zomato.com/"+place+"/order-food-online")

    elif "swiggy" in query:

        webbrowser.open("https://www.swiggy.com/restaurants")
     
#__________________________________________________________AMAZON__________________________________________________________

def amazon():

    speak("What would You Like To order From Amazon")

    query = takecommand().lower()

    speak("you have searched "+query)

    webbrowser.open("https://www.amazon.in/"+query)     
     
```
