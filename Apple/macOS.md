# MacOS

# SIP (System Integrity Protection) ein-/ ausschalten

### Intel-Mac:


1. In den Wiederherstellungsmodus gelangen

- a) über einen Neustart:
	- den Mac ausschalten
	- Ein/Aus-Taste drücken und Befehl-R gedrückt halten
	- warten, bis das Apple-Logo erscheint und dann Befehl-R los lassen
	- Nun sollte das Fenster macOS-Dienstprogrammen zu sehen sein.


- b) über das Terminal:

	```
	$ sudo nvram "recovery-boot-mode=unused
	```
	```
	$ sudo reboot recovery
	```




2. SIP deaktivieren:

	- über die obere Leiste auf "Dienstprogramme" klicken und das Terminal öffnen
	- nun den folgenden Befehl im Terminal einfügen:

	```
	$ csrutil disable
	```

	- Mac neu starten




3. Status prüfen

	Terminal auf dem Desktop öffnen und Befehl eingeben:

	```
	$ csrutil status
	```



4. SIP wieder aktivieren:

	- erneut in den Wiederherstellungsmodus und das Terminal öffnen
	- dann folgenden Befehl im Terminal einfügen:

	```
	$ csrutil enable
	```

	- Mac neu starten


---------------------------------------------------------------------------------------------


# Dateien/Ordner auf MacOS über das Terminal löschen:

Terminal öffnen

	
	$ rm -rf PFAD-DER-DATEI
	


---------------------------------------------------------------------------------------------


# Systemdateien in macOS Finder anzeigen lassen

1.
- Finder öffnen,
- auf "Suche" klicken,
- etwas Beliebiges suchen.

2.
- In der nun erscheinenden Leiste auf "Diesen Mac" klicken,
- dann auf "+",
- bei "Name" im Drop-down-Menu zu "Andere" wechseln,
- nun in der Suche des neuen Fensters nach "Systemdateien" suchen,
- und den Haken setzen,
- auf "OK" klicken.

3.
- Wieder auf "Name" im Drop-down-Menu klicken und Systemdateien auswählen.
- Danach im Drop-down-Menu daneben "einschließen" auswählen.
- Nun sollten ebenfalls versteckte Systemdateien zu sehen sein.


---------------------------------------------------------------------------------------------


# Icons von MacOS Apps und Ordnern ändern

Das Ändern von Icons von Systemapps ist leider nicht mehr möglich, da  die Systemapps auf einem schreibgeschützten System-Volume installiert sind.
Auch das Mounten des schreibgeschützten Volumes, mit Lese- & Schreibrechten ist nicht mehr möglich.
Daher können die Icons auf neueren MacOS Versionen ausschließlich bei Drittanbieter-Apps geändert werden, die 
auf einem System-Volume mit Schreibrechten installiert sind.


- Icons auf MacOS sind im ".icns" Format.


1. "icns" Icons herunterladen:
	- [macosicons.com](https://macosicons.com)



2. App-Icon ändern:
	- Finder öffnen.
	- "Applications" Ordner aufrufen.
	- Rechtsklick auf eine App und auf "Info" gehen.
	- "icns" Icon auf das zu ersetzende App-Symbol ziehen, bis ein Plus-Symbol erscheint.
	- Um die Änderung wirksam zu machen, muss die App ggf. beendet und neu gestartet werden.



3. Ordner-Icon ändern:
	- Rechtsklick auf den gewünschten Ordner und auf "Info" gehen.
	- "icns" Icon auf das zu ersetzende App Symbol ziehen, bis ein Plus-Symbol erscheint.


4. Auf Standard zurücksetzen:
	- Ordner auswählen / "Applications" Ordner aufrufen.
	- Rechtsklick auf den gewünschten Ordner / Rechtsklick auf die gewünschte App und auf "Info" gehen.
	- Auf Icon klicken und Entfernen-Taste drücken.
	- Um die Änderung wirksam zu machen, muss die App ggf. beendet und neu gestartet werden.


__Hinweis__:
Sollte sich das Icon einer App im Dock nicht updaten, einfach die App aus dem Dock entfernen und erneut hinzufügen.


---------------------------------------------------------------------------------------------


# Home Brew

### Paketmanager für Linux und MacOS
### Hier verwendetes Betriebssystem: MacOS Sonoma


[Home-Brew](https://brew.sh/)


## 1. Installation:
```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```
$ xcode-select --install
```
```
$ brew doctor
```
```
$ brew analytics off
```


## 2. Nutzung:
```
$ brew doctor
```
```
$ brew list
```
```
$ brew outdated
```
```
$ brew update
```
```
$ brew upgrade
```
```
$ brew cleanup
```


## 3. Installieren von Paketen:
```
$ brew install {package name}
```


## 4. Deinstallieren von Paketen:
```
$ brew uninstall {package name}
```


## 5. Um GUI Apps installieren zu können:
```
$ brew install cask
```


## 6. Apps aus dem Apple App-Store über das Terminal installieren über mas:
```
$ brew install mas
```


## 7. Das beste Dateimanagement im Terminal:
```
$ brew install midnight-commander
```

---------------------------------------------------------------------------------------------





