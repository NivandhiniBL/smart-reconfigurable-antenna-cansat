**HARDWARE**
Arduino [Uno/Nano]
RF switch [part number], antenna [type, e.g. patch/dipole with switchable elements]
Custom PCB designed in EasyEDA (schematic + layout in /hardware)

**How it works**
Arduino reads a control input (serial command / sensor trigger).
It sets GPIO pins that bias the RF switches.
Each pin state selects one antenna configuration (e.g. config A / B).
The CanSat communication module transmits through the selected configuration.
