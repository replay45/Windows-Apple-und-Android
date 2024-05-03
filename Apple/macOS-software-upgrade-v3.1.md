# MacOS Upgrade (nicht mehr von Apple unterstützte Macs)

- Das neueste MacOS auf einem älteren Mac installieren, um auch auf nicht mehr 
von Apple unterstützten Macs die aktuellste MacOS Version nutzen zu können.


`Getestet auf einem MacBook 6,1 - 13,3" (2013) mit MacOS BigSur als letzte offiziell unterstützte Version.
Upgrade auf MacOS Sonoma erfolgreich durchgeführt.`


`Anleitung verfasst am 8.12.2023`


> [OpenCore-Legacy-Patcher](https://dortania.github.io/OpenCore-Legacy-Patcher/START.html)


---------------------------------------------------------------------------------------------------------------------------------------------


### Was ist der OpenCore-Legacy-Patcher ?

OpenCore ist ein Bootloader, der in das System eingreift und dem Mac vorgaukelt, 
dass die offizielle MacOS Version installiert wäre, obwohl dies nicht der Fall ist.
Denn beim Bootvorgang überprüft der Mac die Version von MacOS, der Bootloader 
patched allerdings diese Stelle und somit kann danach auch eine nicht mehr offiziell 
unterstütze Version installiert werden.


### WICHTIG:
- Es wird für das Upgrade ein USB-Stick von mind. 16GB oder mehr benötigt !
- Zudem sollte der USB-Stick direkt an einem USB-Port des Macs angeschlossen sein (KEIN USB-HUB etc.), um Fehlerquellen zu vermeiden.


- Zudem empfiehlt es sich, alle Daten auf dem Mac abzusichern, da es nicht 
ausgeschlossen ist, dass es zu einem Datenverlust kommen könnte.



---------------------------------------------------------------------------------------------------------------------------------------------


## Disclaimer

Das Upgrade erfolgt auf eigene Gefahr und der Autor der Anleitung haftet nicht für entstandene Schäden !
Es ist nicht ausgeschlossen, dass es zu Datenverlust, Fehlern in MacOS oder Kompatibilitätsproblemen kommen könnte, 
da das Upgrade inoffiziell durchgeführt wird.
Daher empfiehlt es sich das Upgrade nur durchzuführen, wenn jeglicher Support & Garantie für das entsprechende Gerät abgelaufen sind.


---------------------------------------------------------------------------------------------------------------------------------------------


## Software Updates & Upgrades

### Software Upgrades
Wenn ein weiteres MacOS-Upgrade durchgefüghrt werden soll (z.B. von MacOS 14 auf 15), muss dies wieder mit dem OpenCore-Legacy-Patcher
geschehen. Dieser muss davor jedoch auch geupdatet werden.

### Software Updates
Auch wenn Software Updates innerhalb einer Version (z.B. von MacOS 14.1 auf 14.2.) in den meisten Fällen keine Probleme bereiten sollten,
`empfiehlt` es sich jedoch trotzdem diese `nur gewissenhaft zu installieren` und `automatische Updates in den Einstellungen auszuschalten`.


---------------------------------------------------------------------------------------------------------------------------------------------


1. Kompatibilitätsprüfung

Zuerst muss geprüft werden, ob der Mac vom OpenCore-Legacy-Patcher unterstützt wird:

```
$ system_profiler SPHardwareDataType | grep 'Model Identifier'
```

Version kopieren und auf der verlinkten Kompatibilitätsliste prüfen.


---------------------------------------------------------------------------------------------------------------------------------------------


2. Download und Installer

	- Der OpenCore legacy Patcher muss zunächst [heruntergeladen](https://dortania.github.io/OpenCore-Legacy-Patcher/START.html) werden.
	- Nach dem öffnen zu "Creating the Installer" gehen,
	- danach auf "OpenCore Legacy Patcher Release Apps" klicken und von Github die 
	"GUI.app.zip" herunterladen, entpacken und installieren.

---------------------------------------------------------------------------------------------------------------------------------------------


3. Download und Flashing

	- USB Stick einstecken und OpenCore Patcher - App öffnen.
	- Nun auf "create MacOS Installer" klicken,
	- falls dieser Vorgang noch nie durchgeführt wurde, auf "Download macOS Installer" klicken
	- und anschließend eine Version auswählen (Am besten die aktuellste OS-Version, sollten Zweifel bestehen,
	oder das neuste MacOS gerade erst releast worden sein, empfielt es sich, zur Sicherheit die vorletzte
	Version zu nutzen, um sicherzustellen, dass das gewünschte Ergebnis erzielt wird.) 


- Hinweis:
Der Download kann eine Weile dauern !


	- Die Frage, ob der Installer erstellt werden soll, mit "Ja" beantworten.
	- Einen bootbaren USB-Stick erstellen, dabei das Speichermedium achten !
	- Die Frage, ob das Medium überschrieben werden soll, mit "Ja" beantworten.
	- Passwort eingeben.

	- Neustart bestätigen und "alt" - Taste gedrückt halten, um in das Boot-Menü zu kommen.
	- Dort "EFI Boot" aus dem Menü auswählen und den Schritten nach "Install MacOS *version*" folgen.

	- Installationsassistenten folgen (auf installieren klicken),
	- die Installation kann einige Zeit in Anspruch nehmen und der Bildschirm kann den  Anschein haben, eingefroren zu sein, obwohl der Vorgang im Hintergrund weiter läuft.


SEHR WICHTIG:
	Den USB-Stick NICHT entfernen !


---------------------------------------------------------------------------------------------------------------------------------------------


4. Überprüfung

	- Nach der Installation prüfen, ob diese erfolgreich war:
	- Dafür auf "über diesen Mac" klicken und Software Version prüfen.


---------------------------------------------------------------------------------------------------------------------------------------------


5. OpenCore nun auf der internen Festplatte installieren

	- Nun das kann das Popup beachtet werden (auf OK klicken),
	- dann "Install to disk" klicken,
	- das Apple Speichermedium auswählen.

	- Neustart bestätigen und "alt" - Taste gedrückt halten, um in das Boot-Menu zu kommen.

	- Im Boot Menü "EFI-Boot" mit dem Flash-Speicher Symbol auswählen und booten.



	- Der USB-Stick kann nun entfernt werden !


---------------------------------------------------------------------------------------------------------------------------------------------


6.  (optional)

Bootauswahl (Boot-Picker) abschalten, um direkt ins gewünschte System zu booten.

	- OpenCore legacy Patcher öffnen und in die Einstellungen gehen.
	- Unter "Build" den Hacken bei "Show Boot-Picker" entfernen.
	- Auf "Return" klicken.


- Diese Einstellung anwenden:
	- auf "Build and Install" gehen,
	- erneut rebooten.


---------------------------------------------------------------------------------------------------------------------------------------------
