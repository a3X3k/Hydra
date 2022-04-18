
```py
from pyjokes import get_joke
 from random import randint
 '''
 returns  a joke in string format
 you can also add custom jokes in the list
 '''
 joke_list=[]

 def startJoke():
     joke=get_joke()
     joke_list.append(joke)
     return joke_list[randint(0,len(joke_list)-1)]
     
     
     
     
from googletrans import Translator
 translator=Translator()

 def startTranslate(text,src,dest):
     trans=translator.translate(text,src=src,dest=dest)
     print(trans)
     return trans

 #this function detects lang automatically and translates to en
 def autoTranslateEn(text):
     trans=translator.translate(text)
     print(trans)
     return trans

 #this fuction detects lang automatically and translated to dest lang
 def autoTranslate(text,dest):
     trans=translator.translate(text,dest=dest)
     print(trans)
     return trans


 if __name__ == "__main__":
     autoTranslate("This is a demo of translate",dest="es")
```
