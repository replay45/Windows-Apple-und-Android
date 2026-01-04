# Windows-Desktop Einstellungen - Active Directory

`Anleitung verfasst am 23.6.2025, zuletzt bearbeitet am 17.12.2025`

`Windows-Server - Active Directory`


-------------------------------------------------------------------------------------------------------------


## Inhaltsverzeichnis
1. Desktop-Hintergrund setzen
2. Icons hinzufügen
3. Icons entfernen


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


# 1. Desktop-Hintergrund
- Im Gruppenrichtlinienverwaltungs-Editor
    - `Benutzerkonfiguration > Administrative Vorlagen > Desktop > Desktop`
    - `Desktophintergrund` -> Aktiviert
    - Wert: UNC oder lokalen Pfad zum gewünschten Hintergrund angeben.
    - GGf. muss die Bilddatei durch ein Skript etc. auf die Clients kopiert werden, damit das Hintergrundbild evtl. auch außerhalb der AD-Umgebung verfügbar ist.
    - Einfarbige Bilddateien, mit Farbcode Angabe, können unter [analogouscolors.com](https://www.analogouscolors.com/) gefunden werden.
    - Um den gesammten Bildschirm mit dem Hintergrundbild bei Bildschirmen mit unterschiedlichen Seitenverhältnissen (16:9 / 16:10 / 21:9 usw.) auszufüllen, kann `Ausfüllen` beim Wert ausgewählt werden.
    - Alternativ könnte sich auch der Wert `Zentriert` eignen.


-------------------------------------------------------------------------------------------------------------


# 2. Icons hinzufügen (am Beispiel von: Webseite im Browser öffnen)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Einstellungen > Windows-Einstellungen > Verknüpfungen`
	- `Neu` > `Verknüpfung`
	- Aktion: `Erstellen`
	- Name vergeben
	- Zieltyp: `Dateisytemobjekt`
	- Speicherort: `Desktop`
	- Zielpfad: `Pfad zum Programm, z.B. zum Browser` - `C:\Program Files\Mozilla Firefox\firefox.exe`
	- Argument: `https://beispiel.com`

- Der Zielbrowser/ das Zielprogramm muss natürtlich auf den Clients vorhanden (installiert) sein.


-------------------------------------------------------------------------------------------------------------


# 3. Icons entfernen (am Beispiel von: MS-Edge Link vom Desktop entfernen)

- Pfad herausfinden, in dem das Edge Icon (Microsoft Edge.lnk) gespeichert ist:
	- Auf dem Desktop ein Rechtsklick auf das "Edge Symbol" machen
	- `Eigenschaften`
	- `Allgemein`
	- unter `Ort` ist der entsprechende Pfad angegeben.


### Edge Icon Pfad: "C:\Users\<BENUTZERNAME>\Desktop\Microsoft Edge.lnk" (%DesktopDir%\Microsoft Edge)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Einstellungen > Windows-Einstellungen > Verknüpfungen`
	- `Neu` > `Verknüpfung`
	- Aktion: `Löschen`
	- Name: `exakter Name der Verknüpfung, z.B. Microsoft Edge`
	- Speicherort: `Desktop`

- Alternativ zum exakten Namen, kann auch der Pfad zum Link angegeben werden, z.B. `%USERPROFILE%\Desktop\Microsoft Edge`
- Manche Shortcuts tauchen nach Windows Updates wieder auf, daher empfiehl es sich die GPO-Richtlinie aktiv zu lassen.


### Edge Icon Pfad: "C:\Users\Public\Desktop\Microsoft Edge.lnk" (%CommonDesktopDir%\Microsoft Edge)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Einstellungen > Windows-Einstellungen > Verknüpfungen`
	- `Neu` > `Verknüpfung`
	- Aktion: `Löschen`
	- Name: `exakter Name der Verknüpfung, z.B. Microsoft Edge`
	- Speicherort: `Alle Benutzer - Desktop`


-------------------------------------------------------------------------------------------------------------

