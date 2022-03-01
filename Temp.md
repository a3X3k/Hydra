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
           



def get_news():
    url = 'http://newsapi.org/v2/top-headlines?sources=the-times-of-india&apiKey=ae5ccbe2006a4debbe6424d7e4b569ec'
    news = requests.get(url).text
    news_dict = json.loads(news)
    articles = news_dict['articles']
    try:

        return articles
    except:
        return False


def getNewsUrl():
    return 'http://newsapi.org/v2/top-headlines?sources=the-times-of-india&apiKey=ae5ccbe2006a4debbe6424d7e4b569ec'
    



def convert_size(size_bytes):
   if size_bytes == 0:
       return "0B"
   size_name = ("B", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
   i = int(math.floor(math.log(size_bytes, 1024)))
   p = math.pow(1024, i)
   s = round(size_bytes / p, 2)
   print("%s %s" % (s, size_name[i]))
   return "%s %s" % (s, size_name[i])


def system_stats():
    cpu_stats = str(psutil.cpu_percent())
    battery_percent = psutil.sensors_battery().percent
    memory_in_use = convert_size(psutil.virtual_memory().used)
    total_memory = convert_size(psutil.virtual_memory().total)
    final_res = f"Currently {cpu_stats} percent of CPU, {memory_in_use} of RAM out of total {total_memory}  is being used and battery level is at {battery_percent} percent"
    return final_res





def take_commands():
    
    r = sr.Recognizer()
    
    with sr.Microphone() as source:
        print('Listening')
        r.pause_threshold = 0.7
        
        audio = r.listen(source)
        try:
            print("Recognizing")
           
            Query = r.recognize_google(audio)
            print("the query is printed='", Query, "'")
        except Exception as e:
            print(e)
            print("Say that again sir")
            
            return "None"
   
    import time
    time.sleep(2)
    return Query



def Speak(audio):
   
    engine = pyttsx3.init()
    engine.say(audio)
    engine.runAndWait()

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
