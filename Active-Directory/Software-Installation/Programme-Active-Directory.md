# Programminstallation - Active Directory (Domäne)

`Anleitung erstellt am 18.2.2025`

`Windows-Server - Active Directory`


- Voraussetzungen
    - Das Installationspaket des Programms muss im `.msi-Format` sein.
    - exe-Pakete sind `nicht` direkt möglich.

- Skriptbasierte-Installation von MSI/EXE Paketen über ActiveDirectory
	- Wenn MSI oder EXE Pakete zur Installation angeboten werden sollen, die nicht direkt über AD bereitgestellt werden können, kann die [Skriptbasierte-Installation]() verwendet werden.

------------------------------------------------------------------------------------------------------------------------------------------------------------------


# Automatische Installation / Software-Angebot von Programmen über Active Directory

## 1. Automatische Installation von Programmen (Computerrichtlinie)
- Auf den Active-Directory-Windows-Server als Administrator einloggen.
- Entsprechendes MSI-Paket des Programmes herunterladen

- Variante neuer Ordner:
    - Neuen Ordner erstellen und MSI-Paket einfügen
    - `Eigenschaften` des Ordners wählen
    - `Freigabe`, `Erweiterte Freigabe` `Diesen Ordner freigeben`
    - `Übernehmen` `OK`
    - Netzwerkpfad kopieren

- Variante bestehender Ordner:
    - unter `C:\software-angebot` MSI-Paket einfügen
    - `Eigenschaften` des Ordners wählen
    - Netzwerkpfad kopieren

- `Server-Manager` öffnen
    - `Alle Server` in der linken Navigationsleiste wählen.
    - `AD-Server` auswählen
    - `Tools`
    - `Gruppenrichtlinienverwaltung`
    - Nun sollte sich ein neues Fenster öffnen.

- `Gruppenrichtlinienobjekte` in der `Gruppenrichtlinienverwaltung`
    - `Gruppenrichtlinienobjekte` wählen
    - `Neu`
    - Namen vergeben
    - Rechtsklick auf das neue Gruppenrichtlinienobjekt und auf `bearbeiten` klicken
    - Es öffnet sich der `Gruppenrichtlinienverwaltungs-Editor`
    - `Computerkonfiguration`, `Richtlinien`, `Softwareeinstellungen`
    - Rechtsklick auf `Softwareinstallation`
    - `Eigenschaften`
    - Netzwerk-Pfad einfügen (\\SERVER\name-des-ordners)
    - `Zuweisen` auswählen
    - `Übernehmen`, `OK`
    - Erneut Rechtsklick auf `Softwareinstallation`
    - `Neu`, `Paket`
    - Installationspaket auswählen

- zurück zur `Gruppenrichtlinienverwaltung`
    - Unter `Domain.local` -> `Domäne` -> `Computer` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
    - Zum Verknüpfen das gewünschte Objekt auswählen

- Fertig

- In der [CMD](https://de.wikipedia.org/wiki/Cmd.exe) / [PowerShell](https://de.wikipedia.org/wiki/PowerShell) die Gruppen- & Benutzerverwaltung auf den PCs (Clients) aktualisieren
```
$ gpupdate /force
```

- Zum Installieren von Updates bei Programmen, die keinen eigenen Updater haben/ oder bei Programmen, wo gewünscht ist, dass das Update durch die Active Directory erfolgt, zu `Punkt 5. Updates` scrollen.
- Dabei ist es wichtig, dass die Computerrichtlinie mit der alten Programmversion NICHT entfernt wird, sondern bestehen bleibt !


------------------------------------------------------------------------------------------------------------------------------------------------------------------


## 2. Installation von Programmen anbieten (Benutzerrichtlinie)
- Auf den Active-Directory-Windows-Server als Administrator einloggen.
- entsprechendes MSI-Paket des Programmes herunterladen

- Variante neuer Ordner
    - Neuen Ordner erstellen und MSI-Paket einfügen
    - `Eigenschaften` des Ordners wählen
    - `Freigabe`, `Erweiterte Freigabe` `Diesen Ordner freigeben`
    - `Übernehmen` `OK`
    - Netzwerkpfad kopieren

- Variante bestehender Ordner
    - Unter `C:\software-angebot` MSI-Paket einfügen
    - `Eigenschaften` des Ordners wählen
    - Netzwerkpfad kopieren

- `Server-Manager` öffnen
    - `Alle Server` in der linken Navigationsleiste wählen.
    - `AD-Server` auswählen
    - `Tools`
    - `Gruppenrichtlinienverwaltung`
    - Nun sollte sich ein neues Fenster öffnen.

- `Gruppenrichtlinienobjekte` in der `Gruppenrichtlinienverwaltung`
    - `Gruppenrichtlinienobjekte` wählen
    - `Neu`
    - Namen vergeben
    - Rechtsklick auf das neue Gruppenrichtlinienobjekt und auf `bearbeiten` klicken
    - Es öffnet sich der `Gruppenrichtlinienverwaltungs-Editor`
    - `Benutzerkonfiguration`, `Richtlinien`, `Softwareeinstellungen`
    - Rechtsklick auf `Softwareinstallation`
    - `Eigenschaften`
    - Netzwerk-Pfad einfügen (\\SERVER\name-des-ordners)
    - `Veröffentlichen` auswählen
    - `Übernehmen`, `OK`
    - Erneut Rechtsklick auf `Softwareinstallation`
    - `Neu`, `Paket`
    - Installationspaket auswählen

- zurück zur `Gruppenrichtlinienverwaltung`
    - Unter `Domain.local` -> `Domäne` -> `Benutzer` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
    - Zum Verknüpfen das gewünschte Objekt auswählen

- Fertig

- In der CMD / PowerShell die Gruppen- & Benutzerverwaltung auf den PCs (Clients) aktualisieren
    - nur für Clients in Active Directory, NICHT für den Server !
```
$ gpupdate /force
```

- Angewendete Gruppenrichtlinienobjekte prüfen
```
$ gpresult /R
```

### Namen angezeigter Programmname in der Systemsteuerung anpassen
- Öffnen der Gruppenrichtlinienverwaltung
- Zu `Benutzerkonfiguration` → `Richtlinien` → `Softwareeinstellungen` → `Softwareinstallation`
- `Doppelklick` auf das entsprechende MSI-Paket
- Zur Registerkarte `Allgemein` wechseln
- Namen ändern
- Zum Speichern `Übernehmen` `OK`
- GGf. auf einem Client ausführen: `$ gpupdate /force` und Namen in der Systemsteuerung prüfen


------------------------------------------------------------------------------------------------------------------------------------------------------------------


# 3. Falls eine Windows-Version ausgeschlossen wird / werden soll - WMI-Filter

### Einen neuen WMI-Filter anlegen
- `Server-Manager` öffnen
    - `Alle Server` in der linken Navigationsleiste wählen.
    - `AD-Server` auswählen
    - `Tools`
    - `Gruppenrichtlinienverwaltung`
    - Nun sollte sich ein neues Fenster öffnen.

- `WMI-Filter` in der `Gruppenrichtlinienverwaltung`
    - Rechtsklick auf `WMI-Filter`
    - `Neu`
    - Namen vergeben
    - Auf `Hinzufügen` klicken
    - Es öffnet sich ein neues Fenster.
    - Nun in das Abfragefeld den entsprechenden Code einfügen.
    - Für (NUR) Windows11 Clients wäre das `SELECT * FROM Win32_OperatingSystem WHERE Version LIKE "10.%" AND ProductType = 1 AND BuildNumber >= 22000`
    - Für  Windows11 & Windows10 Clients wäre das `SELECT * FROM Win32_OperatingSystem WHERE Version LIKE "10.%" AND ProductType = "1" AND BuildNumber >= "19041"`
    - `OK`
    - `Speichern`

 - GPO mit dem neuen WMI-Filter verknüpfen
    - In der Gruppenrichtlinienverwaltung zu `Gruppenrichtlinienobjekte` gehen
    - Betroffene Richtlinien (GPO) auswählen
    - Im `Bereich WMI-Filterung` den gewünschten Filter auswählen.
    - `OK`

------------------------------------------------------------------------------------------------------------------------------------------------------------------


# 4. Freigabe vom Pfad des Installationspaketes - NTFS-Freigabe
- Überprüfen, ob Berechtigungen korrekt sind
    - Datei-Explorer öffnen
    - In die Leiste, wo der Pfad ist, den Pfad des Ordners einfügen: `SERVER\ORDNER`
    - Wenn eine Fehlermeldung im Browser erscheint, liegt wahrscheinlich ein Berechtigungsfehler vor.
    - Wenn sich hingegen der entsprechende Ordner des Installationspakets öffnet, sind die Berechtigungen korrekt.

- Berechtigungen anpassen
    - Auf dem Active-Directory-Windows-Server als Administrator einloggen.
    - Den entsprechenden Ordner des MSI-Installationspaketes im Explorer öffnen
    - `Eigenschaften` des Ordners wählen
    - Zum Reiter `Sicherheit`
    - Prüfen, ob unter `Gruppen-&-Benutzernamen` `Jeder` enthalten ist.
    - Wenn ja, prüfen, ob die Berechtigung `Lesen` gesetzt ist.
    - Wenn nein, dann auf `Bearbeiten` klicken
    - Im neu geöffneten Fenster unter `verwendenden Objektnamen` `Jeder` einfügen, Suchpfad kann leer bleiben oder beim Standard belassen werden, Objekttyp ebenfalls beim Standard belassen.
    - `Nemen überprüfen`
    - `OK`
    - `Lese-Berechtigung` setzten
    - Bestätigen und `übernehmen`
    - `OK`


------------------------------------------------------------------------------------------------------------------------------------------------------------------


# 5. Updates über Active Directory

- Zum Installieren von Updates bei Programmen, die keinen eigenen Updater haben/ oder bei Programmen, wo gewünscht ist, dass das Update durch Active Directory erfolgt.
- Dabei ist es wichtig, dass die Computerrichtlinie mit der alten Programmversion NICHT entfernt wird, sondern bestehen bleibt !
- Falls die Computerrichtlinie doch entfernt wurde, wird hier auch erklärt, wie man das beheben kann.


### Wieso ist das Behalten der Computerrichtlinie mit der alten Programmversion zunächst wichtig ?
- Ein direktes Upgrade durch eine neue GPO ist nicht möglich, weil Windows keinen Bezug zur alten Installation mehr hat und somit kein Update durchgeführt wird.


### Update über Active Directory (aktualisieren der Computerrichtlinie auf neue Version)

- vorhandene GPO öffnen:
	- Gruppenrichtlinienverwaltung öffnen
	- Zur entsprechenden Computerrichtlinie navigieren
	- `Rechtsklick` auf die GPO und mit `Bearbeiten` den Gruppenverwaltungs-Editor öffnen
	- `Computerkonfiguration` → `Richtlinien` → `Softwareeinstellungen` → `Softwareinstallation`

- `Rechtsklick` auf das bestehende MSI-Paket.
	- Reiter `Aktualisierungen` auswählen
	- Hinzufügen
	- Neues MSI-Paket (Update-Paket) auswählen
	- `Haken` bei `Bestehendes Paket deinstallieren. Aktualisierungspaket installieren`

```
$ gpupdate /force
```
- Clients ggf. neu starten




### Neuinstallation von Programm mit aktueller Version (alte Computerrichtlinie wurde gelöscht)
- Falls die Computerrichtlinie entfernt wurde und ein Update des Programms installiert werden soll, muss eine neue GPO für das Update erstellt werden, in der das Programm zunächst deinstalliert und danach die neue Version installiert wird.
- Zunächst sollte sichergestellt werden, dass das Vorgehen hier nötig ist und nicht durch `$ gpupdate /force` bereits behoben werden kann.

- Neue GPO erstellen:
	- Gruppenrichtlinienverwaltung öffnen
	- Vorgehensweise aus `Punkt 1. automatische Installation von Programmen (Computerrichtlinie)`
	- Mit Verknüpfung bis zum nächsten Punkt warten.

- Sicherstellen, dass die alte Version deinstalliert wird:
	- Unter `Softwareinstallation` → `Rechtsklick auf das neue Paket` → `Eigenschaften`
	- Reiter `Aktualisierungen` → `Haken` bei `Vorhandene Pakete aktualisieren` setzen
	- `Hinzufügen`, die alte Version auswählen, falls diese noch gelistet ist und `Haken` bei `Bestehendes Paket deinstallieren. Aktualisierungspaket installieren`
	- `OK`
	- `Übernhemen`
	- `OK`

- `Verknüpfen` der GPO mit der OU, in der die Computer sind:
	- Zurück zur `Gruppenrichtlinienverwaltung`
    	- Unter `Domain.local` -> `Domäne` -> `Computer` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
    	- Richtlinie auswählen

```
$ gpupdate /force
```
- Clients ggf. neu starten


------------------------------------------------------------------------------------------------------------------------------------------------------------------
