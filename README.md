/*Project Name: Air Conditioning System */
#include <LiquidCrystal.h>

int tempPin = A0;
int motorPin = 12;
int thresholdTemp = 30;

LiquidCrystal lcd(2,3, 4, 5, 6, 7);

float voltage, temperature;
int analogValue;

void setup() {
  Serial.begin(9600);
  pinMode(motorPin, OUTPUT);
  lcd.begin(16, 2);
  lcd.print("Air Conditioning");
  delay(2000);
}

void loop() {
  analogValue = analogRead(tempPin);
  voltage = (analogValue / 1024.0) * 5.0;
  temperature = (voltage - 0.5) * 40;

  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" C");

  lcd.clear();
  lcd.print("Temp: ");
  lcd.print(temperature);
  lcd.print(" C");

  if (temperature > thresholdTemp) {
    digitalWrite(motorPin, HIGH);
    lcd.setCursor(0, 1);
    lcd.print("AC ON");
  } else {
     digitalWrite(motorPin, LOW);
    lcd.setCursor(0, 1);
    lcd.print("AC OFF");
  }

  delay(1000);
}
   
