# Windows Notepad (Text-Editor) GPO-Richtlinien

`Anleitung erstellt am 20.5.2025`

`Windows-Server - Active Directory`


-------------------------------------------------------------------------------------------------------------


### 1. ADMX/ADML Vorlagen
- Offizielle Templates: [learn.microsoft.com](https://learn.microsoft.com/de-de/windows/client-management/manage-notepad?tabs=intune#download-the-notepad-administrative-template-admx)
- cab-Datei extrhieren, danach zip entpacken
- folgende Dateien aus dem Pfad werden benötigt:
	- `WindowsNotepad.admx`
	- `de-DE/WindowsNotepad.adml`

- Wofür sind die beiden Dateien ?
	- `WindowsNotepad.admx` → Enthält die eigentlichen Richtlinien (Regeln & Einstellungen).
	- `WindowsNotepad.adml` → Enthält die sprachspezifischen Beschreibungen für die Benutzeroberfläche

- Für eine Domäne (Active Directory):
	- Windows Explorer auf AD-Server öffnen
	- Wenn der Ordner `PolicyDefinitions` in dem einzufügenden Pfad fehlt, einfach anlegen und innerhalb des Ordners den Ordner `de-DE` erstellen.
	- Nach dem Herunterladen die `WindowsNotepad.admx` in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\`
	- Nach dem Herunterladen die `WindowsNotepad.adml` in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\de-DE\`


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
	- `Computerkonfiguration` -> `Richtlinien` -> `Administrative Vorlagen` -> `Notepad`
	- Hier sind nun alle Vorlagen.

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


-------------------------------------------------------------------------------------------------------------


# KI-Funktionen deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Editor`
	- `KI-Funktionen im Windows-Editor deaktivieren` -> Aktiviert
	- `Übernehmen`, `OK`


-------------------------------------------------------------------------------------------------------------
