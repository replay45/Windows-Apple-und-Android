# [MS-Edge](https://www.microsoft.com/de-de/edge/download?ch=1&form=MA13FJ) einschränken oder deinstallieren - Active Directory

`Anleitung verfasst am 2.9.2025, zuletzt bearbeitet am 6.1.2026`

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


# um MS-Edge einzuschränken: "Kiosk-Modus" selber bauen

- Um den MS-Edge einzuschränken, können folgende Richtlinien verwendet werden:
    - `InPrivate-Modus deaktivieren` > Der Private Modus sollte deaktiviert werden, damit Nutzer nicht den Privaten Modus verweden können, um die Einschränkungen zu umgehen.
    - `URL für die neue Tabseite konfigurieren` > Legt die Seite fest, die beim Öffnen des Browsers erscheint.
    - `Adressleiste deaktivieren` > Diese Richtlinie verhindert die manuelle Eingabe von URLs in die Adressleiste.
    - `Alle Domains blockieren/bestimmte Domains blockieren` > Damit können entweder alle Domains oder nur bestimmte Domains blockiert werden.
    - `Nur bestimmte Websites zulassen - Liste zulässiger URLs` > Hier können dann z.B. erlaubte Seiten, wie Seiten aus dem Intranet oder Seiten der Organisation etc. eingetragen werden.



### Privaten Modus deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Verwaltbarkeit des InPrivate-Modus konfigurieren` -> Aktiviert
- Wert: `InPrivate-Modus deaktiviert`


### URL zur "neue Tabseite" konfigurieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge > Start, Startseite und neue Tabs`
- `URL für die neue Tabseite konfigurieren` -> Aktiviert
- Wert: Die entsprechende URL zur gewünschten Webseite, z.B. Seite aus dem Intranet oder Firmens-/Organisations-Webseite


### Deaktiviert die Adressleiste (Nutzer können trotzdem noch Webseiten über Links/Lesezeichen etc. öffnen)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Konfiguration der Adressleistenbearbeitung` -> Deaktiviert


### Alle Domains blockieren/bestimmte Domains blockieren - URL-Blocklist
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Microsoft Edge`
- `Zugriff auf eine Liste von URLs blockieren` -> Aktiviert
- Wert: `*` um ALLE Domains zu blockieren, um bestimmte Domains zu erlauben die Richtlinie `Liste zulässiger URLs` verwenden
- Wert: `entsprechende URL... z.B. "Domain.de"` um nur bestimmte Domains auf die Blacklist zu setzen


### Nur bestimmte Websites zulassen - Liste zulässiger URLs
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Edge`
- `Liste zulässiger URLs definieren` -> Aktiviert
- Wert: `entsprechende URL... z.B. "Domain.de"`


-------------------------------------------------------------------------------------------------------------
