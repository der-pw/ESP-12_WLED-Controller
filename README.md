# ESP-12_WLED-Controller V1.3 [![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/S6S7GF5NA)

[English Version below](https://github.com/der-pw/ESP-12_WLED-Controller#english)

---

Designidee eines EPS-12(E/F) basierten NeoPixel (WS2812B, WS2811, SK6812)-Controller speziell für [WLED](https://github.com/Aircoookie/WLED) oder auch Alternativen.

### tl;dr
Ich habe einige Tests zur Stromaufnahme am ESP-32_WLED-Controller durchgeführt. Da beide Controller im Bereich des MOSFET gleich aufgebaut sind, lassen sich die Erkenntnisse übertragen.  
Let's talk about [maximum ratings](https://github.com/der-pw/ESP-32_WLED-Controller/blob/main/maximum_ratings.md)

### Übersicht:
 - [Versionen](https://github.com/der-pw/ESP-12_WLED-Controller#versionen)
 - [Gehäuse](https://github.com/der-pw/ESP-12_WLED-Controller#gehäuse) 
 - [Einstellungen](https://github.com/der-pw/ESP-12_WLED-Controller#einstellungen)
 - [Teileliste](https://github.com/der-pw/ESP-12_WLED-Controller#teileliste)
 - [Anschluss Hinweise](wiring.md) ->

Die Idee war es, einen Controller zu bauen, der mit Pegelwandler arbeitet um das Datensignal, welches der ESP8266 nur mit 3,3V Pegel ausgibt, auf die vom LED-Strip benötigten 5V zu setzen. Gerade bei langen Datenleitungen kann ein 3,3V-Pegel sich schneller "verwaschen". 
Als Levelshifter werwende ich einen **74LVC1G125**.
Zusätzlich kann die Versorgungsspannung für den LED-Strip über einen P-Kanal MOSFET abgeschaltet werden. Auch im ausgeschalteten Zustand verbrauchen die NEOPIXEL-Strips Strom (ca. 1mA/Pixel).   
Praktischerweise bietet WLED hier seit einiger Zeit, die Möglichkeit über einen frei definierten Pin ein "Relay" zu schalten.
Vor dem P-MOSFET sitzt ein weiterer N-MOSFET. Einmal funktioniert dieser als Treiber um den P-MOSFET mit 5V Logikpegel zu schalten und zum anderen als Inverter, damit der Haupt-MOSFET praktisch "active HIGH" am GPIO12 des ESP2866 durchschaltet.

### Versionen:
 - 0.9 erstes Layout veröffentlicht
 - 1.0 kleine Änderungen und Fehler beseitigt
 - - 1.01 C1 und C2 Korrektur der Werte (statt 10nF 10µF) hat keine Auswirkung auf die Platine
 - - 1.1 Gatewiderstand R9 hinzugefügt
 - - 1.2 Gatewiderstand Wert auf 300Ohm geändert
 - - 1.3 Platinenlayout überarbeitet  
 THT-MOSFET entfernt und dafür ...    
 Leiterbahn verbreitert und auf zwei Lagen verteilt  
 zweiter C2 Kondensator  
 Lötjumper unter R6 zum Überbrücken gesetzt  
 zweiter GND Anschluss am Terminal  
 Datenpin von IO4 auf IO2 gelegt [Fehler im Design](https://github.com/der-pw/ESP-12_WLED-Controller/issues/2#issuecomment-1024920433).

![PCB top](img/PCB-top.jpg)

### Gehäuse
![PCB case](Case/Controller_case.jpg)
Es gibt ein simples Gehäuse. 
Die beiden Geäusehälften werden zusammen geklipst.
Die Platine wird mittels 2x5mm Linsenkopfschrauben (Grobgewinde) im Gehäuse befestigt.

### Einstellungen
Die Platine verwendet folgendes Pin-Setting.  
Auf **GPIO0** kann ein externer Button verwendet werden, zum Ein- und Ausschalten und zusätzlich initiert man darüber den Flashvorgang.  
An **GPIO2** hängt das Datensignal und über **GPIO12** wird der MOSFET geschaltet.

![Pin-setting](img/Pin-setting.jpg)


### Teileliste

| Refs | Qty | Component | Description |
| ----- | --- | ---- | ----------- |
| C1 | 1 | 10µF | 0805 10µF |
| C2 | 1 | 47F | 0805 47µF oder 22µF |
| aC2 | 1 | 100µF | alternativer Footprint in 1206 für größere Kerkos |
| C3, C5 | 2 | 100nF | 0805 100nF |
| C4 | 1 | 1000µF | Elko radial 1000µF 6.3V RM3.5 d=8mm l=11.5mm |
| D1 | 1 | Freilaufdiode | SS14 DO-214 |
| J1 | 1 | Screw_Terminal_01x05 |  |
| J2 | 1 | Conn_01x04_Male | Buchsenleiste RM2.54mm |
| JP1 | 1 | BTN/FLASH | Jumper mit Pinheader RM2.54 |
| JP2 | 1 | Jumper_2_Open | Lötbrücke auf der Rückseite für R6 |
| Q1 | 1 | IRLML6344 | MOSFET N-Kanal 30 V 5A SOT-23 |
| Q2 | 1 | IRF7410 | MOSFET P-Kanal -12 V -16A SO-8 |
| R1, R2, R3, R4, R5, R7, R8 | 7 | 10k | 0805 10kΩ |
| R6 | 1 | 470R | 0805 470Ω |
| R9 | 1 | 300R | 0805 300Ω |
| SW1 | 1 | SW_RST | 6mm x3.5mm Push Button SMD|
| U1 | 1 | TS1117-3.3 | Linearregler 3.3V fix alt. AMS1117-3.3, SOT-223 |
| U2 | 1 | ESP-12F | ESP-12F (ESP8266) Wifi-Modul |
| U4 | 1 | 74LVC1G125 | Single Buffer Gate Tri-State als Logic Level Converter, SOT-23-5 |


Diese Platine kann mit einem [fertigen Binary](https://install.wled.me/) verwendet werden.

## Dankeschön!  

Ein besonderer Dank geht an [Aircoookie](https://github.com/Aircoookie) und allen Beteiligten, die am [WLED](https://github.com/Aircoookie/WLED) Projekt mitarbeiten.

----
## English

### tl;dr
I did some power consumption tests on the ESP-32_WLED controller. Both controllers have the same structure in the MOSFET area, the results can be transferred.  
Let's talk about [maximum ratings](https://github.com/der-pw/ESP-32_WLED-Controller/blob/main/maximum_ratings.md)

----

Design idea of an EPS-12 (E / F) based NeoPixel (WS2812B, WS2811, SK6812) controller especially for WLED or alternatives.

Overview:
 - [Versions](https://github.com/der-pw/ESP-12_WLED-Controller#versions)
 - [Case](https://github.com/der-pw/ESP-12_WLED-Controller#case) 
 - [Settings](https://github.com/der-pw/ESP-12_WLED-Controller#settings)
 - [Parts list](https://github.com/der-pw/ESP-12_WLED-Controller#parts-list)
 - [Connecting Hints](wiring.md) ->
 

The idea was to build a controller that works with level converters to set the data signal, which the ESP8266 only outputs with a 3.3V level, to the 5V required by the LED strip. Especially with long data lines, a 3.3V level can "fading" more quickly.
As the level shifter I use a **74LVC1G125**.
In addition, the supply voltage for the LED strip can be switched off via a P-Channel MOSFET. Even when switched off, the NEOPIXEL strips consume electricity (approx. 1mA/pixel).
Conveniently, WLED offers the option of switching a "relay" via a freely defined pin. https://github.com/Aircoookie/WLED/issues/631#issuecomment-578551872
Another N-MOSFET sits in front of the P-MOSFET. On the one hand, this works as a driver to operate the P-MOSFET with a 5V logic level and on the other hand as an inverter, so that the main MOSFET switches through practically "active HIGH" on the GPIO12 of the ESP2866.

### Versions:
 - 0.9 first layout published
 - 1.0 minor changes and bugs fixed
 - - 1.01 C1 and C2 wrong Values fixed (10µF instead of 10nF) has no effects of the PCB
 - - 1.1 added gate resistor R9
 - - 1.2 change gate resisitr value to 300Ohm
 - - 1.3 board layout revised  
 THT MOSFET removed and for that...  
 Traces widened and divided onto two layers  
 second alternative C2 capacitor  
 Solder jumper placed under R6 for bridging  
 second GND connector on the terminal.  
 Data pin placed from IO4 to IO2 [Error in design](https://github.com/der-pw/ESP-12_WLED-Controller/issues/2#issuecomment-1024920433). 
 

![PCB top](img/PCB-top.jpg)

### Case
![PCB case](Case/Controller_case.jpg)
There is a simple case. The two halves of the housing are clipped together. The circuit board is attached to the housing by means of 2x5mm pan head screws (coarse thread).

### Settings
The board uses the following pin setting.
An external button can be used on GPIO0 to switch it on and off and also to initiate the flash process.
The data signal is connected to GPIO2 and the MOSFET is switched via GPIO12.

![Pin-setting](img/Pin-setting.jpg)

### Parts list

| Refs | qty | components | Description |
| ----- | --- | ---- | ----------- |
| C1 | 1 | 10µF | 0805 10µF |
| C2 | 1 | 47F | 0805 47µF or 22µF |
| aC2 | 1 | 100µF | alternative footprint in 1206 for larger caps |
| C3, C5 | 2 | 100nF | 0805 100nF |
| C4 | 1 | 1000µF | Capacitor radial 1000µF 6.3V pich3.5 d=8mm l=11.5mm |
| D1 | 1 | Flyback diode | SS14 DO-214 |
| J1 | 1 | Screw_Terminal_01x05 | |
| J2 | 1 | Conn_01x04_Male | Socket strip pitch 2.54mm |
| JP1 | 1 | BTN/FLASH | Jumper with pin header pitch 2.54 |
| JP2 | 1 | Jumper_2_Open | Solder bridge on the back for R6 |
| Q1 | 1 | IRLML6344 | MOSFET N-channel 30V 5A SOT-23 |
| Q2 | 1 | IRF7410 | MOSFET P-channel -12V -16A SO-8 |
| R1, R2, R3, R4, R5, R7, R8 | 7 | 10k | 0805 10kΩ |
| R6 | 1 | 470R | 0805 470Ω |
| R9 | 1 | 300R | 0805 300Ω |
| SW1 | 1 | SW_RST | 6mm x3.5mm Push Button SMD|
| U1 | 1 | TS1117-3.3 | Linear regulator 3.3V fix old. AMS1117-3.3, SOT-223 |
| U2 | 1 | ESP-12F | ESP-12F (ESP8266) Wifi Module |
| U4 | 1 | 74LVC1G125 | Single Buffer Gate Tri-State as Logic Level Converter, SOT-23-5 |


PCB can be used with a [pre compiled binary](https://install.wled.me/).

## Thanks!  

Special thanks to [Aircoookie](https://github.com/Aircoookie) and all the contributors at the [WLED](https://github.com/Aircoookie/WLED) project.  
