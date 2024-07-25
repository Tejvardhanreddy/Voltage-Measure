#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);  
const int potPin = A0;  
const float R1 = 19000.0;  
const float R2 = 1000.0;  

void setup() {
  lcd.init();                      
  lcd.backlight();                 
  lcd.clear();                    
  lcd.setCursor(0, 0);            
  lcd.print("Voltage:");         

  pinMode(potPin, INPUT);          
  Serial.begin(9600);              
}

void loop() {
  int rawValue = analogRead(potPin);
  float scaledVoltage = (rawValue / 1023.0) * 5.0;  
  float actualVoltage = scaledVoltage * (R1 + R2) / R2;  
  
  lcd.setCursor(9, 1);           
  lcd.print("      ");            
  lcd.setCursor(9, 1);            
  lcd.print(actualVoltage, 2);
  lcd.print(" V");               

  delay(100);                  
}
