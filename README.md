# ESP-12_WLED-Controller  [![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
Designidee eines EPS-12(E/F) basierten NeoPixel (WS2812B, WS2811, SK6812)-Controller speziell für [WLED](https://github.com/Aircoookie/WLED) oder auch Alternativen.

## aktuell ist der Status noch "work in progress"!

![PCB top](https://github.com/der-pw/ESP-12_WLED-Controller/blob/main/PCB_top.jpg)

Die Idee war es, einen Controller zu bauen, der mit Pegelwandler arbeitet um das Datensignal, welches der ESP8266 nur mit 3,3V Pegel ausgibt, auf die vom LED-Strip benötigten 5V zu setzen. Gerade bei langen Datenleitungen kann ein 3,3V-Pegel sich schneller "verwaschen". 
Als Levelshifter werwende ich einen 74LVC1G125.
Zusätzlich kann die Versorgungsspannung für den LED-Strip über einen P-Kanal MOSFET abgeschaltet werden. Auch im ausgeschalteten Zustand verbrauchen die NEOPIXEL-Strips Strom (ca. 1mA/Pixel). 
Footprints gibt es einmal als SOIC-8 und einmal als TO-220.  
Praktischerweise bietet WLED hier die Möglichkeit über GPIO12 ein "Relay" zu schalten. https://github.com/Aircoookie/WLED/issues/631#issuecomment-578551872  
Vor dem P-MOSFET sitz ein weiterer N-MOSFET. Einmal funktioniert dieser als Treiber, um den P-MOSFET mit 5V Logikpegel zu bedienen und zum anderen als Inverter, damit der große MOSFET bei einem HIGH-Pegel am ESP2866 durchschaltet.  
  
Auf diese Weise, kann man fertig gebackende WLED-Binaries verwenden ohne Änderungen vorzunehmen.
