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

// Оголошуємо змінні для зберігання станів
bool ledState = false;
bool blinkMode = false;
unsigned long previousMillis = 0;
const long interval = 500; // Інтервал миготіння (500 мс)

void setup() {
  // Ініціалізуємо серійний зв'язок на швидкості 9600 бод
  Serial.begin(9600);
  
  // Встановлюємо пін 13 як вихід
  pinMode(13, OUTPUT);
}

void loop() {
  // Перевіряємо чи є дані для зчитування з серійного порту
  if (Serial.available() > 0) {
    // Зчитуємо вхідний байт
    char input = Serial.read();
    
    // Якщо вхід '1', вмикаємо світлодіод
    if (input == '1') {
      digitalWrite(13, HIGH);
      Serial.println("LED is ON");
      blinkMode = false; // Вимикаємо режим миготіння
    }
    // Якщо вхід '0', вимикаємо світлодіод
    else if (input == '0') {
      digitalWrite(13, LOW);
      Serial.println("LED is OFF");
      blinkMode = false; // Вимикаємо режим миготіння
    }
    // Якщо вхід '2', активуємо режим миготіння
    else if (input == '2') {
      blinkMode = true;
      Serial.println("Blink mode is ON");
    }
  }
  
  // Якщо режим миготіння активний
  if (blinkMode) {
    unsigned long currentMillis = millis();
    
    // Перевіряємо, чи пройшов інтервал миготіння
    if (currentMillis - previousMillis >= interval) {
      // Зберігаємо поточний час
      previousMillis = currentMillis;
      
      // Змінюємо стан світлодіода на протилежний
      ledState = !ledState;
      digitalWrite(13, ledState ? HIGH : LOW);
    }
  }
}
