# Windows


## Inhaltsverzeichnis
1. lokalen Windows 11 Benutzer erstellen - Kontozwang umgehen
2. Die Adminabfrage UAC bei einer Installation eines Programms umgehen
3. Cortana über [PowerShell](https://de.wikipedia.org/wiki/PowerShell) deinstallieren
4. Copilot von Windows 11 deinstallieren
5. Raster auf dem Desktop - Icon Abstände verändern
6. Erstellen eines Systemwiederherstellungspunkts unter Windows 11
7. Schnellstart bei Windows deaktivieren
8. Dienste installierter Programme auf Windows überprüfen
9. Einen USB-Stick zur Windows-Anmeldung nutzen
10. Nutzer manuell für Remote-Desktop (RDP) erlauben ([Terminal](https://de.wikipedia.org/wiki/Windows_Terminal))
11. Usernamen eines lokalen-Benutzers unter Win11 ändern (PowerShell)
12. Microsoft Edge auf Windows 10 deinstallieren


-----------------------------------------------------------------------------


# 1. lokalen Windows 11 Benutzer erstellen - Kontozwang umgehen

`Anleitung verfasst am 20.6.2024`

`Windows Version: Win11 23H2`


# A. Windows 11 Pro

- Bei der Ersteinrichtung des PCs in dem Ersteinrichtungsassistenten unter `Wie möchten Sie dieses Gerät einrichten?` auf `Für Arbeit oder Schule/Uni einrichten` klicken, um ein lokales Konto erstellen zu können.
- Nun anstatt mit einem Konto sich anzumelden, auf `Anmeldeoptionen` gehen und `Stattdessen der Domäne beitreten` auswählen (Es ist nicht nötig einer Domäne beizutreten, die Option ein lokales Konto anzulegen ist lediglich hinter diesem Punkt versteckt).
- Jetzt einfach ein Benutzername vergeben und ein Passwort wählen. Danach wie gewohnt die Sicherheitsfragen beantworten und die Datenschutzoptionen setzen.
(Tipp: Bei den Datenschutzoptionen am besten überall "Nein" auswählen.)
- Sollten diese `Optionen nicht mehr verfügbar sein` zu `Punkt B "Windows 11 Home"` oder `ab Win11 25H2 direkt zu Punkt C` wechseln


# B. Windows 11 Home

- Internetverbindung trennen (Ethernet Kabel trennen / WLAN Verbindung gar nicht erst herstellen).
- Bei Windows 11 Home ist ein anderes Vorgehen als bei Windows 11 Pro nötig, da die Home-Versionen keinen Zugang zu einer Domäne ermöglichen.
- Bei der Ersteinrichtung des PCs in dem Ersteinrichtungsassistenten `SHIFT + F10` drücken (auf Notebooks könnte das drücken der FN-Taste zusätzlich nötig sein), um das Terminal zu öffnen.
- Sollte diese Anletung nicht mehr funktionieren, dann bitte zu Punkt C scrollen.

- Folgendes in das Terminal eingeben:
```
$ oobe\BypassNRO.cmd
```

Sollte der Befehl nicht funktionieren, kann alternativ der folgende Befehl genutzt werden:
```
$ oobe\BypassNRO
```

- Einrichtungsassistenten folgen und bei dem Punkt `Netzwerk verbinden` auf `Ich habe kein Internet` klicken.

- Danach `Mit eingeschränkter Ersteinrichtung fortfahren` auswählen.

- Jetzt einfach ein Benutzername vergeben und ein Passwort wählen. Danach wie gewohnt die Sicherheitsfragen beantworten und die Datenschutzoptionen setzen.
(Tipp: Bei den Datenschutzoptionen am besten überall "Nein" auswählen.)




# C. Sollten Punkt A oder Punkt B nicht mehr funktionieren:
- Falls Punkt A oder B nicht mehr funktionieren sollten (z.B. ab Win11 25H2), dann kann die folgenden Anleitung genutzt werden.


### Alternative Möglichkeiten zur Erstellung eines lokalen Kontos:
- Bei der Aufforderung zum Microsoft-Konto `SHIFT + F10` drücken (auf Notebooks könnte das drücken der FN-Taste zusätzlich nötig sein), um das Terminal zu öffnen.
- folgenden Befehl eingeben:
```
$ start ms-cxh://setaddlocalonly
```
- Enter
- es öffnet sich ein neues Fenster, in dem man nun ein lokales Konto einrichten kann.


-----------------------------------------------------------------------------


# 2. Die Adminabfrage (UAC) bei einer Installation eines Programms umgehen

- Hinweis
	- Diese Anleitung wurde unter Windows 10 getestet !
	- Außerdem hat Microsoft Updates veröffentlich, sodass diese Methode möglicherweise unbrauchbar wird.

- Adminabfrage (UAC) umgehen
	- Wenn man als Benutzer auf Windows auf dem üblichen Weg ein Programm über eine .exe installieren möchte, benötigt man Administratorrechte.
	- Wenn man keine Administratorrechte hat, erscheint eine Abfrage (UAC), wo man gebeten wird, die Installation als Administrator zu bestätigen.
	- Hier wird gezeigt, wie man diese umgehen kann und eine exe-Datei ausführen kann, um ein Programm für den Benutzer zu installieren.

### Adminabfrage umgehen
- exe-Installationsdatei herunterladen
- Neue Textdatei anlegen.
- Folgendes in eine Textdatei einfügen:
```
Set __COMPAT_LAYER=RunAsInvoker
HIER_DER_NAME_DER_SETUP_DATEI.exe
```

- `HIER_DER_NAME_DER_SETUP_DATEI` mit dem Dateinamen des Installationspakets ersetzen.
- Datei speichern und Text-Editor schließen.
- Dateiendung in `.bat` ändern, damit die Datei ein ausführbares Skript wird.
- `Datei.bat` mit einem Doppelklick öffnen.
- Nun sollte sich der Installationsassistenten des Programms öffnen.


-----------------------------------------------------------------------------


# 3. Cortana über [PowerShell](https://de.wikipedia.org/wiki/PowerShell) deinstallieren

## Den Sprachassistenten [Cortana](https://support.microsoft.com/de-de/topic/was-ist-cortana-953e648d-5668-e017-1341-7f26f7d0f825), per PowerShell vollständig entfernen:


- In die Windows-Suche `PowerShell` eigeben und als `Administrator` öffnen.

- Hier nun hinter der Information zum System (z.B.” \system32>”) den folgenden Befehl eingeben:
```
$ Get-AppxPackage -allusers Microsoft.549981C3F5F10 | Remove-AppxPackage
```

- Bestätigen mit der Enter-Taste – "Cortana" wird daraufhin für alle Benutzer des PCs deinstalliert.

- Es erscheint kurz eine grün hinterlegte Statusmeldung, die anzeigt, dass Powershell arbeitet.
Danach erscheint wieder die vorherige Anzeige.

- "Cortana" ist nun erfolgreich deinstalliert.


-----------------------------------------------------------------------------


# 4. Copilot von Windows 11 deinstallieren

## Den Microsoft [Copilot](https://copilot.microsoft.com/) von Windows 11 deinstallieren:

Diese Anleitung ist für die Windows 11 23H2 und höher geeignet.


- In die Windows-Suche `PowerShell` eigeben und als `Administrator` öffnen.

- Hier nun den folgenden Befehl eingeben.

Für `ALLE Benutzerkonten` Copilot deinstallieren:
```
$ Get-AppxPackage -AllUsers -Name "Microsoft.Windows.Ai.Copilot.Provider" | Remove-AppxPackage
```
oder

Für den `aktuellen Benutzer` Copilot deinstallieren:
```
$ Get-AppxPackage -Name "Microsoft.Windows.Ai.Copilot.Provider" | Remove-AppxPackage
```

- Bestätigen mit der Enter-Taste – "Copilot" wird daraufhin für alle Benutzer des PCs deinstalliert.

- Es erscheint kurz eine grün hinterlegte Statusmeldung, die anzeigt, dass Powershell arbeitet.
Danach erscheint wieder die vorherige Anzeige.

- "Copilot" ist nun erfolgreich deinstalliert.


-----------------------------------------------------------------------------


# 5. Raster auf dem Desktop - Icon Abstände verändern

- `regedit` öffnen

- Pfad einfügen:
```
HKEY_CURRENT_USER\Control Panel\Desktop\WindowMetrics
```

- Die Werte `IconSpacing` und `IconVerticalSpacing` nun anpassen.

- Standartgröße ist `-1125`

- Um Abstand zu verringern einen kleineren negativen Wert eingeben (z.B. -1000) und um den Abstand zu vergrößern einen größeren negativen Wert eintragen (z.B. -1200).

- Damit die Änderungen wirksam werden, Benutzer `abmelden` und erneut anmelden.


-----------------------------------------------------------------------------


# 6. Erstellen eines Systemwiederherstellungspunkts unter Windows 11

- In das Suchfeld auf der Taskleiste `Wiederherstellungspunkt erstellen` eingeben.
- Enter
- Nun in den Systemeigenschaften zur Registerkarte `Computerschutz` die Option `Erstellen` auswählen.
- Eine kurze Beschreibung einfügen und auf `Erstellung` klicken.
- Um die automatische Sicherung einzuschalten, auf `Konfigurieren` gehen.
- Dabei sicherstellen, dass das richtige Speichermedium ausgewählt wurde.
- Nun die gewünschten Speicher-Einstellungen treffen, auf `Computerschutz aktivieren` klicken und Einstellungen übernehmen.


Sollten zukünftig Probleme mit Windows auftreten, ist es nun möglich, in den `Erweiterten Startoptionen` auf einen erstellten Systemwiederherstellungspunkt zurückzukehren.


-----------------------------------------------------------------------------


# 7. Schnellstart bei Windows deaktivieren

## Was ist der Schnellstart ?

Der Schnellstart ist eine Funktion in Windows, die beim Herunterfahren ein Image des [RAMs](https://de.wikipedia.org/wiki/Random-Access_Memory) auf den Massenspeicher schreibt.
Beim nächsten Start des PCs wird dieses Abbild in den RAM geladen, was den Boot-Vorgang beschleunigt.


## Wieso sollte man ihn deaktivieren ?

Der Schnellstart kann die Fehleranalyse erschweren, da der RAM nur durch einen vollständigen Neustart komplett zurückgesetzt wird, was für eine Fehlerbehebung notwendig ist.
Wenn man also Fehlerquellen vermeiden möchte, kann man den Schnellstart deaktivieren.


## Wie deaktiviert man den Schnellstart ?

- `Systemsteuerung` öffnen
- sicherstellen, dass die Ansicht auf `Große Symbole` oder `Kleine Symbole` eingestellt ist
- Zu den `Energieoptionen` navigieren
- Einstellungen für das Herunterfahren ändern
- Auf `Einige Einstellungen sind momentan nicht verfügbar.` klicken
- Schnellstart deaktivieren
- `Änderungen speichern`


-----------------------------------------------------------------------------


# 8. Dienste installierter Programme auf Windows überprüfen

- Systemkonfiguration
	- In die Suche `Systemkonfiguration` eingeben und mit Enter bestätigen.
	- Zu dem Reiter `Dienste` wechseln,
	- Windows/Microsoft Dienste sollten immer laufen, da diese essenziell für das Betriebssystem sind/ sein könnten.
	- Daher kann einfach der Haken bei `Alle Microsoft-Dienste ausblenden` gesetzt werden.
	- Nun können nach Bedarf Dienste aktiviert/deaktiviert werden.


Für weniger erfahrene Nutzer, empfiehlt es sich, unbekannte Dienste NICHT zu deaktivieren, da dies zu Problemen führen könnte.


-----------------------------------------------------------------------------


# 9. Einen gewöhnlichen USB-Stick als Schlüssel zur Windows-Anmeldung nutzen:

## Dafür kann z.B. das Tool [USB-LOGON](https://usblogon.quadsoft.org/de/) verwendet werden.

Ein handelsüblicher USB-Stick kann zu einem Schlüssel, für die Anmeldung an einem Windows PC konfiguriert werden.
Nach der Konfiguration kann der USB-Stick als alternative Anmeldemethode zum Passwort in Windows verwendet werden.

Zudem kann eingestellt werden, ob beim Einsetzen des USB-Sticks zusätzlich ein Passwort abgefragt werden soll, oder das Einsetzen des konfigurierten USB-Sticks ausreicht.
Außerdem kann separat eingestellt werden, was passieren soll, wenn der USB-Stick entfernt wird.


-----------------------------------------------------------------------------


# 10. Nutzer manuell für Remote-Desktop (RDP) erlauben ([Terminal](https://de.wikipedia.org/wiki/Windows_Terminal))

`Anleitung verfasst am 10.6.2025`

`getestete Windows Version: Win11 24H2`

- Dafür `Terminal` als `Admin` öffnen oder als Admin in Windows anmelden und Terminal öffnen.
- Systemsprache püfen und entsprechnden Befehl nutzen oder Gruppenname anzeigen lassen und Befehl ggf. anpassen.


### Befehle
- Systemsprache auf `Englisch`:
```
$ net localgroup "Remote Desktop Users" "domäne\username" /add
```
- Systemsprache auf `Deutsch`:
```
$ net localgroup "Remotedesktopbenutzer" "domäne\username" /add
```


### Optional: Gruppennamen anzeigen lassen
- [Terminal](https://de.wikipedia.org/wiki/Windows_Terminal):
```
$ net localgroup
```

- [PowerShell](https://de.wikipedia.org/wiki/PowerShell):
```
$ Get-LocalGroup
```

### Benutzer aus Remote Desktop Gruppe wieder entfernen
- Systemsprache auf `Deutsch`:
```
$ net localgroup "Remotedesktopbenutzer" "domäne\username" /delete
```


-----------------------------------------------------------------------------


# 11. Usernamen eines lokalen-Benutzers unter Win11 ändern (PowerShell)

`Anleitung verfasst am 11.9.2025`

`getestet auf  Windows 11 24H2`


### Benutzernamen eines loakeln Windowsbenutzers ändern
- Poweshell als Administrator öffnen
- Folgenden Befehl verwenden:
```
$ Rename-LocalUser -Name "alterBenutzername" -NewName "neuerBenutzername"
```
- Die Platzhalter "alterBenutzername" und "neuerBenutzername" entsprechend ersetzen.
- Nun Abmelden und als der Benutzer mit dem neuen Namen anmelden.
- Um lokale Benutzer anzeigen zu lassen `$ Get-LocalUser` verwenden


### Passwort eines loakeln Windowsbenutzers ändern
- Poweshell als Administrator öffnen
- Folgenden Befehl verwenden:
```
$ net user BENUTZERNAME NEUESPASSWORT
```
- Die Platzhalter "BENUTZERNAME" und "NEUESPASSWORT" entsprechend ersetzen.
- Nun Abmelden und mit dem neuen Passwort anmelden.
- Um lokale Benutzer anzeigen zu lassen `$ Get-LocalUser` verwenden


-----------------------------------------------------------------------------
