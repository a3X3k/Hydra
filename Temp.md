
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
     
     
import subprocess
import configparser


def show_me_my_images():
    """
    This method will open image directory
    :return: Bool
    """
    config = configparser.ConfigParser()
    config.read('configs/config.ini')
    try:
        path = config['default']['photos']
        path = path.split(",")
        for i in path:
            subprocess.Popen(f'explorer "{i}"')
        return True
    except Exception as e:
        print(f"Unable to locate default directory: {e}")
        return False
        
        
import qrcode
def qrCodeGenerator(self):
        self.talk(f"Boss enter the text/link that you want to keep in the qr code")
        input_Text_link = input("Enter the Text/Link : ")
        qr = qrcode.QRCode(
            version=1,
            error_correction=qrcode.constants.ERROR_CORRECT_L,
            box_size=15,
            border=4,
        )
        QRfile_name = (str(datetime.datetime.now())).replace(" ","-")
        QRfile_name = QRfile_name.replace(":","-")
        QRfile_name = QRfile_name.replace(".","-")
        QRfile_name = QRfile_name+"-QR.png"
        qr.add_data(input_Text_link)
        qr.make(fit=True)

        img = qr.make_image(fill_color="black", back_color="white")
        img.save(f"QRCodes\{QRfile_name}")
        self.talk(f"Boss the qr code has been generated")
        

import speedtest
def InternetSpeed(self):
        self.talk("Wait a few seconds boss, checking your internet speed")
        st = speedtest.Speedtest()
        dl = st.download()
        dl = dl/(1000000) #converting bytes to megabytes
        up = st.upload()
        up = up/(1000000)
        print(dl,up)
        self.talk(f"Boss, we have {dl} megabytes per second downloading speed and {up} megabytes per second uploading speed") 
        
        
 
 def pdf_reader(self):
        self.talk("Boss enter the name of the book which you want to read")
        n = input("Enter the book name: ")
        n = n.strip()+".pdf"
        book_n = open(n,'rb')
        pdfReader = PyPDF2.PdfFileReader(book_n)
        pages = pdfReader.numPages
        self.talk(f"Boss there are total of {pages} in this book")
        self.talk("plsase enter the page number Which I nedd to read")
        num = int(input("Enter the page number: "))
        page = pdfReader.getPage(num)
        text = page.extractText()
        print(text)
        self.talk(text)
        
        

def Instagram_Pro(self):
        self.talk("Boss please enter the user name of Instagram: ")
        name = input("Enter username here: ")
        webbrowser.open(f"www.instagram.com/{name}")
        time.sleep(5)
        self.talk("Boss would you like to download the profile picture of this account.")
        cond = self.take_Command()
        if('download' in cond):
            mod = instaloader.Instaloader()
            mod.download_profile(name,profile_pic_only=True)
            self.talk("I am done boss, profile picture is saved in your main folder. ")
        else:
            pass
            
            
            
#Opensource accounts
    def open_source(self,command):
        print(command)
        if 'github' in command:
            self.talk('opening your github')
            webbrowser.open('https://github.com/BolisettySujith')
        elif 'gitlab' in command:
            self.talk('opening your gitlab')
            webbrowser.open('https://gitlab.com/-/profile')
        else :
            self.No_result_found()


```
