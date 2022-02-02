```py
def Prime():
    speak("Which movie do you wish to watch Sir?")

    query = takecommand().lower()
    query.replace(" ","+")
    print("Ok Sir, Opening Prime Video and Searching for",query)
    webbrowser.open("https://www.primevideo.com/search/ref=atv_nb_sr?phrase="+query+"&ie=UTF8")
```
