# [MS-Edge](https://www.microsoft.com/de-de/edge/download?ch=1&form=MA13FJ) über GPO Richtlinie deinstallieren - Active Directory

`Anleitung verfasst am 2.9.2025`

`Windows-Server - Active Directory`


-------------------------------------------------------------------------------------------------------------


### ADMX/ADML-Vorlagen herunterladen und importieren
- Zunächst müssen natürlich die Vorlagen für den MS-Edge in Active-Directory Server hinzugefügt werden, damit die Einstellungen vorgenommen werden können.
- [Vorlagen herunterladen](https://www.microsoft.com/en-us/edge/business/download?ch=1&cs=3515903432&form=MA13FJ) und entpacken

- Wofür sind die Dateien ?
	- .admx → Enthält die eigentlichen Richtlinien (Regeln & Einstellungen)
	- .adml → Enthält die sprachspezifischen Beschreibungen für die Benutzeroberfläche

- Für eine Domäne (Active Directory):
	- Windows Explorer auf AD-Server öffnen
	- Wenn der Ordner `PolicyDefinitions` in dem einzufügenden Pfad fehlt, einfach anlegen und innerhalb des Ordners den Ordner `de-DE` erstellen.
	- folgenden Pfad aus der entpackten Datei öffnen: `/MSEdgePolicyTemplates/windows/admx/`
	- alle `.admx`-Dateien in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\`
	- alle `.adml`-Dateien in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\de-DE\`



### Gruppenrichtlinienverwaltung öffnen
- `gpmc.msc`
- Neues Gruppenrichtlinienobjekt anlegen
	- Rechtsklick auf `Gruppenrichtlinienobjekt`
	- `neu`
	- Namen vergeben
	- Rechtsklick auf das erstellte Objekt
	- `Bearbeiten`
	- Es sollte sich der Gruppenrichtlinienverwaltungs-Editor öffnen.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Microsoft Edge`
	- Hier sind nun alle Vorlagen.

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


### Richtlinien in Edge überprüfen
- Die Richtlinien können in Edge unter `chrome://policy` bzw. `edge://policy` eingesehen werden.


-------------------------------------------------------------------------------------------------------------


# MS-Edge Desktopverknüpfungen (gilt für alle Kanäle - Stable/Beta/Canary/Dev)


### Desktopverknüpfung standardmäßig bei der Installation erstellen
- Hat keine Auswirkung wenn Edge bereits installiert ist

- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge-Update > Anwendungen`
- `Desktopverknüpfung standardmäßig bei der Installation erstellen` -> Deaktiviert


### Entfernen von Desktopverknüpfungen beim Aktualisieren der Standardeinstellungen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge-Update > Anwendungen`
- `Entfernen von Desktopverknüpfungen beim Aktualisieren der Standardeinstellungen` -> Aktiviert
- Wert: `Erzwingen des Löschens von Desktopverknüpfungen auf System- und Benutzerebene`


-------------------------------------------------------------------------------------------------------------


# MS-Edge über GPO Richtline auf allen Clients deinstallieren

- Das ist nur auf Geräten im EWR-Wirtschaftsraum möglich, da die Gesetzeslage im EWR-Raum Microsoft dazu zwingt, eine Möglichkeit anzubieten MS-Edge zu deinstallieren.
- Die Richtlinien werden beim nächsten Update von Edge aktiv.


### Deinstallationsverhalten für Microsoft Edge angeben
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge-Update > Anwendungen > Microsoft Edge`
- `Deinstallationsverhalten für Microsoft Edge angeben` -> Aktiviert
- Wert: `Aktiviert und Löschen von Benutzerdaten`


### Installation von Edge zulassen/blockieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge-Update > Anwendungen > Microsoft Edge`
- `Installation zulassen` -> Aktiviert
- Wert: `Installationen deaktiviert`


-------------------------------------------------------------------------------------------------------------


# Edge-Beta-Version / Edge-Canary / Edge-Dev


### Installation von Edge-Beta zulassen/blockieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge-Update > Anwendungen > Microsoft Edge Beta`
- `Installation zulassen` -> Aktiviert
- Wert: `Installationen deaktiviert`


### Installation von Edge-Canary zulassen/blockieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge-Update > Anwendungen > Microsoft Edge Canary`
- `Installation zulassen` -> Aktiviert
- Wert: `Installationen deaktiviert`


### Installation von Edge-Dev zulassen/blockieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge-Update > Anwendungen > Microsoft Edge Dev`
- `Installation zulassen` -> Aktiviert
- Wert: `Installationen deaktiviert`


-------------------------------------------------------------------------------------------------------------

