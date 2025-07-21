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

For my project, I built a fully functional AI voice assistant using a Raspberry Pi 5. The voice assistant listens to my voice through a USB microphone and talks back using a speaker. I wrote the code in Python and used speech recognition so it can understand what I say and OpenAI’s API so it can respond like ChatGPT. I also added text-to-speech so I can actually hear it talk back to me.

To show that the assistant can control something in real life, I connected an LED light on a breadboard. When I tell the assistant to turn the light on or off, it sends a signal through the Raspberry Pi’s GPIO pins to do it.

**Challenges I Faced and How I Overcame Them**

One of the biggest challenges I faced was figuring out how to connect the relay module and the LED the right way. The relay module I got was different from the one shown in the instructions, so I had to figure out which pins were which by reading diagrams and looking things up online. I also messed up the wiring at first, which made the LED not turn on or off when I gave a command.

After a lot of trial and error, searching online, and asking my instructors for help, I finally figured out how to connect everything correctly. Once the wiring was fixed and matched with my code, the light finally worked the way it was supposed to. This challenge taught me how important it is to double-check circuit diagrams and be patient when testing hardware.

**What I Learned and Next Steps**

Through this project, I learned how to set up a Raspberry Pi, use GPIO pins, and write Python code to connect hardware and software. I also learned how voice recognition and text-to-speech work together with AI like ChatGPT. In the future, I want to add more commands so my assistant can control more devices, like play music when I ask.

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
