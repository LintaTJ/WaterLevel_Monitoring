#include <NewPing.h> 

#define I2C_ADDR    0x27  

const int TriggerPin = 11;  
const int EchoPin = 12;     
const int MotorPin = 3;     

unsigned long lastTime = 0;     
unsigned long delayTime = 50;   

NewPing sonar(TriggerPin, EchoPin, 100);  

void setup() {
    Serial.begin(9600);         
    pinMode(MotorPin, OUTPUT);   // Set MotorPin as an output
}

void loop() {
    
    if (millis() - lastTime >= delayTime) {
        lastTime = millis();    
        int distance = sonar.ping_cm(); 

        if (distance >= 0) {  // Check if the distance is valid (>=0)
           if (distance >= 6) {
                 digitalWrite(MotorPin, LOW); // Turn off the motor if the object is farther than 6 cm
            }
            else if(distance<=2){
                digitalWrite(MotorPin, HIGH); // Turn on the motor if the object is between 2 cm and 6 cm
            }
            delay(50);
            
            
        }
    }
}

