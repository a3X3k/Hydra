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
           
```
