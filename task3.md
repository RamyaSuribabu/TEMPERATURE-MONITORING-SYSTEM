#include <LiquidCrystal.h>

// Initialize the LCD pins
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

// TMP36 temperature sensor connected to A0
const int tempPin = A0;

void setup() {
  lcd.begin(16, 2);              // Initialize the 16x2 LCD
  Serial.begin(9600);            // Start Serial Monitor
  lcd.print("Temp:");            // Initial message on LCD
}

void loop() {
  int tempValue = analogRead(tempPin);            // Read temperature sensor value
  float voltage = tempValue * (5.0 / 1023.0);     // Convert analog value to voltage
  float temperatureC = (voltage - 0.5) * 100.0;  // Convert voltage to Celsius

  // Display temperature on Serial Monitor
  Serial.print("Temperature: ");
  Serial.print(temperatureC);
  Serial.println(" °C");

  // Display temperature on the LCD
  lcd.setCursor(0, 1);           // Move cursor to the second row
  lcd.print(" ");
  lcd.print(temperatureC);       // Display the temperature value
  lcd.print(" C");

  delay(1000);                   // Update every second
}
