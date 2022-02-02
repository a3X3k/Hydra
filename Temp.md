```py
def Navigate():
	
	speak("\nWhere do you wish to navigate to Sir?")
	
	query = takecommand().lower()
	
	if "navigate to" in query:
		
		query.replace("navigate to","")
		
		print("Navigating from current location to",query)
		
		webbrowser.open('https://www.google.com/maps/place/' + query)


if __name__ == "__main__":
    
        if "navigate" in query:
	
            Navigate()
```
