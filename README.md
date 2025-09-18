# Siri-voice-assistant
A simple voice-controlled assistant built with Python.   This project mimics Siri’s basic functionality 
it can play music, tell the time, fetch Wikipedia info, crack jokes, and more.
Features
-  Play songs on YouTube  
-  Tell the current time  
- Fetch information from Wikipedia  
- Tell jokes  
- Respond to simple fun questions 


  Tech Stack
- Python  
- [speechrecognition](https://pypi.org/project/SpeechRecognition/)  
- [pyttsx3](https://pypi.org/project/pyttsx3/)  
- [pywhatkit](https://pypi.org/project/pywhatkit/)  
- [wikipedia](https://pypi.org/project/wikipedia/)  
- [pyjokes](https://pypi.org/project/py

For windows users
(run those in command prompt/cmt/terminal) For the robot to listen to our voice/speech pip install speechRecognition

To speak out, or text to speech pip install pyttsx3

For advance control on browser pip install pywhatkit

To get wikipedia data pip install wikipedia

To get funny jokes pip install pyjokes

code:
import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)


def talk(text):
    engine.say(text)
    engine.runAndWait()


def take_command():
    try:
        with sr.Microphone() as source:
            print('listening...')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'Siri' in command:
                command = command.replace('Siri', '')
                print(command)
    except:
        pass
    return command


def run_Siri():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('Current time is ' + time)
    elif 'who the heck is' in command:
        person = command.replace('who the heck is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'date' in command:
        talk('sorry, I have a headache')
    elif 'are you single' in command:
        talk('I am in a relationship with wifi')
    elif 'joke' in command:
        talk(pyjokes.get_joke())
    else:
        talk('Please say the command again.')


while True:
    run_Siri()
