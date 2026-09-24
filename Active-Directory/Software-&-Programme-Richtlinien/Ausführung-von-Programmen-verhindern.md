# Ausführung bestimmter Programme verhindern - Active Directory

`Anleitung verfasst am 17.12.2025, zuletzt bearbeitet am 7.6.2026`

`Windows-Server - Active Directory`


-------------------------------------------------------------------------------------------------------------


### Gruppenrichtlinienverwaltung öffnen
- `gpmc.msc`
- Neues Gruppenrichtlinienobjekt anlegen
	- Rechtsklick auf `Gruppenrichtlinienobjekt`
	- `neu`
	- Namen vergeben
	- Rechtsklick auf das erstellte Objekt
	- `Bearbeiten`
	- Es sollte sich der Gruppenrichtlinienverwaltungs-Editor öffnen.
- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` > `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen.


-------------------------------------------------------------------------------------------------------------


# Angegebene Windows-Anwendungen nicht ausführen
- Im Gruppenrichtlinienverwaltungs-Editor
    - `Benutzerkonfiguration > Administrative Vorlagen > System`
    - `Angegebene Windows-Anwendungen nicht ausführen` -> Aktiviert
    - Wert: `Programm.exe`
    - Bei den Werten müssen die genauen Namen der ausführbaren Dateien angegeben werden.


-------------------------------------------------------------------------------------------------------------


# Hinweis zu Autostarts
- Falls sich ein Programm im Autostart befindet und auf die Liste der Programme gesetzt wird, die nicht ausgeführt werden dürfen, dann wird bei einem Neustart immer eine Fehlermeldung mit "Der Vorgang wurde aufgrund von aktuellen Beschränkungen auf dem Computer abgebrochen" erscheinen. 
- Man müsste für jeden Benutzer den Autostart deaktivieren, damit diese Fehlermeldung nicht mehr erscheinen würde.



# Beispiel Programme dessen Ausführung verhindert werden könnte:


## 1. Pfad finden, in dem eine Ausführbare Datei liegt - Desktop Icon
- Rechtsklick auf das Desktop Icon / Verknüpfung des entsprechenden Programms
- `Eigenschaften`
- Unter `Verknüpfung` > `Ziel` liegt der Pfad und am Ende des Pfades ist der Programmname zu finden.


## 2. Pfad finden, in dem eine Ausführbare Datei liegt - Terminal
- Das entsprechende Programm ganz normal starten/öffnen.
- GGf. Name des ausgeführten Programms im Taskmanager prüfen.
- Terminal (PowerShell) öffnen und folgenden Befehl einfügen:
    - Den Platzhalter mit dem entsprechenden Namen des Programms, welches geöffnet ist ersetzen:
```
$ Get-Process -Name "NAME-DES-PROGRAMMS" | Select-Object Path
```
- z.B.
```
$ Get-Process -Name "Programm-xyz" | Select-Object Path
$ Get-Process -Name "Copilot" | Select-Object Path
$ Get-Process -Name "M365Copilot" | Select-Object Path
$ Get-Process -Name "mscopilot" | Select-Object Path
$ Get-Process -Name "mscopilot_proxy.exe" | Select-Object Path
$ Get-Process -Name "msedge" | Select-Object Path
$ Get-Process -Name "PhoneExperienceHost" | Select-Object Path
```


-------------------------------------------------------------------------------------------------------------


## Beispielübersicht mit Dateinamen und Pfaden

### Microsoft/Windows Programme
- [Smartphone-Link](https://www.microsoft.com/de-de/windows/sync-across-your-devices?r=1):
    - Programm: `PhoneExperienceHost.exe`
    - Pfad: C:\Program Files\WindowsApps\Microsoft.YourPhone_1....\
    - WICHTIG: Da der Autostart von Smartphone-Link standardmäßig bei Windwows aktiv ist, wird bei einem Neustart immer eine Fehlermeldung mit "Der Vorgang wurde aufgrund von aktuellen Beschränkungen auf dem Computer abgebrochen" erscheinen. Man müsste für jeden Benutzer den Autostart deaktivieren, damit diese Fehlermeldung nicht mehr erscheinen würde.

### KI-Chatbots
- [ChatGPT Desktop App](https://apps.microsoft.com/detail/9nt1r1c2hh7j?hl=de-DE&gl=DE):
    - Programm: `chatgpt.exe`
    - Pfad: C:\Users\BENUTZERNAME\AppData\Local\Microsoft\WindowsApps\

- [Copilot Desktop App (MS-Store)](https://apps.microsoft.com/detail/9nht9rb2f4hd?hl=de-DE&gl=DE):
    - Programm: `Copilot.exe`
    - Pfad: C:\Program Files\WindowsApps\Microsoft.Copilot_.....\
    
- [M365 Copilot (vorinstalliert)](https://apps.microsoft.com/detail/9nht9rb2f4hd?hl=de-DE&gl=DE):
    - Programm: `M365Copilot.exe`
    - Pfad: C:\Program Files\WindowsApps\Microsoft.MicrosoftOfficeHub_.....\

- [Perplexity Desktop App](https://apps.microsoft.com/detail/xp8jnqfbqh6pvf?hl=de-DE&gl=DE):
    - Programm: `perplexity.exe`
    - Pfad: C:\Users\BENUTZERNAME\AppData\Local\Microsoft\WindowsApps\


### Browser von KI-Unternehmen
- [SigmaOS](https://sigmaos.com/): Stand Dezember2025 nur auf MacOS verfügbar
- [ChatGPT Atlas](https://chatgpt.com/de-DE/atlas/): Stand Dezember2025 nur auf MacOS verfügbar

- [Perplexity Comet](https://www.perplexity.ai/comet):
    - Programm: `comet.exe`
    - Pfad: C:\Users\BENUTZERNAME\AppData\Local\Perplexity\Comet\Application\

- [Arc Browser](https://arc.net/): 
    - Programm: `Arc.exe`
    - Pfad: C:\Program Files\WindowsApps\TheBrowserCompany.Arc_....\

### Andere Browser
- [Opera](https://www.opera.com/de/opera):
    - Programm: `opera.exe`
    - Pfad: C:\Users\BENUTZERNAME\AppData\Local\Programs\Opera\
    - Dateiname des Installationspaket: `OperaSetup.exe`

- [OperaGX](https://www.opera.com/de/gx):
    - Programm: `opera.exe`
    - Pfad: C:\Users\BENUTZERNAME\AppData\Local\Programs\Opera GX\
    - Dateiname des Installationspaket: `OperaGXSetup.exe`

- [Microsoft Edge](https://www.microsoft.com/en-us/edge/?form=MA13FJ&ch=1):
    - Programm: `msedge.exe`
    - Pfad: C:\Program Files (x86)\Microsoft\Edge\Application\
    - Dateiname des Installationspaket (MS-Enterprise): `MicrosoftEdgeEnterpriseX64.msi`


-------------------------------------------------------------------------------------------------------------

