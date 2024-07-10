#define IN1 D5
#define IN2 D6
#define ENA D0
#define POT_PIN A0  // Potansiyometrenin bağlı olduğu analog pin

const int pwmChannel = 0;
const int pwmFreq = 5000;
const int pwmResolution = 8; // 8-bit çözünürlük, değerler 0-255 arasındadır

void setup() {
  // Pin modları ayarlanıyor
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  
  // PWM kanalını kur
  ledcSetup(pwmChannel, pwmFreq, pwmResolution);
  // PWM kanalını ENA pinine ata
  ledcAttachPin(ENA, pwmChannel);

  // Seri haberleşme başlatılıyor
  Serial.begin(115200);
  Serial.println("Deneyap Kart ile mini Vantilator Yapımı!");
}

void loop() {
  // Potansiyometreden değer oku
  int potValue = analogRead(POT_PIN);
  // Potansiyometre değerini 0-4095 aralığından 0-255 aralığına dönüştür
  int speed = map(potValue, 0, 4095, 0, 255); // Potansiyometre 10k ohm, ESP32'nin 12-bit ADC çözünürlüğü

  // Motoru ileri döndürme
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  ledcWrite(pwmChannel, speed);
  
  // Seri port üzerinden hız bilgisini yazdır
  Serial.print("Potansiyometre Değeri: ");
  Serial.print(potValue);
  Serial.print(" -> Motor Hızı: ");
  Serial.println(speed);
  
  delay(100); // 100 milisaniye bekle
}
