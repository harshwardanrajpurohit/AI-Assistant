import datetime
import pyttsx3
import pywhatkit
import requests
import speech_recognition as sr
import webbrowser
import re
from googlesearch import search as google_search
import wikipedia
import time
import threading


def type_with_delay(text):
    for char in text:
        print(char, end='', flush=True)
        time.sleep(0.05)  
    print()


def speak_with_delay(text):
    say(text)

def get_weather(city):
    try:
        query = f"Weather in {city}"
        for result in google_search(query, num=1, stop=1, pause=2):
            webbrowser.open(result)
            return f"Opening weather information for {city}."

        return "Unable to fetch weather information. Please try again later."

    except Exception as e:
        print(f"An error occurred: {e}")
        return "Unable to fetch weather information at the moment."



def calculate(expression):
    try:
        # Use regular expression to sanitize the input and allow only digits and basic operators
        clean_expression = re.sub(r'[^0-9+\-*/().]', '', expression)
        result = eval(clean_expression)
        return result
    except Exception as e:
        print(e)
        return None


def search_on_wikipedia(query):
    try:
        results = wikipedia.summary(query, sentences=2)
        return results
    except wikipedia.exceptions.DisambiguationError as e:
        # Handle disambiguation errors if needed
        print(f"Disambiguation Error: {e}")
        return "Disambiguation Error. Please specify your query."
    except wikipedia.exceptions.PageError as e:
        # Handle page errors if needed
        print(f"Page Error: {e}")
        return "Page not found. Please refine your query."
    
def speak_with_delay(text):
    # Implement your voice output with delay functionality here
    # This function should simulate voice output with delays
    say(text) 


def type_with_delay(text):
    # Implement your typing animation functionality here
    # This function should simulate typing with delays
    print(f"Typing: {text}") 


def type_with_delay(text):
    for char in text:
        print(char, end='', flush=True)
        time.sleep(0.05)  # Adjust the delay as needed
    print()

def say(text, language='en'):
    engine = pyttsx3.init()
    engine.setProperty('rate', 150)
    engine.setProperty('voice', language)
    engine.say(text)
    engine.runAndWait()

def get_hindi_joke():
    api_url = "https://v2.jokeapi.dev/joke/Any?type=single&lang=hi"
    response = requests.get(api_url)
    joke = response.json().get("joke")
    return joke if joke else "Unable to fetch Hindi joke at the moment."

def takeCommand():

    r = sr.Recognizer()
    with sr.Microphone() as source:
        r.energy_threshold = 5000  # Adjust this value based on your environment
        print("Listening...")
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio)
        print(f"User said: {query}")
        return query.lower()
    except sr.UnknownValueError:
        print("Sorry, I did not get that. Could you please repeat?")
        return ""
    except sr.RequestError as e:
        print(f"Error with the speech recognition service; {e}")
        return ""


if __name__ == '__main__':
    print("Hello")
    say("Hello,I am your AI. How may I help you,sir?")

    while True:
        say("Listening...")

        sites = [
            ["youtube", "https://www.youtube.com"],
            ["wikipedia", "https://www.wikipedia.org"],
            ["facebook", "https://www.facebook.com"],
            ["twitter", "https://www.twitter.com"],
            ["instagram", "https://www.instagram.com"],
            ["linkedin", "https://www.linkedin.com"],
            ["github", "https://www.github.com"],
            ["stackoverflow", "https://www.stackoverflow.com"],
            ["amazon", "https://www.amazon.com"],
            ["ebay", "https://www.ebay.com"],
            ["netflix", "https://www.netflix.com"],
            ["hulu", "https://www.hulu.com"],
            ["spotify", "https://www.spotify.com"],
            ["gmail", "https://mail.google.com"],
            ["yahoo", "https://www.yahoo.com"],
            ["outlook", "https://outlook.live.com"],
            ["reddit", "https://www.reddit.com"],
            ["bbc", "https://www.bbc.com"],
            ["cnn", "https://www.cnn.com"],
            ["nytimes", "https://www.nytimes.com"],
            ["weather", "https://weather.com"],
            ["espn", "https://www.espn.com"],
            ["apple", "https://www.apple.com"],
            ["microsoft", "https://www.microsoft.com"],
            ["cnet", "https://www.cnet.com"],
            ["nationalgeographic", "https://www.nationalgeographic.com"],
            ["imdb", "https://www.imdb.com"],
            ["nasa", "https://www.nasa.gov"],
            ["pinterest", "https://www.pinterest.com"],
            ["quora", "https://www.quora.com"],
            ["wikihow", "https://www.wikihow.com"],
            ["buzzfeed", "https://www.buzzfeed.com"],
            ["etsy", "https://www.etsy.com"],
            ["forbes", "https://www.forbes.com"],
            ["nike", "https://www.nike.com"],
            ["adidas", "https://www.adidas.com"],
            ["walmart", "https://www.walmart.com"],
            ["target", "https://www.target.com"],
            ["bestbuy", "https://www.bestbuy.com"],
            ["craigslist", "https://www.craigslist.org"],
            ["huffpost", "https://www.huffpost.com"],
            ["foxnews", "https://www.foxnews.com"],
            ["msn", "https://www.msn.com"],
            ["npr", "https://www.npr.org"],
            ["flipkart", "https://www.flipkart.com"],
            ["snapdeal", "https://www.snapdeal.com"],
            ["paytm", "https://www.paytm.com"],
            ["zomato", "https://www.zomato.com"],
            ["swiggy", "https://www.swiggy.com"],
            ["bookmyshow", "https://www.bookmyshow.com"],
            ["irctc", "https://www.irctc.co.in"],
            ["indiatoday", "https://www.indiatoday.in"],
            ["ndtv", "https://www.ndtv.com"],
            ["timesofindia", "https://www.timesofindia.indiatimes.com"],
            ["hindustantimes", "https://www.hindustantimes.com"],
            ["moneycontrol", "https://www.moneycontrol.com"],
            ["rediff", "https://www.rediff.com"],
            ["ndtv", "https://www.ndtv.com"],
            ["magicbricks", "https://www.magicbricks.com"],
            ["makemytrip", "https://www.makemytrip.com"],
            ["justdial", "https://www.justdial.com"],
            ["cricbuzz", "https://www.cricbuzz.com"],
            ["coursera", "https://www.coursera.org"],
            ["edx", "https://www.edx.org"],
            ["khanacademy", "https://www.khanacademy.org"],
            ["quizlet", "https://www.quizlet.com"],
            ["sparknotes", "https://www.sparknotes.com"],
            ["grammarly", "https://www.grammarly.com"],
            ["mathway", "https://www.mathway.com"],
            ["codecademy", "https://www.codecademy.com"],
            ["scholar.google", "https://scholar.google.com"],
            ["researchgate", "https://www.researchgate.net"],
            ["ted", "https://www.ted.com"],
            ["arxiv", "https://arxiv.org"],
            ["sciencedirect", "https://www.sciencedirect.com"],
            ["jstor", "https://www.jstor.org"],
            ["duolingo", "https://www.duolingo.com"],
            ["merriam-webster", "https://www.merriam-webster.com"],
            ["thesaurus", "https://www.thesaurus.com"],
            ["sparknotes", "https://www.sparknotes.com"],
            ["wolframalpha", "https://www.wolframalpha.com"],
            ["pexels", "https://www.pexels.com"],
            ["unsplash", "https://www.unsplash.com"],
            ["pixabay", "https://www.pixabay.com"],
            ["google", "https://www.google.com"],
            ["gmail", "https://mail.google.com"],
            ["google drive", "https://drive.google.com"],
            ["google maps", "https://maps.google.com"],
            ["google news", "https://news.google.com"],
            ["google photos", "https://photos.google.com"],
            ["google calendar", "https://calendar.google.com"],
            ["google translate", "https://translate.google.com"],
            ["google scholar", "https://scholar.google.com"],
            ["google finance", "https://finance.google.com"],
            ["google books", "https://books.google.com"],
            ["google images", "https://images.google.com"],
            ["google trends", "https://trends.google.com"],
            ["google meet", "https://meet.google.com"],
            ["google classroom", "https://classroom.google.com"],
            ["google hangouts", "https://hangouts.google.com"],
            ["google forms", "https://forms.google.com"],
            ["google sheets", "https://sheets.google.com"],
            ["google slides", "https://slides.google.com"],
            ["google docs", "https://docs.google.com"],
            ["google ads", "https://ads.google.com"],
            ["google analytics", "https://analytics.google.com"],
            ["google developers", "https://developers.google.com"],
            ["google trends", "https://trends.google.com"],
            ["google my business", "https://business.google.com"],
            ["google cloud", "https://cloud.google.com"],
            ["google fonts", "https://fonts.google.com"],
            ["google play", "https://play.google.com"],
            ["google earth", "https://earth.google.com"],
            ["google trends", "https://trends.google.com"],
            ["google jobs", "https://jobs.google.com"],
            ["google arts & culture", "https://artsandculture.google.com"],
            ["google pay", "https://pay.google.com"],
            ["google news", "https://news.google.com"],
            ["google takeout", "https://takeout.google.com"],
            ["google nest", "https://store.google.com/category/nest"],
            ["google photos", "https://photos.google.com"],
            ["google trends", "https://trends.google.com"],
            
        ]
        query = takeCommand()
        for site in sites:
            if f"Open {site[0]}".lower() in query.lower():
                say(f"Opening {site[0]} sir...")
                webbrowser.open(site[1])
                break
        if "play song" in query:
            say("Sure, please tell me the name of the song.")
            song_name = takeCommand()
            pywhatkit.playonyt(song_name)
            break
        
        if "time and date" in query:
            now = datetime.datetime.now()
            current_time = now.strftime("%I:%M %p")  # 12-hour format
            current_date = now.strftime("%B %d, %Y")
            say(f"Current date is {current_date} and the time is {current_time}.", language='en')

        if "time" in query:
                    now = datetime.datetime.now()
                    current_time = now.strftime("%I:%M %p")  # 12-hour format
                    say(f"the time is {current_time}.", language='en')

       
        if "date" in query:
                    now = datetime.datetime.now()
                    # current_time = now.strftime("%I:%M %p")  # 12-hour format
                    current_date = now.strftime("%B %d, %Y")
                    say(f"Current date is {current_date}", language='hi-in')            

        if "play video" in query:
            say("Sure, please tell me the name of the video.")
            video_name = takeCommand()
            pywhatkit.playonyt(video_name)
            break

        if 'Weather' in query:
            say("Sure, please tell me the city name.")
            city_name = takeCommand()
            weather_info = get_weather(city_name)
            say(weather_info)
            
        if 'calculate' in query:
                # Extract the expression after 'calculate'
                expression = query.replace('calculate', '')
                result = calculate(expression)
                if result is not None:
                    say(f"The result is {result}")
                else:
                    say("Sorry, I couldn't perform the calculation.") 

        
        if 'whatsapp' in query:
              say("Opening WhatsApp Web...")
              webbrowser.open("https://web.whatsapp.com/")
              break
          
          
       
        if 'search for ' in query:
            query = query.split('search for ')[-1]
            say(f"Searching {query} on Wikipedia...")
            results = search_on_wikipedia(query)

        # Create two threads for typing animation and voice output
        animation_thread = threading.Thread(target=type_with_delay, args=(results,))
        voice_thread = threading.Thread(target=speak_with_delay, args=(results,))

        # Start both threads
        animation_thread.start()
        voice_thread.start()

        # Wait for both threads to finish
        animation_thread.join()
        voice_thread.join()
        break
