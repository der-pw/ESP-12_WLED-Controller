# ESP-12_WLED-Controller  [![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[English Version below](#english)

### Anschluss des Serial-UART Konverter (hier FTDI Adapter)
![FTDI-Adapter](img/FTDI_conn.jpg)

Der Jumper `BTN/FLASH` ist während des Flashvorganges, mindestens aber bei "Power ON" gebrückt, andernfalls wird der Flashvorgang nicht initialisiert.  

#### Installation von WLED
Die einfachste Möglichkeit, WLED zu installieren ist über die "ESP Web Tools" unter https://install.wled.me/ .  
Dort lassen sich fertige Binaries, ganz einfach über den Browser installieren. Weitere Infos findest du unter: https://kno.wled.ge/basics/install-binary/ .  

##### Doppelfunktion von BTN/FLASH
Später kann im normalen Betrieb von WLED an `BTN/FLASH` ein Taster angeschlossen werden, es besteht die Möglichkeit, den Strip an und aus zu schalten, oder [Makros zu steuern](https://kno.wled.ge/features/macros/). Wichtig hierbei ist, dass man einen NO Taster verwendet, sonst bootet der ESP in die Flash Sequenz.

### Anschluss der Versogungsspannung und des LED-Strips
![FTDI-Adapter](img/STRP-PWR_conn.jpg)

```GND``` für Netzteil- und für Stripanschluss  
```DATA``` Anschluss an die Datenleitung des LED-Strips  
```5V``` Versorgungsspannung vom Netzteil  
```SW_5V``` geschaltete Versorgungsspannung des LED-Strips, wird bei Nichtbenutzen deaktiviert, somit ist der Strip spannungsfrei

---
  

## English

### Connecting Serial-UART converter (in this case FTDI adapter)
![FTDI-Adapter](img/FTDI_conn.jpg)

The Jumper ```BTN/FLASH``` is bridges during des flashing progress, alternative at start up.  

#### Installation of WLED
The easiest way to install WLED is via the "ESP Web Tools" at https://install.wled.me/ .  
Pre compiled binaries can be easily installed in your browser. You can find more information at: https://kno.wled.ge/basics/install-binary/ . 

##### Double function of BTN/FLASH

Later, during normal WLED operation mode, a button can be connected to `BTN / FLASH`, so it's possible to switch the strip on and off, or [control any macros](https://kno.wled.ge/features/macros/). It's important to use an NO button, otherwise the ESP will boot into the flashing sequence. 

### Connecting power supply and LED strip
![FTDI-Adapter](img/STRP-PWR_conn.jpg)

```GND``` for power supply and for the strip   
```DATA``` data line of the LED strip  
```5V``` supply voltage  
```SW_5V``` switched supply voltage of the LED strip is deactivated when not in use. So the strip is quite turned off
