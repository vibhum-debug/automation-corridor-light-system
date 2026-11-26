# automation-corridor-light-system
code for automation corridor light system
/*
  CORRIDOR LIGHT AUTOMATION SYSTEM
  Arduino UNO + PIR + LDR + 1 LED
*/

const int pirPin = 2;
const int ldrPin = A0;
const int ledPin = 5;

// Adjust after checking LDR readings
const int darkThreshold = 500;

void setup() {

  pinMode(pirPin, INPUT);
  pinMode(ledPin, OUTPUT);

  digitalWrite(ledPin, LOW);

  Serial.begin(9600);

  Serial.println("Corridor Light Automation");
  Serial.println("PIR Sensor Initializing...");

  delay(30000);

  Serial.println("System Ready!");
}

void loop() {

  int ldrValue = analogRead(ldrPin);
  int pirValue = digitalRead(pirPin);

  Serial.print("LDR Value: ");
  Serial.print(ldrValue);

  Serial.print(" | PIR Value: ");
  Serial.println(pirValue);

  // Dark + Motion = LED ON
  if (ldrValue < darkThreshold && pirValue == HIGH) {

    digitalWrite(ledPin, HIGH);
    Serial.println("LED ON - Motion Detected");

  }
  else {

    digitalWrite(ledPin, LOW);
    Serial.println("LED OFF");

  }

  delay(300);
}
