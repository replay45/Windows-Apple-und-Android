# Standardprogramme setzen - Active Directory

`Anleitung erstellt am 13.6.2025`

`Windows-Server - Active Directory`

`getestet für Windows 11 Pro (24H2) Clients`


-------------------------------------------------------------------------------------------------------------


## Ziel dieser Anleitung
- Ziel ist es Standardprogramme bei der Erstanmeldung eines Active Directory Benutzers zu setzen, z.B. den von der Organisation vorgeschriebenen/empfohlenen Browser.
- Nutzer können die gesetzten Stanardprogramme nach der Anmeldung natürlich in ihrem eigenen Profil ändern.
- Funktioniert auch mit Windows 11 Pro.

## Einschränkungen
- Die Richtlinie wird `nur angewendet`, wenn sich ein `Nutzer das erste Mal` auf dem Client mit seinem Active-Directory-Benutzer `anmeldet` !
- Bei bestehenden Profilen, (auf den Clients im AD) ist diese Richtlinie wirkungslos !


-------------------------------------------------------------------------------------------------------------


### 1. xml-Datei exportieren
- Standardprogramme auf einem Client setzten
- Powershell als Admin öffnen
```
$ Dism /Online /Export-DefaultAppAssociations:C:\StandardApps.xml
```
- Mit dem Befehl werden die gesetzten Standardprogramme exportiert
- Die xml-Datei kann dann unter `C:\` gefunden werden


### 2. xml-Datei ggf. bearbeiten
- xml-Datei mit Editor öffnen und ggf. einige Zeilen löschen, wenn ein gesetztes Programm gar nicht auf allen Clients installiert ist, oder nicht als Standard gesetzt werden soll.
- speichern
- Beispiel XML-Vorlage ist unten zu finden.


### 3. xml-Datei auf Active-Directory-Server speichern
- Die xml-Datei auf dem Active Directory Domain Controler speichern
- Empfohlen: Die xml-Datei in dem SYSVOL Pfad bei dem Skript zu speichern, da dieser Pfad für alle Clients in der Domäne erreichbar ist.
	- Explorer auf dem Domain Controler öffnen
	- folgenden Pfad öffnen bzw. erstellen: `\\Domain-Controler\SYSVOL\Domäne\Policies\Vorlagen`
	- `StandardApps.xml`-Datei nun einfügen


### 4. GPO anlegen
- Gruppenrichtlinienverwaltung auf dem Active Directory Server öffnen
- `gpmc.msc`
- Neues Gruppenrichtlinienobjekt anlegen
	- Rechtsklick auf `Gruppenrichtlinienobjekt`
	- `neu`
	- Namen vergeben
	- Rechtsklick auf das erstellte Objekt
	- `Bearbeiten`
	- Es sollte sich der Gruppenrichtlinienverwaltungs-Editor öffnen.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-komponenten > Datei-Explorer`
	- Richtlinie: `Konfigurationsdatei für Standardzuordnungen festlegen` -> Aktivieren
	- Wert setzen: Pfad zur XML - `\\Domain-Controler\SYSVOL\Domäne\Policies\Vorlagen\StandardApps.xml`

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


### 5. Testen
- Auf einem Client ausführen:
```
$ gpupdate /force
```
- Mit einem "neuen" Active-Directory-Benutzer anmelden, der auf dem Test Client noch nie eingeloggt war, oder temporär einen neuen Benutzer im Active Directory erstellen.
- Prüfen ob entsprechende Programme als Standard gesetzt wurden.


### 6. Beispiel XML-Vorlage
```
<?xml version="1.0" encoding="UTF-8"?>
<DefaultAssociations>
  <Association Identifier=".htm" ProgId="FirefoxHTML-308046B0AF4A39CB" ApplicationName="Firefox" />
  <Association Identifier=".html" ProgId="FirefoxHTML-308046B0AF4A39CB" ApplicationName="Firefox" />
  <Association Identifier=".mht" ProgId="Applications\firefox.exe" ApplicationName="Firefox" />
  <Association Identifier=".mhtml" ProgId="Applications\firefox.exe" ApplicationName="Firefox" />
  <Association Identifier=".pdf" ProgId="FirefoxPDF-308046B0AF4A39CB" ApplicationName="Firefox" />
  <Association Identifier=".shtml" ProgId="FirefoxHTML-308046B0AF4A39CB" ApplicationName="Firefox" />
  <Association Identifier=".svg" ProgId="FirefoxHTML-308046B0AF4A39CB" ApplicationName="Firefox" />
  <Association Identifier=".xht" ProgId="FirefoxHTML-308046B0AF4A39CB" ApplicationName="Firefox" />
  <Association Identifier=".xhtml" ProgId="FirefoxHTML-308046B0AF4A39CB" ApplicationName="Firefox" />
  <Association Identifier=".xml" ProgId="Applications\firefox.exe" ApplicationName="Firefox" />
  <Association Identifier="http" ProgId="FirefoxURL-308046B0AF4A39CB" ApplicationName="Firefox" />
  <Association Identifier="https" ProgId="FirefoxURL-308046B0AF4A39CB" ApplicationName="Firefox" />
</DefaultAssociations>
```

-------------------------------------------------------------------------------------------------------------

