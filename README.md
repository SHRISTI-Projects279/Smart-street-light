Smart Automatic Street Lighting System  :

The Smart Automatic Street Lighting System is a modern solution aimed at conserving electrical energy and 
enhancing road safety. This project automates street lights using an Arduino microcontroller, a Light Dependent 
Resistor (LDR) to detect daylight, and Infrared (IR) sensors to detect motion of vehicles or pedestrians. The system 
ensures that street lights operate only when necessary — turning off during daytime, glowing dimly during nighttime 
when no activity is detected, and becoming bright upon detecting motion.

Objective : 
The Smart Automatic Street Lighting System improves energy efficiency and safety by automatically controlling street lights based 
on ambient light and motion detection. Main objectives:  
1. Minimize power wastage by automating street light control  
2. Ensure lighting operates only when needed (day/night detection)  
3. Provide brighter illumination when motion is detected at night  
4. Demonstrate an affordable, scalable solution using Arduino technology


Hardware & Software Requirements: 
Hardware:  
Arduino UNO : Microcontroller for processing sensor data and controlling LEDs. 
LDR sensor module:  Detects the ambient light intensity (day/night detection). 
2x IR sensor modules:Detect motion of vehicles or pedestrians near each light. 
2x LEDs(5mm):Represent street lights; brightness controlled via PWM pins. 
2x Resistors (220Ω):  Limit current through LEDs. 
Breadboard and jumper wires (MM/MF/FF): For connecting all components. 

Software: 
.Arduino IDE 
.Tinkercad


Pin Connections: 
Component                    Arduino Pin                 Description 
LDR Sensor                       A0                    Analog input for light detection   
IR Sensor 1                      D2                     Motion detection for LED 1 
IR Sensor 2                      D3                    Motion detection for LED 2  
 LED 1                           D9                    PWM output (with resistor)  
 LED 2                           D10                   PWM output (with resistor)  

Working Principle : 
Day Operation: LDR detects high light → All LEDs OFF  
Night Operation: Low light detected → LEDs at dim level  
Motion Detection: IR sensor triggered → LED brightens for 2 seconds  
The system uses PWM for smooth brightness control and efficient energy usage.  


ARDUINO CODE: 
// --- Pin Configuration --- 
const int LDR_PIN  = A0; 
const int IR1_PIN  = 2; 
const int IR2_PIN  = 3; 
const int LED1_PIN = 9; 
const int LED2_PIN = 10; 
// --- Parameters --- 
int ldrThreshold = 600;   // LDR value above which it's considered dark 
int dimLevel     = 50;    // LED dim brightness 
int brightLevel  = 255;   // LED full brightness 
unsigned long duration = 100; // Time LED stays bright after motion (ms) 
// --- State Variables --- 
unsigned long motionTime1 = 0; 
unsigned long motionTime2 = 0; 
void setup() { 
pinMode(IR1_PIN, INPUT); 
pinMode(IR2_PIN, INPUT); 
pinMode(LED1_PIN, OUTPUT); 
pinMode(LED2_PIN, OUTPUT); 
Serial.begin(9600); 
} 
void loop() { 
int ldrVal  = analogRead(LDR_PIN); 
int ir1Val  = digitalRead(IR1_PIN); 
int ir2Val  = digitalRead(IR2_PIN); 
bool isNight = (ldrVal > ldrThreshold); 
  if (!isNight) { 
    // Daytime → Turn off LEDs 
    analogWrite(LED1_PIN, 0); 
    analogWrite(LED2_PIN, 0); 
  }  
  else { 
    // --- LED 1 Control --- 
    if (ir1Val == LOW) {  
      analogWrite(LED1_PIN, brightLevel); 
      motionTime1 = millis(); 
    }  
    else if (millis() - motionTime1 < duration) { 
      analogWrite(LED1_PIN, brightLevel); 
    }  
    else { 
      analogWrite(LED1_PIN, dimLevel); 
    } 
 
     // --- LED 2 Control --- 
    if (ir2Val == LOW) { 
      analogWrite(LED2_PIN, brightLevel); 
      motionTime2 = millis(); 
    }  
    else if (millis() - motionTime2 < duration) { 
      analogWrite(LED2_PIN, brightLevel); 
    }  
    else { 
      analogWrite(LED2_PIN, dimLevel); 
    }
  } 
 
  delay(100); 
}

Conclusion & Future Scope : 
Conclusion:  
Successfully demonstrates automated street lighting that saves energy while maintaining safety through motionresponsive 
illumination.  

Key Benefits:  
-Energy efficient operation  
-Automatic day/night detection  
-Motion-responsive lighting  
-Cost-effective Arduino implementation 

Future Enhancements:  
-IoT integration for remote monitoring  
-Solar power integration  
-Mobile app control  
-Smart city network integration  
-Weather-based adjustments  

