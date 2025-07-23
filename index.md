# AI Voice Assistant
This is a voice assistant I built using Raspberry Pi that listens to voice commands and turns LED lights on or off on a breadboard. It uses speech recognition, text-to-speech, and OpenAI’s API to understand what I say and respond like ChatGPT. The project shows how a Raspberry Pi can combine hardware control with AI to create a simple smart home assistant.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Sarayu B | Lynrbook High School | Data Science | Incoming Junior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# My Project

<iframe width="560" height="315" src="https://www.youtube.com/embed/pZJwSK9lbgA?si=wVuytmZ6kR-_A6Zf" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

**Project Summary**

For my project, I built a fully functional AI voice assistant using a Raspberry Pi 5. First, I set up the Raspberry Pi by flashing the operating system onto a microSD card and installing all the necessary software. I created a virtual environment for my Python code and installed libraries for speech recognition, text-to-speech, and the OpenAI API.

The voice assistant listens to my voice through a USB microphone and responds through a speaker. It uses speech recognition to turn my speech into text and OpenAI’s API to generate smart replies like ChatGPT. I say the word “Tom” to wake up the assistant, just like saying “Alexa” or “Hey Siri.” When I say “Tom” plus a command, the assistant listens, understands, and replies out loud.

To show that the voice assistant can control real things, I connected an LED light to a breadboard. The Raspberry Pi controls the LED through the GPIO pins and a relay module. When I say “Hey Tom, turn on the light,” the assistant turns the light on, and when I say “Hey Tom, turn off the light,” it turns it off.


**Challenges I Faced and How I Overcame Them**

One big challenge I ran into was getting the relay module and the wiring to work correctly. The relay module I had was different from the one in the instructions, so I had to figure out which pins did what by looking things up online and asking my instructors.

When I wired up the breadboard the first time, a few things went wrong: I connected the wrong GPIO pin in my code, which made the Raspberry Pi send signals to the wrong place. I also accidentally put some positive wires where the negative wires were supposed to go. Because of this, the LED wouldn’t turn on or off when I gave voice commands, and I had to spend a lot of time double-checking the pin numbers and redoing the connections. After lots of Google searches, testing, and help from my instructors, I finally got it right and the light worked perfectly.


**What I Learned and Next Steps**

Through this project, I learned how to set up a Raspberry Pi and connect hardware and software using GPIO pins. I also learned how to use a Python virtual environment and run my code inside it using VS Code. Before this project, I didn’t know that you had to activate a virtual environment in the terminal in VS Code before running the Python script, so that was new for me and really useful to learn.

I also learned how speech recognition and text-to-speech work together with an AI model to make a real voice assistant. In the future, I want to add more voice commands so my assistant can control more lights or even play music when I say, “Hey Tom, play music.”

# My Modifications
**Modifications Summary**

For my Raspberry Pi voice assistant project, I made two extra improvements to make my assistant, Tom, feel more like a real smart home helper. First, I added a feature so Tom can play and stop music when I say voice commands. Second, I made Tom respond to me by saying my name in every reply when I turn the light on or off or when I play or stop music. This made the whole experience feel more personal and fun.

I downloaded a copyright-free MP3 file and saved it in my project folder on the Raspberry Pi. Then, I used the pygame library to play and stop the music file, because playsound couldn’t stop a song once it started. I added commands to my Python script so that when I say “play music,” Tom plays the song, and when I say “stop music,” the song stops. I also edited my script so that when I control the light or the music, Tom says my name in the response, like “Turning the light on, Sarayu,” or “Playing your music now, Sarayu.”

The voice assistant listens through a microphone for commands. If I say “Tom,” it sends what I said to OpenAI and I get an answer back. If I say “turn on the light,” Tom turns the relay on so the LED lights up and says my name. If I say “play music,” it loads the MP3 and plays it. If I say “stop music,” it stops the file right away. Adding my name to the speech makes the responses feel more friendly and personal.

**Challenges I Faced**

One problem was that the playsound library could only play audio, but couldn’t stop it once it started, so I had to switch to pygame and learn how to use it. Another challenge was figuring out how to write the new commands into my existing code without breaking the other parts that control the light or use ChatGPT. I also learned how to make my voice commands more flexible, because sometimes the mic only picks up part of what I say. Finally, I practiced adding custom text to the speak function so Tom would always say my name in the answers for lights and music.

**What I Learned**

These new modifications helped me understand how to handle audio files in Python, use new libraries like pygame, and update voice recognition checks so they are not too strict. I also learned how to personalize the text-to-speech output to say my name, which makes the assistant feel more realistic and fun to use. Overall, this made my project feel closer to real smart speakers like Alexa or Siri but with my own twist.





# Schematics 
![Headstone Image](Schematics)
Fig 1: Schematics on how to set up the breadboard


# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```python
import lgpio
import speech_recognition as sr
import pyttsx3
import openai
import pygame

# Initialize pygame mixer for music playback
pygame.mixer.init()
music_playing = False

# Initializing pyttsx3
listening = True
engine = pyttsx3.init()

# Set your openai api key and customize the chatgpt role
openai.api_key = "insert your open ai key here"
messages = [{"role": "system", "content": "Your name is Tom and give answers in 2 lines"}]

# Customizing the output voice
voices = engine.getProperty('voices')
rate = engine.getProperty('rate')
volume = engine.getProperty('volume')

# Define the GPIO pin number for the relay
RELAY_GPIO_PIN = 17

# Initialize the GPIO
h = lgpio.gpiochip_open(4)

# Set up GPIO pin as output for the relay
lgpio.gpio_claim_output(h, RELAY_GPIO_PIN)

def get_response(user_input):
    messages.append({"role": "user", "content": user_input})
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=messages
    )
    ChatGPT_reply = response["choices"][0]["message"]["content"]
    messages.append({"role": "assistant", "content": ChatGPT_reply})
    return ChatGPT_reply

def turn_on_light():
    lgpio.gpio_write(h, RELAY_GPIO_PIN, 1)
    print("Light turned ON")

def turn_off_light():
    lgpio.gpio_write(h, RELAY_GPIO_PIN, 0)
    print("Light turned OFF")

def speak(text):
    engine.setProperty('rate', 120)
    engine.setProperty('volume', volume)
    engine.setProperty('voice', 'greek')
    engine.say(text)
    engine.runAndWait()

while listening:
    with sr.Microphone() as source:
        recognizer = sr.Recognizer()
        recognizer.adjust_for_ambient_noise(source)
        recognizer.dynamic_energy_threshold = 3000

        try:
            print("Listening...")
            audio = recognizer.listen(source, timeout=5.0)
            response = recognizer.recognize_google(audio)
            print(f"Recognized speech: '{response}'")

            lower_response = response.lower()

            if "tom" in lower_response:
                response_from_openai = get_response(response)
                speak(response_from_openai)

            elif "turn on the light" in lower_response:
                turn_on_light()
                speak("Light turned on")

            elif "turn off the light" in lower_response:
                turn_off_light()
                speak("Light turned off")

            elif "play music" in lower_response:
                if not music_playing:
                    pygame.mixer.music.load('instrumental-undertone-music-275398.mp3')
                    pygame.mixer.music.play()
                    music_playing = True
                    speak("Playing music now")

            elif "stop music" in lower_response:
                if music_playing:
                    pygame.mixer.music.stop()
                    music_playing = False
                    speak("Music stopped")

            else:
                print("Didn't recognize a known command.")

        except sr.UnknownValueError:
            print("Didn't recognize anything.")

# Clean up GPIO on exit
lgpio.gpiochip_close(h)
print("GPIO cleanup completed")
```


```python
import lgpio
import time

RELAY_GPIO_PIN = 17

# Open a GPIO chip (0 is usually the default)
h = lgpio.gpiochip_open(0)

# Set up GPIO pin as output for the relay
lgpio.gpio_claim_output(h, RELAY_GPIO_PIN)

def turn_on_light():
    lgpio.gpio_write(h, RELAY_GPIO_PIN, 1)
    print("Light turned ON")

def turn_off_light():
    lgpio.gpio_write(h, RELAY_GPIO_PIN, 0)
    print("Light turned OFF")

try:
    while True:
        command = input("Type 'on' to turn ON, 'off' to turn OFF, or 'exit' to quit: ").strip().lower()
        if command == "on":
            turn_on_light()
        elif command == "off":
            turn_off_light()
        elif command == "exit":
            break
        else:
            print("Invalid command.")
        time.sleep(0.1)

except KeyboardInterrupt:
    print("\nProgram stopped by user.")

finally:
    # Clean up GPIO
    turn_off_light()
    lgpio.gpiochip_close(h)
    print("GPIO cleaned up.")
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| CanaKit Raspberry Pi 4 4GB Starter PRO Kit - 4 GB RAM | This item is used to set up the Raspberry Pi | $119.99 | <a href= "https://www.amazon.com/CanaKit-Raspberry-4GB-Starter-Kit/dp/B07V5JTMV9/ref=sr_1_3?crid=3I3XY2ESCUCT9&dib=eyJ2IjoiMSJ9.rWngnqnkl0ze0Tu3Q89m-YyU-TuUu5H4EMJPDIgXQWCwbXT8lsJ8fb2-wg7gIbBJ8WM4PJbB1M3gRUYqjucM4RLndoVWVnz1DPY7kEp-sdrcjct9cl9cHpMy4d4CkWd3NQCEZYEA1BfUEJ9shmgH8GrvVNP6xx_vyfJFr-6t7JUC__VJ31efjqF0QijDPe1q_FoMVwdnQPxWnyEBmnnMduXCdDvDfe4RWoyXPgtMazFFI08-sM8kqzOL0v0Xz4Kt_lKxTMvz9h2eiFSLk27fE19Ox_DmrlnK7A6aIPg7UD0.e7PYmGO8gXf6rqj6ZP-MNcl8u78WcJz-fjfFvesuiVw&dib_tag=se&keywords=cana%2Bkit%2Braspberry%2Bpi%2B4&qid=1719254845&s=electronics&sprefix=canakit%2Braspberry%2Bpi%2B4%2Celectronics%2C120&sr=1-3&th=1"> Link </a> |
| AXHDCAP 4K HDMI Video Capture Card, Cam Link Card Game Audio Capture Adapter HDMI to USB 2.0 Record Capture Device for Streaming, Live Broadcasting, Video Conference, Teaching, Gaming | This item is used to connect the Raspberry Pi to your computer | $9.98 | <a href="https://www.amazon.com/Audio-Express-AXHDCAP-Broadcasting-Conference/dp/B0C2MDTY8P/ref=sr_1_3?crid=3CYMQPJXZRG8C&dib=eyJ2IjoiMSJ9.m1E68xLLqhA5tsiHj04YRMJb8qOQG0I9OIpslSLmshw3-fn3xScLIzDEqGlqaXSGxtAQAPa-AOpmBLNL66x1bKwc7JRj5VG3K5KdIgodTnLWYtH_YL-Erp_-J95CCnBd4FvfMl8J43ZIR1c0l4DVqPKDRjmOKmUSCPiBrVgl_xpCuzT5vQNfpbp9PMT3iHnqcy3gw8r3QSnb6jxE0LerJzDC7nGw71z3-MLAtCMa0wh3Y2JPGQTEGoNKP5c1q6KNaVIVkq3g28A7yIQCXTdzUnRciCgg01U8Vz-K5XLBEUQ.jcZvqXwyFOd_ecf2tS-oanK5CPwNooPeurTQLRoY814&dib_tag=se&keywords=hdmi+capture+card&qid=1719254880&s=electronics&sprefix=hdmi+capture+car%2Celectronics%2C136&sr=1-3"> Link </a> |
| [Single] Computer Speaker for Desktop PC, USB-Powered, Plug-n-Play, Wired, External Speaker for Laptop, with Crystal-Clear Sound, Loud Volume, Rich Bass, Built-in USB-C Adapter for Full Compatibility | This item is used to voice the answeres generated by the Voice Assistant | $13.98 | <a href="https://www.amazon.com/Upgraded-Computer-Plug-N-Play-Crystal-Clear-Compatible/dp/B0CJJKF2Q2/ref=sr_1_3?crid=VD4N69I8ME35&dib=eyJ2IjoiMSJ9.2w8B7MOJeg-NqYVZwBfaCL7fq6HetrAl8i4N6Cs-eN_aawzfBjyqG27WiFea1HT4iYwF4vxfBoy5ybf6brsdEMqUu9aj-8xw5CBg144xPYN60T0pAHXkhmiVLGx6m7HpVupXROZW-nWCSSIvVmvsUhgXfKpPDTf4LTBR1zXXFbIoaNSglIfbDuMpqvX23i3fHGGL7amkTzWNaIDcum-QOMOJU4n2PmtXZWAbQgCLRow.B-1KlNd0B6s9rIVUOoicTW5_jZZccCbKzViGO38wMC0&dib_tag=se&keywords=xkx-series%2Bsingle%2Busb%2Bcomputer%2Bspeaker&qid=1753205037&sprefix=xkx-series%2Bsingle%2Busb%2Bcomputer%2Bspeake%2Caps%2C151&sr=8-3&th=1"> Link </a> |
| Youmi Mini USB 2.0 Microphone Mic for Laptop/Desktop PCS - Skype/Voice Recognition Software Driver-Free Audio Receiver Adapter for MSN PC Notebook | This item is used to input your commands into the Raspberry Pi | $7.56 | <a href="https://www.amazon.com/Newest-YOUMI-Microphone-Laptop-desktop/dp/B01MQ2AA0X/ref=sr_1_4?crid=1BQLNHUY2LHCU&dib=eyJ2IjoiMSJ9.cXsUHDop17wBDFrYbVzRrHrOY7kUIPMiN1S0YCF5404Wgb0QjQT1wceu3Q8jkkRHLxgAk26JOwDWRuAiCko8EaN7zvVFG_q40WHskbnh_lh1ygpmk7WO1bli8rKX0dIXgq9ZmuUo-f8scAzuiixKYHUqT9d8Er8MADzLu9G5l2h5lV5bg0iFkLRZY0Ogp3jYJKazsimT2Z4_wRT_2ZsmlqDKlT5chu3rOhCPbD-B1GLYGwTOWArf0vYo675I5ZSV0T-1tTis95pypu4Pw4RCA6v2awtZBAJJQGh9bT6SrdY.gD6a-wpksQfcfHIGeBmxmVOxPB2wPCIqCP4wgSe1Fac&dib_tag=se&keywords=mini+usb+microphone&qid=1719254942&s=electronics&sprefix=mini+microphone%2Celectronics%2C157&sr=1-4"> Link </a> |
| HiLetgo 2pcs 5V One Channel Relay Module Relay Switch with OPTO Isolation High Low Level Trigger | This item connects the Raspberry Pi to a Breadboard in order to control the LED Light | $7.39 | <a href="https://www.amazon.com/HiLetgo-Channel-optocoupler-Support-Trigger/dp/B00LW15A4W/ref=sr_1_2_sspa?crid=2SLR7UAFCVOIE&dib=eyJ2IjoiMSJ9._DYrg2VaJ__x0WDwc6kzeKzUZ-I4cG_HuKZguKLJ6x2wU1JWRAwS7DXLXaPIqbDC75yrqeufpq5UIjGYHhyPUxsyI1oDFu_xzRGc6JKWduau0Cj_6h0WhCwygPCtvA4_CgYTlryCan8bYBTf8OuDtGnTHNTNy8HIE5u3vAD2ZvF2iqD9pHIOJo9CTFOLb1co4zIsEVCo2ff6SQZqB8Ydi-9P0zeNgCAj4aBscyz5IYf1-8t5ilh3uW4sioFKwkUiRVyO-VPdg6PyLJ-9ZzOA1VTnVwBr0zxKjkxOA1sXyzE.Y9tJENLjhR535KMgmf2mT8tunOt8rUZxFo0aKOdIi3A&dib_tag=se&keywords=single+relay+module&qid=1720195075&s=electronics&sprefix=songle+relay+modul%2Celectronics%2C145&sr=1-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1"> Link </a> |
