# Rop
void setup() {
  Serial.begin(9600);
  pinMode(13, OUTPUT);
}

void loop() {
  if (Serial.available() > 0) {
    char input = Serial.read();
    if (input == '1') {
      digitalWrite(13, HIGH);
      Serial.println("LED is ON");
    }
    else if (input == '0') {
      digitalWrite(13, LOW);
      Serial.println("LED is OFF");
    }
  }
}
