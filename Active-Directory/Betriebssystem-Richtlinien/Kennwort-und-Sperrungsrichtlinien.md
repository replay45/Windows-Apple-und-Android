# Kennwort und Sperrungsrichtlinien über Active Directory

`Anleitung verfasst am 25.6.2025, zuletzt bearbeitet am 15.9.2026`

`Windows-Server - Active Directory`

------------------------------------------------------------------------------------------------------------------------------

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

------------------------------------------------------------------------------------------------------------------------------

# Sicherheitseinstellungen

### Kontorichtlinien/Kennwortrichtlinien
- GPO: `Computerkonfiguration > Windows-Einstellungen > Sicherheitseinstellungen > Kontorichtlinien/Kennwortrichtlinien`
- Richtlinien:
  - `Kennwort muss Komplexitätsvoraussetzungen entsprechen` -> Aktiviert
  - `Minimale Kennwortlänge` -> Aktiviert


### Kontensperrungsschwelle
- GPO: `Computerkonfiguration > Windows-Einstellungen > Sicherheitseinstellungen > Kontorichtlinien/Kennwortrichtlinien`
- Richtlinien:
    - `Kontensperrungsschwelle` -> Aktiviert (Wert: z.B. 10)
    - `Kontosperrdauer` -> Aktiviert (Wert: z.B. 10 minuten)
    - `sperrung des Administratorkontos zulassen` -> Aktiviert (Wert: `deaktiviert`)
    - `Zurücksetzungsdauer des Kontosperrungszählers` -> Aktiviert (Wert: z.B. 10 minuten)


------------------------------------------------------------------------------------------------------------------------------


# Bildschirm sperren mit Gruppenrichtlinien

- [Bildschirm sperren mit Gruppenrichtlinien](https://www.windowspro.de/wolfgang-sommergut/bildschirm-sperren-gruppenrichtlinien-dynamische-sperre)

### Kennworteingabe beim Verlassen des Ruhezustands/Standbymodus anfordern
- GPO: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > System/Energieverwaltung`
- Richtlinien:
    - `Kennworteingabe beim Verlassen des Ruhezustands/Standbymodus anfordern` -> Aktiviert

### Bildschirm sperren (legt nur Zeit fest, Abhängig von GPOs zum "Bildschirmschoner")
- GPO: `Computerkonfiguration > Richtlinien > Windows-Einstellungen > Sicherheitseinstellungen > Lokale Richtlinien > Sicherheitsoptionen`
- Richtlinien:
    - `Interaktive Anmeldung: Inaktivitätsgrenze des Computers` -> Aktiviert (Wert: z.B 480sek für 8 Minuten)


### Bildschirmschoner
- GPO: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Systemsteuerung > Anpassung`
- Richtlinien:
    - `Bildschirmschoner aktivieren` -> Aktiviert
    - `Kennwortschutz für den Bildschirmschoner verwenden` -> Aktiviert
    - `Zeitlimit für den Bildschirmschoner` -> Aktiviert
    - `Bestimmten Bildschirmschoner erzwingen` -> Aktiviert (Wert: `rundll32.exe user32.dll,LockWorkStation`)


------------------------------------------------------------------------------------------------------------------------------
