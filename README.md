# VScodeSesliArama
import speech_recognition as sr
import webbrowser

r = sr.Recognizer()

def record_audio(ask = False):
    with sr.Microphone() as source:
        if ask:
            print(ask)
        audio = r.record(source,duration=3)#Süre ayarı#
        try:
            voice_data = r.recognize_google(audio,language="TR-tr")
            print(voice_data)
        except sr.UnknownValueError:
            print("Ses algılanamadı.")
        except sr.RequestError:
            print("Sistem hatası!")
        return voice_data
    
def respond(voice_data):
    if "Merhaba" in voice_data:
        print("Merhabalar...")
    if "internette ara" in voice_data:
        kelime = record_audio("Ne aramak istersiniz?")
        url = "https://www.google.com/search?q=" + kelime
        webbrowser.get().open(url)

print("Merhaba, efendim.")
voice_data = record_audio()
respond(voice_data)
