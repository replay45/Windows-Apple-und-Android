# Startmenü und Taskleiste-Richtlinien

`Anleitung verfasst am 19.1.2026`

`Windows-Server - Active Directory`

----------------------------------------------------------------------------------------

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

----------------------------------------------------------------------------------------

## Startmenü (nur Win11)

### "Link Internet durchsuchen in das Startmenü aufnehmen" (Internetsuche im Start-Manü (Suchberechtigung) deaktivieren)
- Pfad: `Benutzerkonfiguration > Administrative Vorlagen > Startmenü und Taskleiste`
- `Link Internet durchsuchen in das Startmenü aufnehmen` -> Deaktiviert

### Anheften der Microsoft-Store-App an die Taskleiste nicht zulassen
- Pfad: `Benutzerkonfiguration > Administrative Vorlagen > Startmenü und Taskleiste`
- `Anheften der Store-App an die Taskleiste nicht zulassen` -> Aktiviert

### Suchleiste zeigt keine Ergebnisse aus dem Internetverlauf/Favoriten an
- Pfad: `Benutzerkonfiguration > Administrative Vorlagen > Startmenü und Taskleiste`
- `Nicht im Internet suchen` -> Aktiviert

### Personalisierte Website-Empfehlungen aus dem Abschnitt "Empfohlen" im Startmenü entfernen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Startmenü und Taskleiste`
- `Personalisierte Website-Empfehlungen aus dem Abschnitt "Empfohlen" im Startmenü entfernen` -> Aktiviert

### Startmenü
- Das Layout im Startmenü lässt sich unter Windows 11 nicht mehr so wie in Windows 10 anpassen.
- Lediglich in Windows-Enterprise ist das eingeschränkt möglich.

----------------------------------------------------------------------------------------

## Windows-Komponenten - Taskleiste

### Neuigkeiten und interesante Themen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Neuigkeiten und interesante Themen`
- `Aktivieren von Neuigkeiten und Interessen auf der Taskleiste` -> Deaktiviert

### Suchhighlights (Suchhervorhebungen zulassen)
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Suche` 
- `Suchhervorhebungen zulassen` -> Deaktiviert

### Widgets
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Widgets`
- `Zulassen von Widgets` -> Deaktiviert

### Chat-Symbol aus Taskleiste entfernen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Chat`
- `Konfiguriert das Chat-Symbol in der Taskleiste` -> Aktiviert
- Wert: `Deaktiviert`

### Programme von der Taskleiste entfernen / anheften
- Nur mit Windows Enterprise Versionen möglich.

### Vorgeschlagene Apps im Windows lnk-Arbeitsbereich zulassen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Windows-Komponenten > Windows Ink-Arbeitsbereich`
- `Vorgeschlagene Apps im Windows lnk-Arbeitsbereich zulassen` -> Deaktiviert

----------------------------------------------------------------------------------------
