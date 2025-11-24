// Smart-bulb-programmed-with-Arduino
const int soundSensor = 2;
const int relay = 3;

bool lightOn = false;
unsigned long lastTriggerTime = 0;
unsigned int debounceDelay = 800;

void setup() {
  pinMode(soundSensor, INPUT);
  pinMode(relay, OUTPUT);
  digitalWrite(relay, HIGH);
}

void loop() {
  int sound = digitalRead(soundSensor);
  unsigned long currentTime = millis();

  if (sound == HIGH && currentTime - lastTriggerTime > debounceDelay) {
    lightOn = !lightOn;
    digitalWrite(relay, lightOn ? LOW : HIGH);
    lastTriggerTime = currentTime;
  }
}
