# Windows Update-Richtlinien über Active Directory konfigurieren

`Anleitung verfasst am 25.6.2025`

`Windows-Server - Active Directory`


------------------------------------------------------------------------------------------------


# ADMX-Vorlagen von Microsoft installieren
- Nach der neusten ADMX-Vorlage suchen und von der offiziellen Microsoft Seite herunterladen.
- Diese ist meist in einem .msi Paket
- Dieses auf dem Windows-Server installieren.
- Nach der Installation sind die Dateien hier: `C:\Program Files (x86)\Microsoft Group Policy\Windows-Version\PolicyDefinitions`
- Nun alle `.admx-Vorlagen` in die folgenden Pfad kopieren:`\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\`
- Alle `.adml-Dateien` in kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\de-DE\`


# Gruppenrichtlinienverwaltung öffnen
- `gpmc.msc`
- Neues Gruppenrichtlinienobjekt anlegen
	- Rechtsklick auf `Gruppenrichtlinienobjekt`
	- `neu`
	- Namen vergeben
	- Rechtsklick auf das erstellte Objekt
	- `Bearbeiten`
	- Es sollte sich der Gruppenrichtlinienverwaltungs-Editor öffnen.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Windows-Komponenten`
	- Hier sind nun alle Vorlagen.

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


------------------------------------------------------------------------------------------------


# Windows Updates


### Automatische Updates (Endbenutzeroberfläche)
- GPO: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Windows Update > Endbenutzeroberfläche verwalten`
- Richtlinien:
	- `Automatische Updates konfigurieren` -> Aktiviert
	- Wert: `4-Autom. Herunterladen und laut Zeitplan installieren`
	- Wert: `0-Täglich`
	- Wert: z.B. `07:00`
	- Wert: `Jede Woche`
	- zusätzlich empfohlener Wert: `Updates für andere Microsoft-Produkte installieren` (z.B. Updates für Office, VS-Code, AQL-Servermanager, ...)


### Automatische Neustarts außerhalb der Nutzungzeiten (Endbenutzeroberfläche)
- GPO: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Windows Update > Endbenutzeroberfläche verwalten`
- Richtlinien:
	- `Automatischen Neustart nach Updates während der Nutzungszeit deaktivieren` -> Aktiviert
	- Wert: z.B. `08:00`
	- Wert: z.B. `18:00`


### Automatische Updates sofort installieren (Legacy Richtlinien)
- GPO: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Windows Update > Legacy Richtlinien`
- Richtlinien:
	- `Automatische Updates sofort installieren` -> Aktiviert


### Keinen auto Neustart für geplante Installationen von auto Updates, wenn Benutzer angemeldet sind (Legacy Richtlinien)
- GPO: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Windows Update > Legacy Richtlinien`
- Richtlinien:
	- `Keinen automatischen Neustart für geplante Installationen automatischer Updates durchführen, wenn Benutzer angemeldet sind` -> Aktiviert


### OPTIONAL: "Empfohlene Updates" über auto-Updates aktivieren (Legacy Richtlinien)
- GPO: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Windows Update > Legacy Richtlinien`
- Richtlinien:
	- `Empfohlene Updates über automatische Updates aktivieren` -> Aktiviert


### OPTIONAL: Suchhäufigkeit für automatische Updates (vom Windows Server Service angebotene Updates verwalten)
- GPO: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Windows Update > vom Windows Server Service angebotene Updates verwalten`
- Richtlinien:
	- `Suchhäufigkeit für automatische Updates` -> Aktiviert
	- Wert z.B. `22`


------------------------------------------------------------------------------------------------

