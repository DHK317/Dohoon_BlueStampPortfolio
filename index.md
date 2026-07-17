The Color Copying Chameleon Light is an Arduino-based project that uses a color sensor to detect the color of an object and instantly changes an RGB LED to match it while displaying the detected color on an LCD screen. One of the biggest challenges was calibrating the sensor so it could accurately recognize different colors, but through testing and adjusting the code, the system became much more reliable. This project strengthened my programming, electronics, and problem-solving skills while showing me how hardware and software work together to create an interactive device.
You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:

```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Dohoon K | Homestead High School | Mechanical Engineering | Incoming Freshman

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/3hmFIJoHKkA?si=CKYQKkNUAFL36dxa" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Since I reached my milestone I put together the color sensor, RGB LED, breadboard and Arduino into one working circuit. I programmed the Arduino so the RGB LED changes to red, green or blue depending on the color detected by the color sensor.The Color Copying Chameleon Light project needs this to work because it needs to copy the color it sees and thats the goal of the Color Copying Chameleon Light. One thing that surprised me was how much testing and adjusting the code was needed to make the color sensor detect colors correctly. I also had problems with the wiring being wrong the LEDs showing the colors and the color sensor identifying colors it didn't know incorrectly.After I fixed these problems the project started to work better. Before I'm done I still need to make the color detection more accurate make the wiring look better and make sure the Color Copying Chameleon Light works with colored objects all the time.The color sensor and RGB LED are really important, for this project.I have to make sure the color sensor works correctly and the RGB LED shows the colors.The Color Copying Chameleon Light needs to copy colors. Thats what I'm trying to achieve.

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/pSkQ2OPn-X0?si=bP1Z78ehyFoMZbBi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my first milestone, my goal was to get the color sensor working with my Arduino Uno R4 Minima. My project is a color-copying chameleon light that detects whether an object is red, green, or blue and changes an RGB LED to match that color, just like a chameleon changing its skin. So far, I have connected the color sensor to the Arduino, written code to read the sensor's output, and tested it with different colored objects. I also used the Serial Monitor to verify that the sensor was correctly identifying the colors. One of the biggest challenges has been getting the sensor to recognize each color accurately because some colors were mixed up or detected inconsistently. I solved this by testing the sensor multiple times and adjusting the code and color thresholds. My next steps are to improve the accuracy of the color detection, connect the RGB LED so it changes to the detected color, and then build and test the complete chameleon light system.

# Schematics 
<img width="827" height="607" alt="Screenshot 2026-07-14 at 8 47 44 AM" src="https://github.com/user-attachments/assets/1007b35a-6006-43d7-966f-11c08a75ca72" />


# Code
```c++
#include <LiquidCrystal.h>


// LCD
LiquidCrystal lcd(12, 13, 8, A0, A1, A2);


// Color Sensor
#define S0 4
#define S1 5
#define S2 6
#define S3 7
#define sensorOut 2


// RGB LED
#define RED_LED 9
#define GREEN_LED 10
#define BLUE_LED 11


int r, g, b;


void setup() {
 Serial.begin(9600);


 lcd.begin(16, 2);
 lcd.clear();
 lcd.print("Color Sensor");


 pinMode(S0, OUTPUT);
 pinMode(S1, OUTPUT);
 pinMode(S2, OUTPUT);
 pinMode(S3, OUTPUT);
 pinMode(sensorOut, INPUT);


 pinMode(RED_LED, OUTPUT);
 pinMode(GREEN_LED, OUTPUT);
 pinMode(BLUE_LED, OUTPUT);


 // 20% frequency scaling
 digitalWrite(S0, HIGH);
 digitalWrite(S1, LOW);


 delay(2000);
 lcd.clear();
}


void loop() {


 // Read Red
 digitalWrite(S2, LOW);
 digitalWrite(S3, LOW);
 r = pulseIn(sensorOut, LOW);


 // Read Green
 digitalWrite(S2, HIGH);
 digitalWrite(S3, HIGH);
 g = pulseIn(sensorOut, LOW);


 // Read Blue
 digitalWrite(S2, LOW);
 digitalWrite(S3, HIGH);
 b = pulseIn(sensorOut, LOW);


 Serial.print("R=");
 Serial.print(r);
 Serial.print(" G=");
 Serial.print(g);
 Serial.print(" B=");
 Serial.println(b);


 lcd.setCursor(0, 0);
 lcd.print("Color:        ");
 lcd.setCursor(0, 1);


 if (r < g && r < b) {
   digitalWrite(RED_LED, HIGH);
   digitalWrite(GREEN_LED, LOW);
   digitalWrite(BLUE_LED, LOW);


   lcd.print("RED           ");
 }
 else if (g < r && g < b) {
   digitalWrite(RED_LED, LOW);
   digitalWrite(GREEN_LED, HIGH);
   digitalWrite(BLUE_LED, LOW);


   lcd.print("GREEN         ");
 }
 else if (b < r && b < g) {
   digitalWrite(RED_LED, LOW);
   digitalWrite(GREEN_LED, LOW);
   digitalWrite(BLUE_LED, HIGH);


   lcd.print("BLUE          ");
 }
 else {
   digitalWrite(RED_LED, LOW);
   digitalWrite(GREEN_LED, LOW);
   digitalWrite(BLUE_LED, LOW);


   lcd.print("UNKNOWN       ");
 }


 delay(300);
}

```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Mega 2560 | Main microcontroller that runs the project | $49.90 | <a href="https://www.amazon.com/Teyleten-Robot-TCS230-TCS3200-Recognition/dp/B08HH8QYF8"> Link </a> |
| TCS3200 Color Sensor | Detects the color of objects | $15.99 | <a href="https://www.amazon.com/Teyleten-Robot-TCS230-TCS3200-Recognition/dp/B08HH8QYF8"> Link </a> |
| 1602A LCD Display (16×2) | Displays the detected color | $8.99 | <a href="https://www.amazon.com/Kiro-Seeu-Characters-Compatible-Duemilanove/dp/B099K3J8GL"> Link </a> |
| 10kΩ Potentiometer | Adjusts the LCD screen contrast | $6.29 | <a href="https://www.amazon.com/Potentiometer-Breadboard-Resistors-Assortment-Compatible/dp/B09G9TBY38"> Link </a> |
| Common Cathode RGB LED (4-Pin) | Lights up the detected color | $5.89 | <a href="https://www.amazon.com/EDGELEC-Tri-Color-Multicolor-Diffused-Resistors/dp/B077XGF3YR"> Link </a> |
| 220Ω Resistors (Pack) | Limits current for the RGB LED and LCD backlight | $5.99 | <a href="https://www.amazon.com/EDGELEC-Resistor-Tolerance-Resistance-Optional/dp/B07HDGF48W"> Link </a> |
| Male-to-Male Jumper Wires | Connects the components together | $6.98 | <a href="https://www.amazon.com/EDGELEC-Breadboard-Multicolored-1pin-1pin-Connector/dp/B07GD1ZCHQ"> Link </a> |
| Solderless Breaboard | Keeps all the compnents organized and connected | $8.99 | <a href="https://www.amazon.com/EL-CP-003-Breadboard-Solderless-Distribution-Connecting/dp/B01EV6LJ7G"> Link </a> |
| USB A to USB B Cable | Programs and powers the Arduino Mega | $15.99 | <a href="https://www.amazon.com/Printer-Gold-Plated-Connector-Compatible-Keyboard/dp/B0GFDKF382"> Link </a> |

<!-- # Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Mega 2560 | Main microcontroller that runs the project | $49.90 | <a href="https://www.amazon.com/Teyleten-Robot-TCS230-TCS3200-Recognition/dp/B08HH8QYF8/"> Link </a>|

| TCS3200 Color Sensor | Detects the color of objects | $15.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6](https://www.amazon.com/Teyleten-Robot-TCS230-TCS3200-Recognition/dp/B08HH8QYF8/"> Link </a> |

| 1602A LCD Display (16×2) | Displays the detected color | $8.99 | <a href="https://www.amazon.com/Kiro-Seeu-Characters-Compatible-Duemilanove/dp/B099K3J8GL/"> Link </a> |
| 10kΩ Potentiometer | Adjusts the LCD screen contrast | $6.29 | <a href="https://www.amazon.com/Potentiometer-Breadboard-Resistors-Assortment-Compatible/dp/B09G9TBY38/"> Link </a> |
| Common Cathode RGB LED (4-Pin) | Lights up the detected color | $5.89 | <a href="https://www.amazon.com/EDGELEC-Tri-Color-Multicolor-Diffused-Resistors/dp/B077XGF3YR/"> Link </a> |
| 220Ω Resistors (Pack) | Limits current for the RGB LED and LCD backlight | $5.99 | <a href="https://www.amazon.com/EDGELEC-Resistor-Tolerance-Resistance-Optional/dp/B07HDGF48W/"> Link </a> |
| Male-to-Male Jumper Wires | Connects the components together | $6.98 | <a href="https://www.amazon.com/EDGELEC-Breadboard-Multicolored-1pin-1pin-Connector/dp/B07GD1ZCHQ/"> Link </a> |
| Solderless Breaboard | Keeps all the compnents organized and connected | $8.99 | <a href="https://www.amazon.com/EL-CP-003-Breadboard-Solderless-Distribution-Connecting/dp/B01EV6LJ7G/"> Link </a> |
| USB A to USB B Cable | Programs and powers the Arduino Mega | $15.99 | <a href="https://www.amazon.com/Printer-Gold-Plated-Connector-Compatible-Keyboard/dp/B0GFDKF382/"> Link </a> |

-->


# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Basic Design](https://www.circuits-diy.com/electronic-chameleon-arduino/)
- [Color Sensor](https://randomnerdtutorials.com/arduino-color-sensor-tcs230-tcs3200/)
- [LCD Screen](https://lastminuteengineers.com/arduino-1602-character-lcd-tutorial/)
- [RGB LED](https://projecthub.arduino.cc/semsemharaz/interfacing-rgb-led-with-arduino-b59902/)
To watch the BSE tutorial on how to create a portfolio, click here.
