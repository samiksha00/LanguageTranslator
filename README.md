# LanguageTranslator
import speech_recognition as sr
import pyttsx3
from translate import Translator
r = sr.Recognizer()
def SpeakText(command):
    engine = pyttsx3.init()
    engine.say(command)
    engine.runAndWait()

print("Start.......")
print("Language code--\nhi for Hindi\nfr for French\netc....")
lang=input("Enter a Language ")
while(1):
    try:
        
        print("Start Speaking in",lang)
        with sr.Microphone() as source:
            r.adjust_for_ambient_noise(source, duration=0.2)
            audio2 = r.listen(source)
            MyText = r.recognize_google(audio2,language = lang)
            #MyText = r.recognize_google(audio2)
            MyText = MyText.lower()
            print("Did you say "+MyText)
            translator= Translator(from_lang=lang,to_lang="en")
            translation = translator.translate(MyText)
            print(translation)
            SpeakText(translation)
            if translation.lower()=="quit":
                break
    except sr.RequestError as e:
        print("Could not request results; {0}".format(e))
             
    except sr.UnknownValueError:
        print("unknown error occured")
