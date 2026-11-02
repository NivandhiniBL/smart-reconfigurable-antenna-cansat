**HARDWARE**
Arduino [Uno/Nano]
RF switch [part number], antenna [type, e.g. patch/dipole with switchable elements]
Custom PCB designed in EasyEDA (schematic + layout in /hardware)

**How it works**
Arduino reads a control input (serial command / sensor trigger).
It sets GPIO pins that bias the RF switches.
Each pin state selects one antenna configuration (e.g. config A / B).
The CanSat communication module transmits through the selected configuration.

**Firmware (sketch)**
const int SW_A = 4;   // RF switch control 1
const int SW_B = 5;   // RF switch control 2

void setConfig(char c) {
  digitalWrite(SW_A, c == 'A');
  digitalWrite(SW_B, c == 'B');
}

void setup() {
  pinMode(SW_A, OUTPUT);
  pinMode(SW_B, OUTPUT);
  Serial.begin(9600);
  setConfig('A');
}

void loop() {
  if (Serial.available()) {
    char c = Serial.read();
    if (c == 'A' || c == 'B') {
      setConfig(c);
      Serial.print("Config: "); Serial.println(c);
    }
  }
}
