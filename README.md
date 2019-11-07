# S.A.M.I-Voice-Assistant-

import pyttsx3
import webbrowser
import smtplib
import random
import speech_recognition as sr
import wikipedia
import datetime
import os
import sys
from gtts import gTTS
from win32com.client import Dispatch

engine = pyttsx3.init('sapi5')

voices = engine.getProperty('voices')
engine.setProperty('voice', voices[len(voices)-1].id)

def speak(audio):
    print('' + audio)
    engine.say(audio)
    engine.runAndWait()

def wishMe():
    H = int(datetime.datetime.now().hour)
    if H>=0 and H<12:
        speak('Good Morning!')

    elif H>=12 and H<18:
        speak('Good Afternoon!')

    else:
        speak('Good Evening!')

wishMe()

speak("Namaskar Sir")
speak("Mein hu Sami aapki voice assistant")
speak('Hello Sir, I am your digital assistant Sami your creation!')
speak('How may I help you?')
speak('You just need to command me and I will do it for you')


def takeCommand():
   
    r = sr.Recognizer()                                                                                   
    with sr.Microphone() as source:
        speak("I am listening to you")
        print("Listening...") 
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        print("Recognition.....")
        text = r.recognize_google(audio, language='en-in')
        print('User: ' + text)
        ##speak(text)
        
    except sr.UnknownValueError:
        speak('Sorry sir! I didn\'t get that! Try typing the command!')
        text = str(input('Command: '))

    return text
        

if __name__ == '__main__':

    while True:
    
        text = takeCommand();
        text = text.lower()
        
        if 'open youtube' in text or 'open youtube Sami' in text or 'youtube kholo' in text or 'Youtube kholo' in text or 'Youtube chalao' in text or 'youtube chalao' in text:
            speak('okay')
            webbrowser.open('www.youtube.com')
            
        elif 'search' in text or 'Search' in text or 'search karo' in text or 'Search karo' in text or 'Search Karo' in text or 'search karo' in text:
            speak('okay')
            webbrowser.open("https://www.google.com/search?sxsrf=ACYBGNQNNVU6nHgCNqPuYvac3zbUp-0caA%3A1572455701479&ei=FcW5Xcf6HLrUz7sPpceUIA&q=" +text)

        elif 'open google' in text or 'open google Sami' in text or 'Google kholo' in text or 'google kholo' in text or 'Google chalao' in text or 'google chalao' in text or 'chalo google shuru karo' in text or 'chalo Google shuru karo' in text or 'sami chalo Google shru karo' in text or 'sami chalo google shru karo' in text:
            speak('okay')
            webbrowser.open('www.google.co.in')
            
        elif 'play Shape of you song' in text or 'play shape of you' in text or 'Play shape of you song' in text or Play shape of you song' in text:
        speak('Playing Shape of you by Ed Sheeran')
        webbrowser.open("https://www.youtube.com/watch?v=JGwWNGJdvx8")

        elif 'open gmail' in text or 'open gmail Sami' in text or 'chalo gmail shuru karo' in text:
            speak('okay')
            webbrowser.open('www.gmail.com')

        elif "what\'s up" in text or 'how are you' in text:
            stMsgs = ['Just doing my thing!', 'I am fine!', 'Nice!', 'I am nice and full of energy']
            speak(random.choice(stMsgs))
        
        elif "What is your name??" in text or "tell me your name" in text or "Apna Naam batao" in text:
            stMsgs1 = ['My name is Sami a voice assistent']
            speak(random.choice(stMsgs1))
            
        elif "introduce yourself" in text or 'introduction please' in text or ' Apne bare mein kuch batao' in text:
            stMsgs2 = ['I am Sami a voice assistant. I am hear to make your work easier than you think. I can communicate to you in the language you want. You just want to tell me in which language you want me to communicate']
            speak(random.choice(stMsgs2))
            
        elif "Song" in text or "song" in text:
            speak("Yes Sir")
            webbrowser.open("https://www.youtube.com/results?search_query=" + text)

        elif 'email' in text:
            speak('Who is the recipient? ')
            recipient = takeCommand()

            if 'me' in recipient:
                try:
                    speak('What should I say? ')
                    content = takeCommand()
        
                    server = smtplib.SMTP('smtp.gmail.com', 587)
                    server.ehlo()
                    server.starttls()
                    server.login("Your_Username", 'Your_Password')
                    server.sendmail('Your_Username', "Recipient_Username", content)
                    server.close()
                    speak('Email sent!')

                except:
                    speak('Sorry Sir! I am unable to send your message at this moment!')


        elif 'nothing' in text or 'abort' in text or 'stop' in text or 'Sami abort' in text or 'Sami stop' in text:
            speak('okay')
            speak('Bye Sir, have a good day.')
            sys.exit()
           
        elif 'hello' in text:
            speak('Hello Sir')

        elif 'bye' in text:
            speak('Bye Sir, have a good day.')
            sys.exit()
                                    
        elif 'play music' in text:
            music_folder = Your_music_folder_path
            music = [music1, music2, music3, music4, music5]
            random_music = music_folder + random.choice(music) + '.mp3'
            os.system(random_music)
                  
            speak('Okay, here is your music! Enjoy!')
            

        else:
            text = text
            speak('Searching...')
            try:
                try:
                    res = client.text(text)
                    results = next(res.results).texts
                    speak('WOLFRAM-ALPHA says - ')
                    speak('Got it.')
                    speak(results)
                    
                except:
                    results = wikipedia.summary(text, sentences=1)
                    speak('Got it.')
                    speak('WIKIPEDIA says - ')
                    speak(results)
        
            except:
                webbrowser.open('www.{}.co.in'.format(text))
        
        speak('Next Command! Sir!')
