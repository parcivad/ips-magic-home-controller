[![Version](https://img.shields.io/badge/Symcon-PHP--Modul-red.svg)](https://www.symcon.de/service/dokumentation/entwicklerbereich/sdk-tools/sdk-php/)
[![Version](https://img.shields.io/badge/Symcon%20Version-5.0%20%3E-blue.svg)](https://www.symcon.de/produkt/)
# MHC - Magic Home Controller `copied`

Dieses Modul ist ***kopiert*** von @Wilkware, weil es um die Funktion `SetCustomPattern()` erweitert wurde. IP-Symcon Modul für die Ansteuerung von WiFi LED Controller der Firma _Magic Home_.

## Inhaltverzeichnis

1. [Funktionsumfang](#1-funktionsumfang)
2. [Voraussetzungen](#2-voraussetzungen)
3. [Installation](#3-installation)
4. [Einrichten der Instanzen in IP-Symcon](#4-einrichten-der-instanzen-in-ip-symcon)
5. [Statusvariablen und Profile](#5-statusvariablen-und-profile)
6. [WebFront](#6-webfront)
7. [PHP-Befehlsreferenz](#7-php-befehlsreferenz)

### 1. Funktionsumfang

Das Modul dient zur Ansteuerung von LED Stripes mittels eines WiFi LED Controllers des Herstellers Magic Home.
Das sind Controller vom Typ LD382 bzw. LD382A.

Wenn jemand noch weitere kennt, bitte einfach bei mir melden!

### 2. Voraussetzungen

* ab IP-Symcon Version 5.0

### 3. Installation

* Über den Modul Store das Modul 'Magic Home Controller' installieren.
* Alternativ Über das Modul-Control folgende URL hinzufügen.  
`https://github.com/Wilkware/IPSymconMHC` oder `git://github.com/Wilkware/IPSymconMHC.git`

### 4. Einrichten der Instanzen in IP-Symcon

* Unter "Instanz hinzufügen" ist das 'Magic Home Controller'-Modul (Alias: LED Controller) unter dem Hersteller '(Sonstige)' aufgeführt.

__Konfigurationsseite__:

Die Konfiguration beinhaltet die Zuweisung der IP-Adresse und der Auswahl der Farbkanal-Reihenfolge (RGB-Pins).  
Derzeit werden Stripes mit der Reihenfolge GRB (Gelb, Rot, Blau) und BRG (Blau, Rot, Gelb) unterstützt.  
Die Reihenfolge der Pins beginnt immer ausgehend vom GND-Pin (12V Pin).

Darüber hinaus kann noch ausgewählt werden, ob die Debug-Meldungen auch im Status Logging (Log Meldungen) ausgegeben werden sollen.

Name               | Beschreibung
------------------ | ---------------------------------
WiFi Controller IP | IP-Adresse des Controlers im lokalen WLAN (zb. 192.168.0.10)
RGB Pin Belegung   | Reihenfolge der Farb-Pins (GRB oder BRG), Standard ist GRB

### 5. Statusvariablen und Profile

Ident         | Name                | Typ       |  Profil                      | Beschreibung
------------- | ------------------- | --------- | ---------------------------- | -------------------------------------------------------
Brightness    | Helligkeit          | Integer   | ~Intensity.100               | Helligkeitswert von 0 bis 100%
Color         | Farbe               | Integer   | ~HexColor                    | Farbwert
Mode          | Modus               | Integer   | MHC.ModeGRB oder MHC.ModeBRG | Manueller Farbmodus oder vordefinierter Funktionsmodus
Power         | Aktiv               | Boolean   | ~Switch                      | An/Aus Schalter
Speed         | Geschwindigkeit     | Integer   | ~Intensity.100               | Geschwindigkeitswert von 0 bis 100%

### 6. WebFront

Man kann die Statusvariaben direkt im WebFront verlinken.

### 7. PHP-Befehlsreferenz

`void MHC_SetBrightness(int $InstanzID, int $Brightness);`  
Setzt die Helligkeit auf $Brightness. Die Funktion liefert keinerlei Rückgabewert.

`void MHC_SetColor(int $InstanzID, int $Color);`  
Setzt den Farbwert auf $Color. Die Funktion liefert keinerlei Rückgabewert.

`void MHC_SetCustomPatternColor(int $InstanzID, int $Color);`  
Setzt den Farbwert auf $Color. Die Funktion liefert keinerlei Rückgabewert.

`void MHC_SetMode(int $InstanzID, int $Mode);`  
Setzt den Anzeigemodus auf auf $Mode. Die Funktion liefert keinerlei Rückgabewert.

`void MHC_SetCustomPattern(int $InstanzID, int $Speed, string $Transition_Type, array $color_list );`  
Setzt den gewünschten Modus, Geschwindigkeit und Farbkombination. Diese Funktion wird nicht in den Variablen
aufgeführt, dass heißt das sei nur im Code ausgelöst werden kann:
```php
// Transition: fade // jump // strobe
// Colors : [ [r,g,b], [r.g.b], ... ]
MHC_SetCustomPattern( 150, 'fade', [ [255,0,0], [0,255,0], [0,0,255] ]);
```

### Entwickler

* Heiko Wilknitz ([@wilkware](https://github.com/wilkware))
* Timur Stegmann ([@parcivad](https://github.com/parcivad))
