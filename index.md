# Chameleon Light

The Color Copying Chameleon Light is an Arduino-based project that uses a color sensor to detect the color of an object and instantly changes an RGB LED to match it while displaying the detected color on an LCD screen. One of the biggest challenges was calibrating the sensor so it could accurately recognize different colors, but through testing and adjusting the code, the system became much more reliable. This project strengthened my programming, electronics, and problem-solving skills while showing me how hardware and software work together to create an interactive device.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Dohoon K | Homestead High School | Mechanical Engineering | Incoming Freshman

<img width="449" height="316" alt="View recent photos 2" src="https://github.com/user-attachments/assets/568431fa-4c2d-4a0e-b232-9fa138d5c336" />

<img width="3627" height="2614" alt="IMG_0062" src="https://github.com/user-attachments/assets/681df24e-6751-4247-be44-f45a10f97f41" />

# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/9VQuna4wJoY?si=SSX4iqRXOWXZphUK" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my final milestone, I successfully completed my Color Copying Chameleon Light by building an enclosure that holds all of the components together in a clean and organized way. Since my previous milestone, I finished wiring the circuit, improved the color detection by calibrating the sensor with accurate RGB values, programmed the LCD to display the detected color, and assembled everything into the finished case. One of my biggest challenges at BSE was troubleshooting the hardware and code when the sensor gave incorrect readings or the components did not work together as expected. Through patience and testing, I was able to solve these problems, and seeing the finished project accurately detect colors and light up the matching LED was my biggest accomplishment. Throughout BSE, I learned about Arduino programming, electronic circuits, sensors, LCD displays, debugging, and the engineering design process. In the future, I hope to continue learning more about electronics, programming, and robotics so I can build even more advanced projects that combine hardware and software to solve real-world problems.



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/3hmFIJoHKkA?si=CKYQKkNUAFL36dxa" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Since I reached my milestone I put together the color sensor, RGB LED, breadboard and Arduino into one working circuit. I programmed the Arduino so the RGB LED changes to red, green or blue depending on the color detected by the color sensor.The Color Copying Chameleon Light project needs this to work because it needs to copy the color it sees and thats the goal of the Color Copying Chameleon Light. One thing that surprised me was how much testing and adjusting the code was needed to make the color sensor detect colors correctly. I also had problems with the wiring being wrong the LEDs showing the colors and the color sensor identifying colors it didn't know incorrectly.After I fixed these problems the project started to work better. Before I'm done I still need to make the color detection more accurate make the wiring look better and make sure the Color Copying Chameleon Light works with colored objects all the time.The color sensor and RGB LED are really important, for this project.I have to make sure the color sensor works correctly and the RGB LED shows the colors.The Color Copying Chameleon Light needs to copy colors. Thats what I'm trying to achieve.

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/pSkQ2OPn-X0?si=bP1Z78ehyFoMZbBi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my first milestone, my goal was to get the color sensor working with my Arduino Uno R4 Minima. My project is a color-copying chameleon light that detects whether an object is red, green, or blue and changes an RGB LED to match that color, just like a chameleon changing its skin. So far, I have connected the color sensor to the Arduino, written code to read the sensor's output, and tested it with different colored objects. I also used the Serial Monitor to verify that the sensor was correctly identifying the colors. One of the biggest challenges has been getting the sensor to recognize each color accurately because some colors were mixed up or detected inconsistently. I solved this by testing the sensor multiple times and adjusting the code and color thresholds. My next steps are to improve the accuracy of the color detection, connect the RGB LED so it changes to the detected color, and then build and test the complete chameleon light system.

# Schematics 
<img width="827" height="607" alt="Screenshot 2026-07-14 at 8 47 44 AM" src="https://github.com/user-attachments/assets/1007b35a-6006-43d7-966f-11c08a75ca72" />

# CAD
Box:

<img width="50%" height="50%" alt="Screenshot 2026-07-17 at 12 07 20 PM" src="https://github.com/user-attachments/assets/59e2912f-19dc-42e1-b4ae-706b433dbef7" />

Lid:

<img width="50%" height="50%" alt="Screenshot 2026-07-17 at 12 07 50 PM" src="https://github.com/user-attachments/assets/0c2d1541-96b5-4dbf-8f31-fccd70955807" />

# Code
```c++

#include <LiquidCrystal.h>

#define OUT 2
#define S0 4
#define S1 5
#define S2 6
#define S3 7


#define LED_R 9
#define LED_G 10
#define LED_B 11


const bool COMMON_ANODE = false;


LiquidCrystal lcd(42, 43, 32, 33, 34, 35);


struct ColorSig {
 const char* name;
 int sigR, sigG, sigB;     
 int ledR, ledG, ledB;    
};


ColorSig colors[] = {
 {"Purple", 84, 114, 69,   128, 0,   128},
 {"Green",  95, 54,  68,   0,   255, 0  },
 {"Red",    36, 118, 94,   255, 0,   0  },
 {"Yellow", 21, 26,  46,   255, 255, 0  },
 {"Blue",   126, 68, 38,   0,   0,   255},
 {"Black",  158, 156, 137, 0,   0,   0  }
};


const int numColors = sizeof(colors) / sizeof(colors[0]);


int matchColorIndex(int r, int g, int b) {
 long bestDist = -1;
 int bestIndex = 0;


 for (int i = 0; i < numColors; i++) {
   long dr = r - colors[i].sigR;
   long dg = g - colors[i].sigG;
   long db = b - colors[i].sigB;
   long dist = dr * dr + dg * dg + db * db;


   if (bestDist == -1 || dist < bestDist) {
     bestDist = dist;
     bestIndex = i;
   }
 }
 return bestIndex;
}


void setLED(int r, int g, int b) {
 if (COMMON_ANODE) {
   r = 255 - r;
   g = 255 - g;
   b = 255 - b;
 }
 analogWrite(LED_R, r);
 analogWrite(LED_G, g);
 analogWrite(LED_B, b);
}


int readColorFrequency(bool s2, bool s3) {
 digitalWrite(S2, s2 ? HIGH : LOW);
 digitalWrite(S3, s3 ? HIGH : LOW);
 delay(10);
 return pulseIn(OUT, LOW);
}


void setup() {
 Serial.begin(9600);


 pinMode(S0, OUTPUT);
 pinMode(S1, OUTPUT);
 pinMode(S2, OUTPUT);
 pinMode(S3, OUTPUT);
 pinMode(OUT, INPUT);


 pinMode(LED_R, OUTPUT);
 pinMode(LED_G, OUTPUT);
 pinMode(LED_B, OUTPUT);


 digitalWrite(S0, HIGH);
 digitalWrite(S1, LOW);


 lcd.begin(16, 2);
 lcd.print("Color Sensor");
 delay(1000);
 lcd.clear();
}


void loop() {
 int redFreq   = readColorFrequency(LOW, LOW);
 int greenFreq = readColorFrequency(HIGH, HIGH);
 int blueFreq  = readColorFrequency(LOW, HIGH);


 Serial.print("R = "); Serial.print(redFreq);
 Serial.print("   G = "); Serial.print(greenFreq);
 Serial.print("   B = "); Serial.println(blueFreq);


 int idx = matchColorIndex(redFreq, greenFreq, blueFreq);
 ColorSig detected = colors[idx];


 Serial.print("Detected: ");
 Serial.println(detected.name);


 // Update LCD
 lcd.setCursor(0, 0);
 lcd.print("Color: ");
 lcd.print(detected.name);
 lcd.print("        ");
  lcd.setCursor(0, 1);
 lcd.print("R");
 lcd.print(redFreq);
 lcd.print(" G");
 lcd.print(greenFreq);
 lcd.print(" B");
 lcd.print(blueFreq);
 lcd.print("     ");


 setLED(detected.ledR, detected.ledG, detected.ledB);


 delay(500);
}


```

# Bill of Materials

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
- [Basic Design](https://www.circuits-diy.com/electronic-chameleon-arduino/)
- [Color Sensor](https://randomnerdtutorials.com/arduino-color-sensor-tcs230-tcs3200/)
- [LCD Screen](https://lastminuteengineers.com/arduino-1602-character-lcd-tutorial/)
- [RGB LED](https://projecthub.arduino.cc/semsemharaz/interfacing-rgb-led-with-arduino-b59902/)
