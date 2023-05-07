#include <MPU6050_tockn.h> // IMU MPU6050 sensor library
#include <Wire.h> // I2C communication
#include <LiquidCrystal_I2C.h> // LCD sensor library

MPU6050 mpu6050(Wire); // Declare instance of MPU6050 class
LiquidCrystal_I2C lcd(0x27, 16, 2); // Initialize the LCD display

int buttonPin = 4; // push button pin
int buttonState; // Current state of the button
int lastButtonState = LOW; // Previous state of the button
int lcdState = LOW; // Current state of the LCD display
int piezoPin = 8; // piezo speaker pin
int ledPin = 13; // led pin
bool isLcdOn = false; // lcd is turned off

void setup() {
  Serial.begin(9600);
  Wire.begin();
  mpu6050.begin();
  mpu6050.calcGyroOffsets(true); // calculates the gyro offsets to calibrate the sensor

  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(piezoPin, OUTPUT);
  pinMode(ledPin, OUTPUT);
  lcd.init();
  lcd.backlight();
  lcd.clear(); // Clear the LCD screen
  lcd.setCursor(0, 0); // Set the cursor to the first column of the first row
}

void loop() {
  buttonState = digitalRead(buttonPin); // reads the state of the push button
  if (buttonState != lastButtonState) {
    if (buttonState == LOW) { // if the button is pressed
      if (isLcdOn) {  // if the LCD display is turned on
        isLcdOn = false; // turn off the LCD display
        lcd.clear(); // clear the LCD screen
        lcd.noBacklight(); // turn off the backlight of the LCD display
        digitalWrite(ledPin, LOW); // turn off the LED
      } else {
        isLcdOn = true;
        lcdState = HIGH;
        lcd.setCursor(0, 0); // Set the cursor to the first column of the first row
        lcd.print("Get ready to get"); // displays text on the LCD display
        lcd.setCursor(0, 1); // sets the cursor to the first column of the second row
        lcd.print("lost?:)"); // displays text on the LCD display
        tone(piezoPin, 1000, 1000);
        delay(2000);
        noTone(piezoPin);
        lcd.clear();
        lcd.backlight();
        delay(1000);
      }
    }
  }
  lastButtonState = buttonState;

  if (isLcdOn) {
    mpu6050.update();
    float yAngle = mpu6050.getAngleY();
    if (yAngle < 0) {
      yAngle += 360; // Add 360 degrees to make it positive
    }
    String compassDir;
    if (yAngle >= 337.5 || yAngle < 22.5) {
      compassDir = "GO NORTH"; // North
    } else if (yAngle >= 22.5 && yAngle < 67.5) {
      compassDir = "GO NORTHEAST"; // North East
    } else if (yAngle >= 67.5 && yAngle < 112.5) {
      compassDir = "GO EAST"; // East
    } else if (yAngle >= 112.5 && yAngle < 157.5) {
      compassDir = "GO SOUTHEAST"; // South East
    } else if (yAngle >= 157.5 && yAngle < 202.5) {
      compassDir = "GO SOUTH"; // South 
    } else if (yAngle >= 202.5 && yAngle < 247.5) {
      compassDir = "GO SOUTHWEST"; // South West
    } else if (yAngle >= 247.5 && yAngle < 292.5) {
      compassDir = "GO WEST"; // West
    } else if (yAngle >= 292.5 && yAngle < 337.5) {
      compassDir = "GO NORTHWEST"; // North West
    }

    Serial.print("Y-axis angle: ");
    Serial.print(yAngle);
    Serial.print(" degrees (");
    Serial.print(compassDir);
    Serial.println(")");

  lcd.setCursor(0, 1); // Set the cursor to the first column of the second row
  lcd.print("Angle: "); // Display the text on the LCD
  lcd.print(yAngle); // Display the angle on the LCD
  lcd.print(" deg   ");
  lcd.setCursor(0, 0); // Set the cursor to the first column of the first row
  
  // Randomly display "YOU ARE LOST!" on the LCD
  if (random(10) < 3) { // 30% chance of displaying "YOU ARE LOST!"
    lcd.print("YOU ARE LOST!");
    digitalWrite(ledPin, HIGH);
    tone(piezoPin, 3000, 1000);
  } else {
    lcd.print(compassDir); // Display the direction on the LCD
    digitalWrite(ledPin, LOW);
  }
  
  delay(1000); // Wait for 1 second
}
}
