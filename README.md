# ESP-12_WLED-Controller V1.3 [![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[English Version below](https://github.com/der-pw/ESP-12_WLED-Controller#english)

Durch einen hässlichen [Fehler im Design](https://github.com/der-pw/ESP-12_WLED-Controller/issues/2#issuecomment-1024920433) ist der Controller bis V1.2 zwar nutzbar, aber bei einigen Effekten resettet der ESP sich nach unbestimmter Zeit. Ich habe die Platine inzwischen überarbeitet, als V1.3 veröffentlicht und somit auch gleich den standard **GPIO02** für den Datenausgang verwendet.

----

Designidee eines EPS-12(E/F) basierten NeoPixel (WS2812B, WS2811, SK6812)-Controller speziell für [WLED](https://github.com/Aircoookie/WLED) oder auch Alternativen.

Übersicht:
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
 - 1.01 C1 und C2 Korrektur der Werte (statt 10nF 10µF) hat keine Auswirkung auf die Platine
 - 1.1 Gatewiderstand R9 hinzugefügt
 - 1.2 Gatewiderstand Wert auf 300Ohm geändert
 - 1.3 Platinenlayout überarbeitet  
 THT-MOSFET entfernt und dafür ...    
 Leiterbahn verbreitert und auf zwei Lagen verteilt  
 zweiter C2 Kondensator  
 Lötjumper unter R6 zum Überbrücken gesetzt  
 zweiter GND Anschluss am Terminal  
 Datenpin von IO4 auf IO2 gelegt.

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
| C1 | 1 | 10µF | Unpolarized capacitor |
| C2 | 1 | 47F | Unpolarized capacitor |
| aC2 | 1 | 100µF | optional |
| C3, C5 | 2 | 100nF | Unpolarized capacitor |
| C4 | 1 | 1000µF | Unpolarized capacitor |
| D1 | 1 | Flyback diode | Diode |
| J1 | 1 | Screw_Terminal_01x05 | Generic screw terminal, single row, 01x05, script generated (kicad-library-utils/schlib/autogen/connector/) |
| J2 | 1 | Conn_01x04_Male | Generic connector, single row, 01x04, script generated (kicad-library-utils/schlib/autogen/connector/) |
| JP1 | 1 | BTN/FLASH |  |
| JP2 | 1 | Jumper_2_Open | Jumper, 2-pole, open |
| Q1 | 1 | IRLML6344 | 3.9A Id, 20V Vds, N-Channel MOSFET, SOT-23 |
| Q2 | 1 | IRF7410 | -6.7A Id, -20V Vds, P-Channel HEXFET Power MOSFET, SO-8 |
| R1, R2, R3, R4, R5, R7, R8 | 7 | 10k | Resistor |
| R6 | 1 | 470R | Resistor |
| R9 | 1 | 300R | Resistor |
| SW1 | 1 | SW_RST | Push button switch, generic, two pins |
| U1 | 1 | TS1117-3.3 | 1A Low Dropout regulator, positive, 3.3V fixed output, SOT-223 |
| U2 | 1 | ESP-12E | 802.11 b/g/n Wi-Fi Module |
| U4 | 1 | 74LVC1G125 | Single Buffer Gate Tri-State, Low-Voltage CMOS |


Diese Platine kann mit einem [fertigen Binary](https://install.wled.me/) verwendet werden.

## Dankeschön!  

Ein besonderer Dank geht an [Aircookie](https://github.com/Aircoookie) und allen Beteiligten, die am [WLED](https://github.com/Aircoookie/WLED) Projekt mitarbeiten.


----
## English

Due to an ugly [error in the design](https://github.com/der-pw/ESP-12_WLED-Controller/issues/2#issuecomment-1024920433) the board can be used up to V1.2, but at some effects the ESP resets after an indefinite period of time. In the meantime I have revised the board, published it as V1.3 and therefore also used the standard **GPIO02** for the data output.

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
 - 1.01 C1 and C2 wrong Values fixed (10µF instead of 10nF) has no effects of the PCB
 - 1.1 added gate resistor R9
 - 1.2 change gate resisitr value to 300Ohm
 - 1.3 board layout revised  
 THT MOSFET removed and for that...  
 Conductor widened and divided into two layers  
 second C2 capacitor  
 Solder jumper placed under R6 for bridging  
 second GND connection on the terminal  
 

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

| Refs | Qty | Component | Description |
| ----- | --- | ---- | ----------- |
| C1 | 1 | 10µF | Unpolarized capacitor |
| C2 | 1 | 47F | Unpolarized capacitor |
| aC2 | 1 | 100µF | Unpolarized capacitor |
| C3, C5 | 2 | 100nF | Unpolarized capacitor |
| C4 | 1 | 1000µF | Unpolarized capacitor |
| D1 | 1 | Flyback diode | Diode |
| J1 | 1 | Screw_Terminal_01x05 | Generic screw terminal, single row, 01x05, script generated (kicad-library-utils/schlib/autogen/connector/) |
| J2 | 1 | Conn_01x04_Male | Generic connector, single row, 01x04, script generated (kicad-library-utils/schlib/autogen/connector/) |
| JP1 | 1 | BTN/FLASH |  |
| JP2 | 1 | Jumper_2_Open | Jumper, 2-pole, open |
| Q1 | 1 | IRLML6344 | 3.9A Id, 20V Vds, N-Channel MOSFET, SOT-23 |
| Q2 | 1 | IRF7410 | -6.7A Id, -20V Vds, P-Channel HEXFET Power MOSFET, SO-8 |
| R1, R2, R3, R4, R5, R7, R8 | 7 | 10k | Resistor |
| R6 | 1 | 470R | Resistor |
| R9 | 1 | 300R | Resistor |
| SW1 | 1 | SW_RST | Push button switch, generic, two pins |
| U1 | 1 | TS1117-3.3 | 1A Low Dropout regulator, positive, 3.3V fixed output, SOT-223 |
| U2 | 1 | ESP-12E | 802.11 b/g/n Wi-Fi Module |
| U4 | 1 | 74LVC1G125 | Single Buffer Gate Tri-State, Low-Voltage CMOS |


PCB can be used with a [pre compiled binary](https://install.wled.me/).

## Thanks!  

Special thanks to [Aircookie](https://github.com/Aircoookie) and all the contributors at the [WLED](https://github.com/Aircoookie/WLED) project.
