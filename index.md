# AI Voice Assistant
This is a voice assistant I built using Raspberry Pi that listens to voice commands and turns LED lights on or off on a breadboard. It uses speech recognition, text-to-speech, and OpenAI’s API to understand what I say and respond like ChatGPT. The project shows how a Raspberry Pi can combine hardware control with AI to create a simple smart home assistant.

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Sarayu B | Lynrbook High School | Data Science | Incoming Junior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# My Project
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


# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
