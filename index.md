# Color Copying Chameleon Light
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

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
| Arduino Mega 2560 | Main microcontroller that runs the project | $49.90 |[ <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a>](https://store-usa.arduino.cc/products/arduino-mega-2560-rev3?srsltid=AfmBOopyJSRFs9aLWJ-gadOdfoNWRNcBSrGM3HQCiS_rnRD5DFws96cc) |
| TCS3200 Color Sensor  | Detects the color of objects | $15.99 | [<a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a>](https://www.amazon.com/Teyleten-Robot-TCS230-TCS3200-Recognition/dp/B08HH8QYF8/ref=sr_1_1_sspa?channelId=500&clpRedir=Y&dib=eyJ2IjoiMSJ9.8Jrg5R16mW3etaJnxSWH5dzj20dKdocjKJEpj4WYQswUkYwti4ttz9yoXbcVBtupAQvq7qrG-CHhx40rfwO65A-8nZgg3K-dbCj_he-UbrPHmDTEfofEuuE_tHEU_Y7UGJFNS3JCtd6LtutdRy5P2vjmTYsf63-uoT8n_CEjB7g6TLlr6cA5jnPGCbML6raChXT1QZ-8rw-qVgJLfuLMyBKXxBUs19dzh7_Fep7kznk.THlPiJERvmhy5KZyWHB8v9j9xFOaiMhuxqs_u_ElGuI&dib_tag=se&keywords=tcs3200+color+sensor&plpRedirect=mhFallback&qid=1783982309&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1) |
| 1602A LCD Display (16×2) | Displays the detected color | $8.99 | [<a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a>](https://www.amazon.com/naughtystarts-Character-Controller-Blacklight-Compatible/dp/B0B1QFDJ3Y/ref=sr_1_3?crid=1K92VXBRV7O21&dib=eyJ2IjoiMSJ9.fEvaU7DCes2rdhGXa5nCIL6M4PoIsaFfHF5YLeFly90oqsQQTCb7eYHDBaQuX5SmHxHhQeujSaQceI7qLgZCqyaFLXhSIZwTKOxZBhTL9cJlErSjsHq-HaibEYhvcDjYhnJENnop7be08v9RqOryEHsIc6yjeI2FvH8d9D47NQG0rB7V2g7TZO7eKRs082YKKaBJU4sg6vOZYjZDvRfMYcdvHihls7zbPjdPuNlw2QCwUt4Q5GL0qSDdfcS8GY73qVT-sGwepOsgE35CDfis07mjJ1eM8wGhFbt6qOdFgvs.wAvidEls7ZFzIRiRiKkBdbXVargSbosKn204y3OBt7M&dib_tag=se&keywords=1602A+LCD+Display+%2816%C3%972%29&qid=1783982412&s=electronics&sprefix=1602a+lcd+display+16+2+%2Celectronics%2C380&sr=1-3) |
| 10kΩ Potentiometer| Adjusts the LCD screen contrast | $6.29 |[[ <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a>](https://store-usa.arduino.cc/products/arduino-mega-2560-rev3?srsltid=AfmBOopyJSRFs9aLWJ-gadOdfoNWRNcBSrGM3HQCiS_rnRD5DFws96cc) ](https://www.amazon.com/Pack-10K-Breadboard-Trim-Potentiometer/dp/B0H2HTC9F9/ref=sr_1_1_sspa?channelId=500&clpRedir=Y&dib=eyJ2IjoiMSJ9.nE7bByED4pEwUIBz__xcRq5hmijiFmeH8eRoc0hQYsd7KpSLh5Nbr0TVqvnVWQANC2eJiFkIpB2-4szxhvegNLZawIH4PDwKvUc2AkwVIGHCDIAz4gRXqz9VU9hbTbdYS5ekvcJGWilceE9K-W_VhtjnNcx9TeGdeTc1Blaadn_Zr2aFtaYH31szc4M_u_mPpebcR22sOmvy9csM5ibVfVvwzKlsUOWy1jZ-khEYgFU.QrOGhcGqCh8ONaAJeZ48u3b_gAIAyV8kzGlvsY_YgN4&dib_tag=se&keywords=10k+potentiometer&plpRedirect=mhFallback&qid=1783982487&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1)|
| Common Cathode RGB LED (4-Pin) | Lights up the detected color | $5.89 | [[<a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a>](https://www.amazon.com/Teyleten-Robot-TCS230-TCS3200-Recognition/dp/B08HH8QYF8/ref=sr_1_1_sspa?channelId=500&clpRedir=Y&dib=eyJ2IjoiMSJ9.8Jrg5R16mW3etaJnxSWH5dzj20dKdocjKJEpj4WYQswUkYwti4ttz9yoXbcVBtupAQvq7qrG-CHhx40rfwO65A-8nZgg3K-dbCj_he-UbrPHmDTEfofEuuE_tHEU_Y7UGJFNS3JCtd6LtutdRy5P2vjmTYsf63-uoT8n_CEjB7g6TLlr6cA5jnPGCbML6raChXT1QZ-8rw-qVgJLfuLMyBKXxBUs19dzh7_Fep7kznk.THlPiJERvmhy5KZyWHB8v9j9xFOaiMhuxqs_u_ElGuI&dib_tag=se&keywords=tcs3200+color+sensor&plpRedirect=mhFallback&qid=1783982309&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1)](https://www.amazon.com/dp/B01MXDSP3V?lv=shuf&channelId=500&plpRedirect=mhFallback) |
| 220Ω Resistors (Pack) |Limits current for the RGB LED and LCD backlight | $5.99 | amazon.com/EDGELEC-Resistor-Tolerance-Multiple-Resistance/dp/B07QK9ZBVZ/ref=sr_1_1?channelId=500&clpRedir=Y&dib=eyJ2IjoiMSJ9.yA61WM4VUMd44diNlAHQmlYydGps9Cd8ytq8lvv78brvYYcSZMEMnidC7Vpe_2v4EJPpSK49v5UWKVvKaFuwYoN7sdiypY6qMMmxOxVbiX0DietlMyOOOW4IF1WClDgAiocIj6Apjc8IGYyUTvqBaF0BasBYtXTKPIs5IHkRPf2OrHyVodX6qh1-K7nCDAE8AQfqzY7xI7_iGTYLDuij4CaGBnfKOaTwrwrrsXYaBW0.i6nLKeJmtl2Upbi9aTF1g-OmJve31sXRAuwx5f4yKGI&dib_tag=se&keywords=220+ohm+resistors&plpRedirect=mhFallback&qid=1783982703&sr=8-1 |
| Solderless Breadboard| Holds the circuit components | $8.99|[[[ <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a>](https://store-usa.arduino.cc/products/arduino-mega-2560-rev3?srsltid=AfmBOopyJSRFs9aLWJ-gadOdfoNWRNcBSrGM3HQCiS_rnRD5DFws96cc) ](https://www.amazon.com/Pack-10K-Breadboard-Trim-Potentiometer/dp/B0H2HTC9F9/ref=sr_1_1_sspa?channelId=500&clpRedir=Y&dib=eyJ2IjoiMSJ9.nE7bByED4pEwUIBz__xcRq5hmijiFmeH8eRoc0hQYsd7KpSLh5Nbr0TVqvnVWQANC2eJiFkIpB2-4szxhvegNLZawIH4PDwKvUc2AkwVIGHCDIAz4gRXqz9VU9hbTbdYS5ekvcJGWilceE9K-W_VhtjnNcx9TeGdeTc1Blaadn_Zr2aFtaYH31szc4M_u_mPpebcR22sOmvy9csM5ibVfVvwzKlsUOWy1jZ-khEYgFU.QrOGhcGqCh8ONaAJeZ48u3b_gAIAyV8kzGlvsY_YgN4&dib_tag=se&keywords=10k+potentiometer&plpRedirect=mhFallback&qid=1783982487&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1)](https://www.amazon.com/EL-CP-003-Breadboard-Solderless-Distribution-Connecting/dp/B01EV6LJ7G/ref=sr_1_2_sspa?channelId=500&clpRedir=Y&dib=eyJ2IjoiMSJ9.5Z5yTwL-oa1r18Ah_zf9OTNexnjSyZDQT0sGT-t_w5YTjogMKB7zIo8u_TUoaq3NYFFf2_INftvxWCJ2-VWegsHiPSSc6o4jtLfuevuJmqgeWdpb2fEigSBzqwRp6jJBeR9TDKA-QOXhtzHvFWtaRweYfxVM5wfJ54rBlw8GC9ijfEO7_JzmIJAvxQhnj4vkjifJjECkMPAC6a9b021NcSQ4hjm8Z56Da-0ux58FYyc.gmWZWGDts3YjhgqJznowEw88FE4DoQ95kxE24WJ24q8&dib_tag=se&keywords=solderless+breadboard&plpRedirect=mhFallback&qid=1783982778&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1)|
| Male-to-Male Jumper Wires |Connects the components together | $6.98 | https://www.amazon.com/EDGELEC-Breadboard-Multicolored-1pin-1pin-Connector/dp/B07GD1ZCHQ/ref=sr_1_1_sspa?crid=3K5C0FF3XJU40&dib=eyJ2IjoiMSJ9.BMvrgU_YjBIEPI70oBIcSePG-SiwkwmsyvjcXrOVmvhAE43A_kwPGZSsGKkTRDxLbjuNtqgZZ03fkrbEMYbdORM3R1RYusE0l6ns5QGdXx360Hlt8FSaUL3aCo_xE-GJHucqt6HBFBgC4Ef6zGFGyrKqyxJGMbHVr3lVhxvS8kxs_74EzlMeoWjdMCZSrleOwL-lJkMoonluvpSv_PgYWrvPOMslkJXFsTvxqA5NZl8.VAuXOgtu3iEIOoMCyh9jUAi_S7XNsnPLkf9nBYfRp60&dib_tag=se&keywords=Male-to-Male%2BJumper%2BWires&qid=1783982856&sprefix=male-to-male%2Bjumper%2Bwires%2Caps%2C221&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1 |
| USB A to USB B Cable |Programs and powers the Arduino Mega | $15.99 | [amazon.com/EDGELEC-Resistor-Tolerance-Multiple-Resistance/dp/B07QK9ZBVZ/ref=sr_1_1?channelId=500&clpRedir=Y&dib=eyJ2IjoiMSJ9.yA61WM4VUMd44diNlAHQmlYydGps9Cd8ytq8lvv78brvYYcSZMEMnidC7Vpe_2v4EJPpSK49v5UWKVvKaFuwYoN7sdiypY6qMMmxOxVbiX0DietlMyOOOW4IF1WClDgAiocIj6Apjc8IGYyUTvqBaF0BasBYtXTKPIs5IHkRPf2OrHyVodX6qh1-K7nCDAE8AQfqzY7xI7_iGTYLDuij4CaGBnfKOaTwrwrrsXYaBW0.i6nLKeJmtl2Upbi9aTF1g-OmJve31sXRAuwx5f4yKGI&dib_tag=se&keywords=220+ohm+resistors&plpRedirect=mhFallback&qid=1783982703&sr=8-1](https://www.amazon.com/Printer-Gold-Plated-Connector-Compatible-Keyboard/dp/B0GFDKF382/ref=sr_1_1_sspa?crid=1R38XZDU51W8Z&dib=eyJ2IjoiMSJ9.0pl8BL_1yUhugdKy06gDe_JpWY50I1P1369Jvo5Re-Fxu0OufhWIc3_Z5q_Kkl5GU6vWhCXaiX4BiHvF7w0_TTGZAcqK-ievEjNeOjD1gckYANsisQ77gFALpdVdbIgKTw3hR0vUbgaPOZDU_-FvmH7AW_RWEHbnk7MhrWquY96yq912IOUAXxdQ87HOpcOG48GQBwbMcWOsD-x3vKzu7rjnlxlrYkcGzNm6ddV5pME.Dey3Mx9dwCrAycuglY_UR9Xx8C0QySt83YVjnnoxGNA&dib_tag=se&keywords=USB%2BA%2Bto%2BUSB%2BB%2BCable&qid=1783982919&sprefix=usb%2Ba%2Bto%2Busb%2Bb%2Bcable%2Caps%2C181&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1) |
# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
