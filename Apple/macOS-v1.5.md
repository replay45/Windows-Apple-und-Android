# MacOS


## Inhaltsverzeichnis

### 1. [SIP (System Integrity Protection)](https://support.apple.com/de-de/102149) ein-/ ausschalten
### 2. Dateien/Ordner auf MacOS über das Terminal löschen
### 3. Systemdateien in [MacOS Finder](https://de.wikipedia.org/wiki/Finder_(Mac)) anzeigen lassen
### 4. Icons von MacOS Apps und Ordnern ändern
### 5. [Home Brew](https://brew.sh/)


----------------------------------------------


# 1. [SIP (System Integrity Protection)](https://support.apple.com/de-de/102149) ein-/ ausschalten

### Intel-Mac:


### 1.1. In den Wiederherstellungsmodus gelangen

- a) Über einen Neustart:
	- Den Mac ausschalten,
	- Ein/Aus-Taste drücken und `Befehl-R` gedrückt halten,
	- warten, bis das Apple-Logo erscheint und dann `Befehl-R` los lassen.
	- Nun sollte das Fenster macOS-Dienstprogrammen zu sehen sein.


- b) Über das Terminal:

```
$ sudo nvram "recovery-boot-mode=unused
```
```
$ sudo reboot recovery
```




### 1.2. SIP deaktivieren:

- Über die obere Leiste auf "Dienstprogramme" klicken und das Terminal öffnen.
- Nun den folgenden Befehl im Terminal einfügen:

```
$ csrutil disable
```

- Mac neu starten.




### 1.3. Status prüfen

Terminal auf dem Desktop öffnen und Befehl eingeben:

```
$ csrutil status
```



### 1.4. SIP wieder aktivieren:

- erneut in den Wiederherstellungsmodus und das Terminal öffnen.
- Dann folgenden Befehl im Terminal einfügen:

```
$ csrutil enable
```

- Mac neu starten.


---------------------------------------------------------------------------------------------


# 2. Dateien/Ordner auf MacOS über das Terminal löschen

Terminal öffnen und Befehl eingeben:

```	
$ rm -rf PFAD-DER-DATEI
```


---------------------------------------------------------------------------------------------


# 3. Systemdateien in [MacOS Finder](https://de.wikipedia.org/wiki/Finder_(Mac)) anzeigen lassen

1.
- Finder öffnen,
- auf `Suche` klicken,
- etwas Beliebiges suchen.

2.
- In der nun erscheinenden Leiste auf `Diesen Mac` klicken,
- dann auf `+`,
- bei `Name` im Drop-down-Menu zu `Andere` wechseln,
- nun in der Suche des neuen Fensters nach `Systemdateien` suchen,
- und den Haken setzen,
- auf `OK` klicken.

3.
- Wieder auf `Name` im Drop-down-Menu klicken und `Systemdateien` auswählen.
- Danach im Drop-down-Menu daneben `einschließen` auswählen.
- Nun sollten ebenfalls `versteckte Systemdateien` zu sehen sein.


---------------------------------------------------------------------------------------------


# 4. Icons von MacOS Apps und Ordnern ändern

Das Ändern von Icons von Systemapps ist leider nicht mehr möglich, da  die Systemapps auf einem schreibgeschützten System-Volume installiert sind.
Auch das Mounten des schreibgeschützten Volumes, mit Lese- & Schreibrechten ist nicht mehr möglich.
Daher können die Icons auf neueren MacOS Versionen `ausschließlich bei Drittanbieter-Apps` geändert werden, die 
auf einem `System-Volume mit Schreibrechten` installiert sind.


- Icons auf MacOS sind im `icns` Format.


4.1. `icns` Icons herunterladen:
- [macosicons.com](https://macosicons.com)



4.2. App-Icon ändern:
   - Finder öffnen.
   - `Applications` Ordner aufrufen.
   - Rechtsklick auf eine App und auf `Info` gehen.
   - `icns` Icon auf das zu ersetzende App-Symbol ziehen, bis ein `Plus-Symbol` erscheint.
   - Um die Änderung wirksam zu machen, muss die App ggf. beendet und neu gestartet werden.



4.3. Ordner-Icon ändern:
   - Rechtsklick auf den gewünschten Ordner und auf `Info` gehen.
   - `icns` Icon auf das zu ersetzende App Symbol ziehen, bis ein `Plus-Symbol` erscheint.


4.4. Auf Standard zurücksetzen:
   - `Ordner` auswählen / `Applications` Ordner aufrufen.
   - Rechtsklick auf den gewünschten `Ordner` / Rechtsklick auf die gewünschte `App` und auf `Info` gehen.
   - Auf `Icon` klicken und `Entfernen-Taste` drücken.
   - Um die Änderung wirksam zu machen, muss die App ggf. beendet und neu gestartet werden.


__Hinweis__:
Sollte sich das Icon einer App im Dock nicht updaten, einfach die App aus dem Dock entfernen und erneut hinzufügen.


---------------------------------------------------------------------------------------------


# 5. [Home Brew](https://brew.sh/)

`Paketmanager für Linux und MacOS`

`für die Anleitung verwendetes Betriebssystem: MacOS Sonoma`


## 5.1. Installation:
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


## 5.2. Nutzung:
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


## 5.3. Installieren von Paketen:
```
$ brew install {package name}
```


## 5.4. Deinstallieren von Paketen:
```
$ brew uninstall {package name}
```


## 5.5. Um GUI Apps installieren zu können:
```
$ brew install cask
```


## 5.6. Apps aus dem Apple App-Store über das Terminal installieren über mas:
```
$ brew install mas
```


## 5.7. Das beste Dateimanagement im Terminal:
```
$ brew install midnight-commander
```
```
$ sudo mc
```


---------------------------------------------------------------------------------------------
