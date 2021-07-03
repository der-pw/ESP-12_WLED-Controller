# ESP-12_WLED-Controller  [![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
Designidee eines EPS-12(E/F) basierten NeoPixel (WS2812B, WS2811, SK6812)-Controller speziell für [WLED](https://github.com/Aircoookie/WLED) oder auch Alternativen.

### Versionen:
 - 0.9 erstes Layout veröffentlicht
 - 1.0 kleine Änderungen und Fehler beseitigt

![PCB top](https://github.com/der-pw/ESP-12_WLED-Controller/blob/main/PCB_top.jpg)

Die Idee war es, einen Controller zu bauen, der mit Pegelwandler arbeitet um das Datensignal, welches der ESP8266 nur mit 3,3V Pegel ausgibt, auf die vom LED-Strip benötigten 5V zu setzen. Gerade bei langen Datenleitungen kann ein 3,3V-Pegel sich schneller "verwaschen". 
Als Levelshifter werwende ich einen **74LVC1G125**.
Zusätzlich kann die Versorgungsspannung für den LED-Strip über einen P-Kanal MOSFET abgeschaltet werden. Auch im ausgeschalteten Zustand verbrauchen die NEOPIXEL-Strips Strom (ca. 1mA/Pixel). 
Footprints gibt es einmal als SOIC-8 und einmal als TO-220.  
Praktischerweise bietet WLED hier die Möglichkeit über einen frei definierten Pin ein "Relay" zu schalten. https://github.com/Aircoookie/WLED/issues/631#issuecomment-578551872  
Vor dem P-MOSFET sitzt ein weiterer N-MOSFET. Einmal funktioniert dieser als Treiber, um den P-MOSFET mit 5V Logikpegel zu bedienen und zum anderen als Inverter, damit der große MOSFET bei einem HIGH-Pegel am GPIO12 des ESP2866 durchschaltet.

### Gehäuse
![PCB case](https://github.com/der-pw/ESP-12_WLED-Controller/blob/main/Case/Controller_case.jpg)
Es gibt ein simples Gehäuse. 
Die beiden Geäusehälften werden zusammen geklipst.
Die Platine wird mittels 2x5mm Linsenkopfschrauben (Grobgewinde) im Gehäuse befestigt.

### Einstellungen
Die Platine verwendet folgendes Pin-Setting.  
Auf **GPIO0** kann ein externer Button verwendet werden, zum Ein- und Ausschalten und zusätzlich initiert man darüber den Flashvorgang.  
An **GPIO4** hängt das Datensignal und über **GPIO12** wird der MOSFET geschaltet.

![Pin-setting](https://github.com/der-pw/ESP-12_WLED-Controller/blob/main/Pin-setting.jpg)

#### Warum GPIO4 und nicht Standard GPIO2?
In WLED wird das Datensignal in ausgeschaltetem Zustang auf *HIGH* gelegt. Vermutlich um über einen N-MOSFET (einfacher) den Strip spannungsfrei zu bekommen und keinen "Rücklauf" über DATA zu haben.
Ich habe mich in meiner Schaltung bewusst für einen P-Kanal MOSFET entschieden weil so die Versorgungsspannung zum Strip abgeklemmt wird und nicht nur GND.
Auf GPIO4 wird zudem das Datensignal auf *LOW* geschaltet. Der Strip ist "soft off" quasi spannungsfrei.

Diese Platine kann mit einem fertigen Binary verwendet werden.



