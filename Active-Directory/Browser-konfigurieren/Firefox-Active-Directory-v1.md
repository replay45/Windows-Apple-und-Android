# [Firefox](https://www.mozilla.org/de/firefox/new/) über Active Directory konfigurieren - Active Directory

`Anleitung erstellt am 13.2.2025, zuletzt bearbeitet am 16.9.2025`

`Windows-Server - Active Directory`

- Funktioniert für Standard-Firefox & Firefox ESR


-------------------------------------------------------------------------------------------------------------


# 1. ADMX/ADML-Vorlagen für Firefox herunterladen und importieren
- Offizielle Mozilla-Richtlinien: [github.com/mozilla/policy-templates](https://github.com/mozilla/policy-templates)
- folgende Dateien aus dem Pfad werden benötigt
	- Windows/firefox.admx
	- Windows/de-DE/firefox.adml


- Wofür sind die beiden Dateien ?
	- firefox.admx → Enthält die eigentlichen Richtlinien (Regeln & Einstellungen).
	- firefox.adml → Enthält die sprachspezifischen Beschreibungen für die Benutzeroberfläche


- Für eine Domäne (Active Directory):
	- Windows Explorer auf AD-Server öffnen
	- Wenn der Ordner `PolicyDefinitions` in dem einzufügenden Pfad fehlt, einfach anlegen und innerhalb des Ordners den Ordner `de-DE` erstellen.
	- Nach dem Herunterladen die `firefox.admx` in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\`
	- Nach dem Herunterladen die `firefox.adml` in folgenden Pfad kopieren: `\\DomainController\SYSVOL\Domain\Policies\PolicyDefinitions\de-DE\`


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
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- Hier sind nun alle Vorlagen.

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


-------------------------------------------------------------------------------------------------------------


# Erweiterungen installieren

### über JSON-Code
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Erweiterungen`
	- `Erweiterungen mit JSON verwalten` -> Aktiviert
	- Folgenden JSON Code einfügen und Platzhalter ersetzten
- für eine Erweiterung:
```
{
  "*": {
    "installation_mode": "allowed"
  },
  "uBlock0@raymondhill.net": {
    "installation_mode": "force_installed",
    "install_url": "https://addons.mozilla.org/firefox/downloads/latest/ublock-origin/latest.xpi",
    "private_browsing": "allow"
  }
}
```

- Für zwei Erweiterungen:
```
{
  "*": {
    "installation_mode": "allowed"
  },
  "uBlock0@raymondhill.net": {
    "installation_mode": "force_installed",
    "install_url": "https://addons.mozilla.org/firefox/downloads/latest/ublock-origin/latest.xpi",
    "private_browsing": "allow"
  },
  "keepassxc-browser@keepassxc.org": {
    "installation_mode": "force_installed",
    "install_url": "https://addons.mozilla.org/firefox/downloads/latest/keepassxc-browser/latest.xpi",
    "private_browsing": "allow"
  }
}
```
- Parameter:
	- `installation_mode`: `force_installed` erzwingt die Installation
	- `install_url`: direkte URL zur XPI-Datei
	- `private_browsing`: `allow` Erweiterung auch im privaten Modus aktiv
	- `ID-Platzhalter`: `ID` der Browsererweiterung einfügen
	- `Link zur Erweiterung` mit Link zur xpi Datei ersetzten

- ID herausfinden
	- Es gibt mehrere Möglichkeiten, die ID zu finden, nicht immer sind alle Möglichkeiten erfolgreich.
	- Gesucht wird eine vom Entwickler vorgesehene feste ID, die in der `manifest.json` definiert sein sollte.
	- Unter `about:debugging#/runtime/this-firefox` wird die Erweiterungs-ID benötigt.
	- Wenn das nicht zu Erfolg führt, kann die auch aus der `Manifest.json` gelesen werden, dafür immer noch unter `about:debugging#/runtime/this-firefox` auf die `Manifest-Adresse klicken` und dort nach der ID suchen.

- Beispiel:
	- Für [uBlock Origin](https://ublockorigin.com/de) ist die ID: uBlock0@raymondhill.net
	- Link: https://addons.mozilla.org/firefox/downloads/latest/ublock-origin/latest.xpi
	- Für [KeePassXC-Browser](https://keepassxc.org/) ist die ID: keepassxc-browser@keepassxc.org
	- Link: https://addons.mozilla.org/firefox/downloads/latest/keepassxc-browser/latest.xpi


-------------------------------------------------------------------------------------------------------------


# Benutzer-Benachrichtigungen

### Empfehlungen, Onboarding & "Mehr von Mozilla"-Bereich deaktivieren
- Onboarding ist die Einführung, die erscheint, wenn der Browser das erste Mal gestartet wird, um dem Nutzer die Einrichtung zu erleichtern, jedoch wird das meist nicht benötigt, wenn der Browser durch Acitve Directory verwaltet wird und kann daher deaktiviert werden.


- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Benutzer-Benachrichtigungen`
	- `Empfehlungen zur Erweiterung` -> Deaktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Benutzer-Benachrichtigungen`
	- `Funktions-Empfehlungen` -> Deaktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Benutzer-Benachrichtigungen`
	- `Firefox Labs` -> Deaktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Benutzer-Benachrichtigungen`
	- `Keine Änderungen der Einstellungen für die Nachrichtenübermittlung zulassen` -> Aktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Benutzer-Benachrichtigungen`
	- `Mehr von Mozilla` -> Deaktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Benutzer-Benachrichtigungen`
	- `Onboarding überspringen` -> Aktiviert


-------------------------------------------------------------------------------------------------------------


# Berechtigungseinstellungen

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Berechtigungen > Standort`
	- `Neue Anfragen zum Standort blockieren` -> Aktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Berechtigungen > Virtual Reality`
	- `Neue Anfragen für den Zugriff auf Virtual-Reality-Geräte blockieren` -> Aktiviert


-------------------------------------------------------------------------------------------------------------


# Browserdaten löschen, wenn Browser geschlossen wird
- Hier kann eingestellt werden, welche Daten beim Beenden von Firefox gelöscht werden.
- Beispielsweise wird das Einstellen vom Löschen des Caches gezeigt, aber auch das Löschen des Verlaufes Cookies etc. ist möglich.


- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Berechtigungen > Standort`
	- `Cache` -> Aktiviert


-------------------------------------------------------------------------------------------------------------


# Cookies
- Drittanbieter-Cookies/Third-Party-Cookies ablehnen

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Cookies`
	- `Cookie-Verhalten` -> Aktiviert
	- Wert: z.B. `Cookies von Drittanbietern ablehnen` wählen, um Third-Party-Cookies abzulehnen

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Cookies`
	- `Cookie-Verhalten beim privaten Surfen` -> Aktiviert
	- Wert: z.B. `Cookies von Drittanbietern ablehnen` wählen, um Third-Party-Cookies abzulehnen


-------------------------------------------------------------------------------------------------------------


# Firefox Suggest
- nur USA -> kann daher deaktiviert werden

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Firefox Suggest`
	- `Verbessern Sie Firefox Suggest` -> Deaktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Firefox Suggest`
	- `Vorschläge von Sponsorens` -> Deaktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Firefox Suggest`
	- `Vorschläge aus dem Internet` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------


# Lesezeichen per GPO hinzufügen (ohne vorhandene zu entfernen) & Lesezeichenleiste immer anzeigen
- Lesezeichen hinzufügen
	- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Lesezeichen`
	- Ein Lesezeichenslot auswählen, beginnend mit 01 
	- `Aktiviert`
	- Wert: Titel, Adresse (http://... | https://...) & ggf. Favicon Adresse eingeben
	- Wert: `Speicherort`: `Werkzeugleiste`

- Lesezeichenleiste immer anzeigen
	- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Lesezeichen`
	- `Lesezeichen-Symbolleiste anzeigen` -> Aktiviert
	- Wert: z.B.: `Immer anzeigen`


------------------------------------------------------------------------------------------------------------


# PopUps blockieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Popups`
	- `Popups von Webseiten blockieren` -> Aktiviert


------------------------------------------------------------------------------------------------------------


# Proxy Einstellungen
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Proxy`
	- `Keine Änderungen der Proxy-Einstellungen zulassen` -> Aktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Proxy`
	- `Verbindungstyp` -> Aktiviert
	- Wert: `Proxy-Einstellungen des Systems verwenden`


------------------------------------------------------------------------------------------------------------


# Suche & Suchmaschine

### Suchvorschläge deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Suche`
	- `Suchvorschläge` -> Deaktivieren

### Suchmaschine
- *folgt in Kürze*


------------------------------------------------------------------------------------------------------------


# Datenschutz- und Sicherheitseinstellungen setzen (Tracking-Schutz)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Tracking-Schutz`
	- `Tracking-Schutz`
	- `Aktiviert` -> Aktiviert

- ggf. zusätzlich noch `Cryptomining`, `Fingerprinter` & `E-Mail-Verfolgung` Schutzeinstellungen `Aktivieren`, um Schutzeinstellungen im Browser auf `"Benutzerdefiniert"` zu setzen
- Um das Ändern von den Einstellungen durch den Benutzer verhindern, die Einstellung `Änderungen an den Einstellungen ... verbieten` auswählen (Optional).


------------------------------------------------------------------------------------------------------------


# Zertifikatsspeicher des Betriebssystems nutzen (nur wenn gewünscht/benötigt)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox > Zertifikate`
	- `Windows-Zertifikatesspeicher benutzen` -> Aktiviert


------------------------------------------------------------------------------------------------------------


# Automatische Updates
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Automatisches Update` -> Aktiviert


------------------------------------------------------------------------------------------------------------


# Firefox-Passwortspeicherung & Autovervollständigungen deaktivieren

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Autovervollständigung für Zahlungsarten aktivieren` -> Deaktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Autovervollständigung für Adressen aktivieren` -> Deaktiviert

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Zugangsdaten und Passwörter für Websiten speichern` -> Deaktiviert


------------------------------------------------------------------------------------------------------------


# Firefox Home/Startseite
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Firefox Home anpassen` -> Aktiviert
	- Wert: Entsprechende Optionen an- & abwählen


------------------------------------------------------------------------------------------------------------


# Telemetrie/Studien deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Firefox Studien deaktivieren` -> Aktiviert
	- `Telemetrie deaktivieren` -> Aktiviert


------------------------------------------------------------------------------------------------------------


# Firefox-Konto-Funktion im Browser deaktivieren
- Verhindern, dass Nutzer sich mit Firefox-Konto im Browser anmelden können.
	- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Firefox-Konto deaktivieren` -> Aktiviert


------------------------------------------------------------------------------------------------------------


# Firefox Standardbrowser-Überprüfung - aktivieren/deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Firefox Standardbrowser-Überprüfung deaktivieren`
	- Wert: `Deaktiviert` auswählen für `aktive Standardbrowser-Überprüfung`
	- Wert: `Aktiviert` auswählen für `KEINE aktive Standardbrowser-Überprüfung`


------------------------------------------------------------------------------------------------------------


# Nur HTTPS-Modus in Fireox aktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Nur HTTPS-Modus` -> Aktiviert
	- Empfohlener Wert: `Standardmäßig eingeschaltet` oder `Eingeschaltet und gesperrt`


------------------------------------------------------------------------------------------------------------


# Pocket deaktivieren
- Pocket ist eine Funktion, mit der man Seiten "speichern" kann, allerdings benötigt man dazu ein Mozilla-Konto.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Poket für Firefox deaktivieren` -> Aktiviert


------------------------------------------------------------------------------------------------------------


# Daten von anderen Browsern in Firefox importieren - blockieren
- Pocket ist eine Funktion, mit der man Seiten "speichern" kann, allerdings benötigt man dazu ein Mozilla-Konto.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Profil-Import deaktivieren` -> Aktiviert


------------------------------------------------------------------------------------------------------------


# Links im Support Menü hinzufügen
- Über diese Richtlinie können Links im Support-Menü von Firefox hinzugefügt werden.
- Diese "Hilfen" findet man unter dem `Hamburger-Menü > Hilfe`

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Support Menü` -> Aktiviert
	- Wert: "Titel", "URL", Optional auch "Taste"


------------------------------------------------------------------------------------------------------------


# Upgrade Seite - Webseite, nach einem Firefox-Update
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Upgrade Seite ändern` -> Aktiviert
	- Wert: URL zur gewünschten Seite einfügen


------------------------------------------------------------------------------------------------------------


# Willkommensseite (Seite beim allerersten Start von Firefox)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Willkommensseite ändern` -> Aktiviert
	- Wert: URL zur gewünschten Seite einfügen


------------------------------------------------------------------------------------------------------------


# SSO mit Microsoft- oder Geschäftskonten verbieten - Windows SSO
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Windows SSO` -> Deaktiviert


------------------------------------------------------------------------------------------------------------


# Zugriffe auf Konfigurationsseiten

### Zugriff auf "about:config" verhindern
- "about:config" ist eine Erweiterung in der man tiefgehende Einstellungen setzten kann, das ist besonders für Entwicker wichtig, in Unternhemn kann der Zugriff jedoch über die Richtlinien verweigert werden, um die Stabilität und Sicherheit zu erhöhen.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Zugriff auf "about:config" verhindern` -> Aktiviert

### Zugriff auf "about:profiles" verhindern
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Zugriff auf "about:profiles" verhindern` -> Aktiviert

### Zugriff auf "about:third-party" verhindern - Blockierung von Drittanbietermodulen
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Blockierung von Drittanbietermodulen deaktivieren` -> Aktiviert

### Zugriff auf "about:support" verhindern - Informationen zur Fehlerbehebung
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Firefox`
	- `Zugriff auf Informationen zur Fehlerbehebung verhindern` -> Aktiviert


-------------------------------------------------------------------------------------------------------------

