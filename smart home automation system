#include <DHT.h>
#define DHTPIN 4           // DHT11 connected to GPIO 4
#define DHTTYPE DHT11
#define PIRPIN 14          // PIR motion sensor to GPIO 14
#define LDRPIN 34          // LDR to GPIO 34 (Analog)
#define RELAY_LIGHT 26     // Relay for Light
#define RELAY_FAN 27       // Relay for Fan

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(115200);
  dht.begin();

  pinMode(PIRPIN, INPUT);
  pinMode(LDRPIN, INPUT);
  pinMode(RELAY_LIGHT, OUTPUT);
  pinMode(RELAY_FAN, OUTPUT);

  digitalWrite(RELAY_LIGHT, LOW);
  digitalWrite(RELAY_FAN, LOW);
}

void loop() {
  float temp = dht.readTemperature();
  float hum = dht.readHumidity();
  int ldrValue = analogRead(LDRPIN);
  int motion = digitalRead(PIRPIN);

  // Auto Light: ON if dark + motion
  if (ldrValue < 1000 && motion == HIGH) {
    digitalWrite(RELAY_LIGHT, HIGH); // Light ON
  } else {
    digitalWrite(RELAY_LIGHT, LOW);  // Light OFF
  }

  // Auto Fan: ON if temp > 30°C
  if (temp > 30) {
    digitalWrite(RELAY_FAN, HIGH);   // Fan ON
  } else {
    digitalWrite(RELAY_FAN, LOW);    // Fan OFF
  }

  // Serial monitor for debug
  Serial.print("Temp: "); Serial.print(temp);
  Serial.print(" °C, Humidity: "); Serial.print(hum);
  Serial.print(" %, LDR: "); Serial.print(ldrValue);
  Serial.print(", Motion: "); Serial.println(motion);

  delay(2000);
}
