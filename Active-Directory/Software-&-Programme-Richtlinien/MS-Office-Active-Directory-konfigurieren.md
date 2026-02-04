# [Microsoft Office 2019/2021](https://support.microsoft.com/de-de/office/herunterladen-und-installieren-oder-erneutes-installieren-von-office-2021-office-2019-oder-office-2016-7c695b06-6d1a-4917-809c-98ce43f86479) über Active Directory konfigurieren

`Anleitung erstellt am 5.5.2025`

`Windows-Server - Active Directory`


-------------------------------------------------------------------------------------------------------------


# 1. ADMX/ADML-Vorlagen für Office herunterladen und importieren
- Offizielle [MS-Office-Richtlinien](https://www.microsoft.com/en-us/download/details.aspx?id=49030) herunterladen
- `.exe`-Datei ausführen
- Dateien werden in Ordner entpackt (auf den Pfad achten)
- Pfad öffnen und Dateien aus `admx`-Ordner kopieren (admin-Ordner kann ignoriert werden)


- Wofür sind die Dateien ?
	- .admx → Enthält die eigentlichen Richtlinien (Regeln & Einstellungen).
	- .adml → Enthält die sprachspezifischen Beschreibungen für die Benutzeroberfläche


- Für eine Domäne (Active Directory):
	- Windows Explorer auf AD-Server öffnen
	- Wenn der Ordner `PolicyDefinitions` in dem einzufügenden Pfad fehlt, einfach anlegen und innerhalb des Ordners den Ordner `de-DE` erstellen.
	- Nach dem Herunterladen die `.admx` in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\`
	- Nach dem Herunterladen die `.adml` in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\de-DE\`



# 2. Gruppenrichtlinienverwaltung öffnen
- `gpmc.msc`
- Neues Gruppenrichtlinienobjekt anlegen
	- Rechtsklick auf `Gruppenrichtlinienobjekt`
	- `neu`
	- Namen vergeben
	- Rechtsklick auf das erstellte Objekt
	- `Bearbeiten`
	- Es sollte sich der Gruppenrichtlinienverwaltungs-Editor öffnen.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Microsoft "entsprechendes Office Produkt" 2016` (trotz "2016"-Bezeichnung gelten Richtlinien auch für Office 2019 und neuer)
	- Hier sind nun alle Vorlagen.

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


-------------------------------------------------------------------------------------------------------------


# 1. Microsoft Office (für alle Office Dienste)


## Datenschutz Optionen

### Feedback an Microsoft verbieten
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Benutzern gestatten, Feedback an Microsoft zu senden` -> Deaktiviert
	- Richtlinie: `Benutzern das Einschließen von Protokolldateien und releanten Inhaltsbeispielen gestatten, wenn Feedback an Microsoft gesendet wird` -> Deaktiviert


### Screenshots in Feedback an Microsoft verbieten
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Benutzern gestatten, Screenshots und Anlagen beim Senden von Feedback an Microsoft hinzuzufügen` -> Deaktiviert


### Verhindern, dass Nutzer am Programm zur Verbesserung der Benutzerfreundlichkeit teilnehmen
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Program zur Verbesserung der Benutzerfreundlichkeit aktivieren` -> Deaktiviert
	

### Verhindern, dass Microsoft Benutzer kontaktieren darf, die Feedback gesendet haben
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Microsoft das Nachverfolgen des von Benutzern übermittelten Feedbacks gestatten` -> Deaktiviert


### Umfragen
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Benutzern das Empfangen von und reagieren auf Umfragen von Microsoft innerhalb des Produktes gestatten` -> Deaktiviert


### Persönliche Informationen an Microsoft senden
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Persönliche Informationen senden` -> Aktiviert


### Diagnosedaten
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Stufe der von Office gesendeten Clientsoftware-Diagnosedaten konfigurieren` -> Aktiviert
	- Wert: `Weder noch`


### Microsoft grundsätzlich verbieten Inhalte zu analysieren und "verbundene Erlebnisse" anzubieten -> hat übergeordnete Auswirkung auf alle Optionen der "verbundenen Erlebnisse"
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Die Verwendung verbundener Erfahrungen in Office zulassen` -> Deaktiviert


### zusätzliche Onlinefunktionen deaktivieren (3D-/Online Grafiken über Bing, Onlinevideos in PowerPoint)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Die Verwendung zusätzlicher optionaler verbundener Erfahrungen in Office zulassen` -> Deaktiviert


### Microsoft verbieten Inhalte aus Office zu analysieren 
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Datenschutz > Trust Center`
	- Richtlinie: `Die Verwendung verbundener Erfahrungen, die Inhalt analysieren, in Office zulassen` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------


## KI Optionen


### Trainig von KI für personalisierte Inhalte deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > AI > Trainig > General`
	- Richtlinie: `Trainig aller Features für den Benutzer deaktivieren` -> Aktiviert


### Trainig von KI für personalisierte Inhalte deaktivieren (Adaptive Floatie)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > AI > Trainig > Specific > Adaptive Floatie`
	- Richtlinie: `Trainig des Features "Adaptive Floatie" für den Benutzer deaktivieren` -> Aktiviert


-------------------------------------------------------------------------------------------------------------


## Standardbrowser für Links

### Standardbrowser für Links in Office
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Office 2016 > Links`
	- Richtlinie: `Auswählen, welcher browser Weblinks öffnet` -> Aktiviert
	- Wert: `Standardbrowser des Systems`


-------------------------------------------------------------------------------------------------------------


# 2. Outlook


### Senden von Diagnosdaten bei Abstürzen/Fehlern verhindern
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Outlook 2016 > Weitere`
	- Richtlinie: `Supportdiagnose in Outlook deaktivieren` -> Aktiviert


### Verhindern, dass Kennwörter von POP3-/ IMAP- / HTTP-Konten (Internet-Konten) in Outlook gespeichert werden
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Outlook 2016 > Sicherheit`
	- Richtlinie: `Kennwort speichern für Internet-E-Mail-Konten deaktivieren` -> Aktiviert


### Empfehlung der neuen Outlook App von Microsoft deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Outlook 2016 > Outlook-Optionen > Weitere`
	- Richtlinie: `Intervall zwischen neuen Outlook Migrationsversuchen` -> Aktiviert
	- Wert: `0`


### Empfehlung von Outlook Browser-Erweiterung deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Microsoft Outlook 2016 > Weitere`
	- Richtlinie: `Empfehlen Sie die Microsoft Outlook-Erweiterung` -> Aktiviert


-------------------------------------------------------------------------------------------------------------

