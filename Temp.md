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
        
def date():
    """
    Just return date as string
    :return: date if success, False if fail
    """
    try:
        date = datetime.datetime.now().strftime("%b %d %Y")
    except Exception as e:
        print(e)
        date = False
    return date


def time():
    """
    Just return time as string
    :return: time if success, False if fail
    """
    try:
        time = datetime.datetime.now().strftime("%H:%M:%S")
    except Exception as e:
        print(e)
        time = False
    return time
    
    
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



#_______________________________________________________________________________________________________________________________



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
