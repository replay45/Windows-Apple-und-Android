# Windows Datenschutzrichtlinien über [Microsoft Active Directory](https://de.wikipedia.org/wiki/Active_Directory) konfigurieren

`Anleitung verfasst am 8.4.2025, zuletzt bearbeitet am 3.2.2026`

`Windows-Server - Active Directory`


------------------------------------------------------------------------------------------------------------------------------


# ADMX-Vorlagen von Microsoft installieren
- Nach der neusten ADMX-Vorlage suchen und von der offiziellen Microsoft Seite herunterladen.
- Diese ist meist in einem .msi Paket
- Dieses auf dem Windows-Server installieren.
- Nach der Installation sind die Dateien hier: `C:\Program Files (x86)\Microsoft Group Policy\Windows-VERSION\PolicyDefinitions`
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
    - `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen`
    - Hier sind nun alle Vorlagen.
- zurück zur `Gruppenrichtlinienverwaltung`
    - Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
    - Zum Verknüpfen das gewünschte Objekt auswählen


------------------------------------------------------------------------------------------------------------------------------


# Datenschutzrichtlinien


### Datenschutzeinstellungen
- Werbe-ID deaktivieren
    - Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Benutzerprofile`
    - `WerbeID deaktivieren` -> Aktiviert (Richtlinie aktivieren um WerbeID zu deaktivieren, WerbeID ist eine ID um Nutzer genau zu tracken und Analysen anzufertigen, sollte unbedingt deaktiviert werden!)


### Verbessern der Freihand- und Tipperkennung
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Texteingabe`
- Richtlinie: `Verbessern der Freihand- und Tipperkennung` -> Deaktiviert


### Diagnose & Feedback
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Datensammlung und Vorabversionen`
- Richtlinien:
    - `Absturzabbildsammlung einschränken` -> Aktiviert
    - `Diagnosedaten zulassen` -> Aktiviert, Wert: `"Diagnosedaten deaktiviert"` (nur in Win-Server/Enterprise/Education))
    - `Diagnoseprotokollsammlung einschränken` -> Aktiviert
    - `Die Benutzeroberfläche der Einstellungen zur Aktivierung der Diagnosedaten konfigurieren` -> Aktiviert, Wert: `"...Diagnosedaten deaktivieren"`
    - `Feedbackbenachrichtigungen nicht mehr anzeigen` -> Aktiviert
    - `Sammlung von Browserdaten für Desktop Analytics konfigurieren` -> Aktiviert, Wert: `"Senden des Verlaufs nicht zulassen"`
    - `Übermitteln des Gerätenamens in Windows-Diagnosedaten zulassen` -> Deaktiviert


### Programm zur Verbesserung der Benutzerfreundlichkeit
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Programm zur Verbesserung der Benutzerfreundlichkeit`
- Richtlinie: `Unternehmensinterne Umleitung von Uploads zur Verbesserung der Benutzerfreundlichkeit zulassen` -> Deaktiviert


### Aktivitätsverlauf
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Betriebssystemrichtlinien`
- Richtlinien:
    - `Aktivitätsfeed aktivieren` -> Deaktiviert
    - `Synchronisierung der Zwischenablage geräteübergreifend zulassen` -> Deaktiviert
    - `Upload von Benutzeraktivitäten zulassen` -> Deaktiviert
    - `Veröffentlichen von Benutzeraktivitäten zulassen` -> Deaktiviert
    - Ergebnis: Kein Aktivitätenverlauf, keine Timeline-Synchronisierung


### Windows-Einstellungen synchronisieren
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Einstellungen synchronisieren`
- Richtlinien:
    - `App-Einstellungen nicht synchronisieren` -> Aktiviert
    - `Apps nicht synchronisieren` -> Aktiviert
    - `Barrierefreiheitseinstellungen nicht synchronisieren` -> Aktiviert
    - `Browsereinstellungen nicht synchronisieren`  -> Aktiviert
    - `Desktoppersonalisierung nicht synchronisieren`  -> Aktiviert
    - `Keine Synchronisierung über getaktete Verbindungen` -> Aktiviert
    - `Kennwörter nicht synchronisieren` -> Aktiviert
    - `Nicht synchronisieren` -> Aktiviert
    - `Personalisierung nicht synchronisieren` -> Aktiviert
    - `Spracheinstellungen nicht synchronisieren` -> Aktiviert
    - `Starteinstellungen nicht synchronisieren`  -> Aktiviert
    - `Weitere Windows-Einstellungen nicht synchronisieren` -> Aktiviert
    - Ergebnis: Keine Synchronisierung von Windows Einstellungen mit dem MS-Account


### Synchronisierung von Nachrichtendaten zulassen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Nachrichten`
- Richtlinie:
    - `Synchronisierung von Nachrichtendaten zulassen` -> Deaktiviert


------------------------------------------------------------------------------------------------------------------------------


# Windows-KI

### Windows Recall / Windows-KI deaktivieren
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Windows-KI`
- Richtlinien:
    - `Aktion per Mausklick deaktivieren` -> Aktiviert
    - `Aktivieren von Recall zulassen` -> Deaktiviert
    - `Export von Recall- und Momentaufnahmeinformationen zulassen` -> Deaktiviert
    - `Speichern von Momentaufnahmen für die Verwendung mit Recall deaktivieren` -> Aktiviert
    - `Agentische Sucherfahrung für Einstellungen deaktiveren` -> Aktiviert
    - Ergebnis: Recall fertigt keine automatischen (und unsichtbaren) Bildschirmaufnahmen mehr an, um Inhalte zu durchsuchen


------------------------------------------------------------------------------------------------------------------------------


# Cloudinhalte

### Cloudinhalt (Benutzerkonfiguration)
- Pfad: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Cloudinhalt`
- Richtlinien:
    - `Keine Diagnosedaten zur Personalisierung der Benutzererfahrung verwenden` -> Aktiviert
    - `Keine Inhalte von Drittanbietern in Windows-Blickpunkt vorschlagen` -> Aktiviert
    - `Windows-Blickpunkt im Info-Center deaktivieren` -> Aktiviert
    - `Windows-Willkommensseite deaktivieren` -> Aktiviert
- Ergebnis: Diagnosedaten werden nicht mehr für personalisierte Benutzererfahrung verwendet / Keine Werbung von Drittanbietern bei Windows Spotlight / Keine Benachrichtigungen und Vorschläge im Benachrichtigungscenter / Keine Willkommenseite mit Tipps, Werbung, Angeboten nach Updates (z.B. Aufforderungen zu Edge, OneDrive, Office...)


### Cloudinhalt (Computerkonfiguration)
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Cloudinhalt`
- Richtlinien:
    - `Deaktivieren von Inhalten, die für die Cloud optimiert sind` -> Aktiviert
    - `Inhalte des Cloud-Verbraucherkontostatus deaktivieren` -> Aktiviert
    - `Microsoft-Anwenderfeatures deaktivieren` -> Aktiviert (NUR Windows Enterprise/Education)
    - `Windows-Tipps nicht anzeigen` -> Aktiviert (NUR Windows Enterprise/Education)
- Ergebnis: Deaktivierung von online Tipps, Cloudbasierten Empfehlungen, ungewünschter Personalisierung und Werbung / Empfehlungen auf Basis des MS-Kontos deaktivieren / Keine Empfehlungen von Microsoft (NUR Windows Enterprise/Education) / Empfehlungen & Hinweise zu MS-Konto & hinweise zu MS-Produkten (NUR Windows Enterprise/Education)


------------------------------------------------------------------------------------------------------------------------------


# Gerät suchen

### Mein Gerät suchen deaktivieren
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Mein Gerät suchen`
- Richtlinie: `Mein Gerät suchen` -> Deaktiviert
- Ergebnis: Standort vom Gerät wird nicht mit Microsoft geteilt


------------------------------------------------------------------------------------------------------------------------------


# Microsoft Konto

### auto login in Diensten mit MS-Konto deaktivieren
- Diese Richtlinie verhindert die automatische Kontoweitergabe, also, dass Nutzer automatisch in Diensten wie OneDrive, Outlook oder MS-Store Apps eingeloggt werden, sofern Nutzer im Windows mit einem MS-Konto angemeldet sind.
- Bestehende Anmeldungen bleiben auch nach aktivierung der Richtlinie.
- Diese Richtlinie wirkt sich nicht auf Active Directory (AD)/ Azure AD (AAD)-Konten aus.
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Microsoft-Konto`
- Richtlinien:
  - `Benutzerauthentifizierung von Microsoft-Konten aller Anwender blockieren` -> Aktiviert


------------------------------------------------------------------------------------------------------------------------------


# Suche

### Windows-Sucheinstellungen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Suche`
- Richtlinien:
    - `Bei getakteten Verbindungen nicht im Web suchen und keine Webergebnisse in der Suche anzeigen` -> Aktiviert
    - `Cloudsuche zulassen` -> Deaktiviert
    - `Cortana auf Sperrbildschirm zulassen` -> Deaktiviert
    - `Cortana zulassen` -> Deaktiviert
    - `Der Suche und Cortana Nutzung von Positionsdaten erlauben`  -> Deaktiviert
    - `Festlegen der in Suche freigegebenden Informationen` -> Aktiviert, Wert: `Anonyme Informationen`
    - `Nicht im Web suchen und keine Webergebnisse in der Suche anzeigen` -> Aktiviert
    - `Suchhervorhebungen zulassen` -> Deaktiviert
    - `Websuche nicht zulassen` -> Aktiviert


------------------------------------------------------------------------------------------------------------------------------


# Offline-Karten

### Offline-Karten
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Karten`
- Richtlinien:
    - `Nicht angeforderten Netzwerk-Datenverkehr auf der Einstellungsseit "Offlinekarten" deaktivieren` -> Aktiviert
    - `Automatische Downloads und Updates von Kartendaten` -> Aktiviert
- Ergebnis: Karten werden nicht mehr im Hintergrund heruntergeladen.


------------------------------------------------------------------------------------------------------------------------------


# Apps

### App-Datenschutz
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > App-Datenschutz`
- Richtlinien:
    - `Windows-App-zugriff auf Diagnoseinformationen anderer Apps zulassen (Verweigern erzwingen)` -> Aktiviert
    - `Windows-App-Zugriff auf Positionsdaten zulassen (Verweigern erzwingen)` -> Aktiviert


### Copilot deaktivieren
- Pfad: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Windows Copilot`
- Richtlinie: `Windows Copilot deaktivieren` -> Aktiviert


### App-Telemetrie deaktivieren (erst wirksam nach Neustart)
- Pfad: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Anwendungskompatibilität`
- Richtlinie: `Anwendungstelemetrie deaktivieren` -> Aktiviert


### Übermitteln von Anwendungs-, Datei-, Geräte-, und Treiberdaten an Microsoft deaktivieren
- Pfad: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Anwendungskompatibilität`
- Richtlinie: `Inventory Collector deaktivieren` -> Aktiviert


### Problemaufzeichnung von Benutzern an Microsoft übermitteln deaktivieren
- Pfad: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Anwendungskompatibilität`
- Richtlinie: `Problemaufzeichnung deaktivieren` -> Aktiviert


------------------------------------------------------------------------------------------------------------------------------


# Microsoft-Store

### Microsoft-Store deaktivieren (Store für Benutzer unter Windows-Pro sperren oder deaktivieren für Win-Enterprise)
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Store`
- Richtlinie: `Store-Anwendung deaktivieren` -> Aktiviert
- Durch die Deaktivierung können keine neuen Apps aus dem Store installiert werden und bereits installierte Apps auch nicht mehr aktualisiert werden (NUR Windows Enterprise) !

- Für Windows Pro:
    - Richtlinie kann auch als Benutzerkonfiguration gesetzt werden, damit z.B. nur bestimte User nicht darauf zugreigfen können, Admins aber ggf. schon, je nach Konfiguration des Domänenstruktur.
    - Pfad: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Store`
    - Richtlinie: `Store-Anwendung deaktivieren` -> Aktiviert


### keine öffentlichen Apps im Microsoft-Store, nur von der Organisation zur Verfügung gestellte Apps
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Store`
- Richtlinie: `Nur privaten Store im Microsoft Store anzeigen` -> Aktiviert
- Durch diese Einstellung können nur von der Organisation zur Verfügung gestellte Apps aus dem Microsoft Store installiert werden - Für Enterpsrise & Pro !

- Richtlinie kann auch als Benutzerkonfiguration gesetzt werden, damit z.B. nur bestimte User nicht darauf zugreigfen können, Admins aber ggf. schon, je nach Konfiguration des Domänenstruktur.
    - Pfad: `Benutzerkonfiguration > Richtlinien > Administrative Vorlagen > Windows-Komponenten > Store`
    - Richtlinie: `Nur privaten Store im Microsoft Store anzeigen` -> Aktiviert


### Apps aus dem Microsoft-Store deaktivieren (optional, sinnvoll wenn Store komplett deaktiviert wurde)
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Richtlinien > Windows-Komponenten > Store`
- Richtlinie: `Alle Apps aus dem Microsoft Store deaktivieren` -> Aktiviert
- Durch diese Einstellung können nur von der Organisation zur Verfügung gestellte Apps aus dem Microsoft Store installiert werden - Für Enterpsrise & Pro !


### beim öffnen eines unbekannten Dateityps: "Apps im Microsoft-Store durchsuchen"
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Internetkommunikationseinstellungen`
- Richtlinie:
    - `Zugriff auf den Store deaktivieren` -> Aktiviert
- Ergebnis: Benutzer sehen nicht mehr beim öffnen eines unbekannten Dateityps den Punkt "Apps im Microsoft-Store durchsuchen"


------------------------------------------------------------------------------------------------------------------------------


# Internetkommunikationseinstellungen


### Deaktivieren von Senden von Fehlerbereichten an Microsoft (Handschrifterkennung)
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Internetkommunikationseinstellungen`
- Richtlinie:
    - `Handschrifterkennungs-Fehlerberichterstattung deaktivieren` -> Aktiviert
- Ergebnis: Benutzer können keine Fehlerbereichte an Microsoft bei der Handschrifterkennung senden.


### Programm zur Verbesserung der Benutzerfreundlichkeit (Es gibt 2 Richtlinien mit dem gleichen Namen, es sind jedoch nicht die gleichen Richtlinien)
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Internetkommunikationseinstellungen`
- Richtlinie:
    - `Programm zur Verbesserung der Benutzerfreundlichkeit deaktivieren` -> Aktiviert
    - `Programm zur Verbesserung der Benutzerfreundlichkeit deaktivieren` -> Aktiviert
- Ergebnis: Benutzer können keine Fehlerbereichte an Microsoft bei der Handschrifterkennung senden.


------------------------------------------------------------------------------------------------------------------------------


# Windows-Fehlerberichterstattung


### Fehlerberichterstattung konfigurieren
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Windows-Fehlerberichterstattung`
- Richtlinie: `Fehlerberichterstattung konfigurieren` -> Aktiviert
- Werte: alle Kästchen anwählen


### Fehlerberichterstattung
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > System > Windows-Fehlerberichterstattung`
- Richtlinien:
    - `Keine zusätzlichen Daten senden` -> Aktiviert
    - `Speicherabbild für vom Betriebssystem erstellte Fehlerberichte automatisch senden` -> Deaktiviert
    - `Windows-Fehlerberichterstattung deaktivieren` -> Aktiviert


------------------------------------------------------------------------------------------------------------------------------
