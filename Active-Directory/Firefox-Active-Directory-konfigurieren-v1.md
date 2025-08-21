# [Firefox](https://www.mozilla.org/de/firefox/new/) über Active Directory konfigurieren - Active Directory

`Anleitung erstellt am 13.2.2025`

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
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox`
	- Hier sind nun alle Vorlagen.

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


-------------------------------------------------------------------------------------------------------------


# 1. Erweiterungen installieren
- Hier kann es evtl. sein, dass nur Firefox ESR-Versionen unterstützt werden.

1. Über eine Richtlinie in der Vorlage (funktioniert möglicherweise nicht, daher über JSON-Code)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Erweiterungen`
	- `Erweiterungen installieren`
	- Kommentar hinzufügen
	- `Aktiviert` auswählen
	- `Anzeigen`
	- `ID` der Browsererweiterung einfügen
	- `Übernehmen`, `OK`


2. über JSON
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Erweiterungen`
	- `Erweiterungen mit JSON verwalten`
	- Kommentar hinzufügen
	- `Aktiviert` auswählen
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
	- `Übernehmen`, `OK`



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



# 2. Lesezeichen per GPO hinzufügen (ohne vorhandene zu entfernen)
- Lesezeichen hinzufügen
	- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Lesezeichen`
	- Ein Lesezeichenslot auswählen, beginnend mit 01
	- Kommentar hinzufügen
	- `Aktiviert` auswählen
	- Titel, Adresse (http://... \ https://...) & ggf. Favicon Adresse eingeben
	- `Speicherort`: `Werkzeugleiste`
	- `Übernehmen`, `OK`

- Lesezeichenleiste immer anzeigen
	- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Lesezeichen-Symbolleiste anzeigen`
	- `Windows-Zertifikatesspeicher benutzen`
	- Kommentar hinzufügen
	- `Aktiviert` auswählen (Immer anzeigen)
	- `Übernehmen`, `OK`


# 3. Zertifikatsspeicher des Betriebssystems nutzen
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Zertifikate`
	- `Windows-Zertifikatesspeicher benutzen`
	- Kommentar hinzufügen
	- `Aktiviert` auswählen
	- `Übernehmen`, `OK`


# 4. Telemetrie deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Alle Einstellungen`
	- `Telemetrie deaktivieren`
	- `Aktiviert` auswählen


# 5. Firefox-Passwortspeicherung & Autovervollständigungen deaktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Alle Einstellungen`
	- `Zugangsdaten und Passwörter für Websiten speichern`
	- `Deaktiviert` auswählen

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Alle Einstellungen`
	- `Autovervollständigung für Adressen aktivieren`
	- `Deaktiviert` auswählen

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Alle Einstellungen`
	- `Autovervollständigung für Zahlungsarten aktivieren`
	- `Deaktiviert` auswählen


# 6. Pocket deaktivieren
- Pocket ist eine Funktion, mit der man Seiten "speichern" kann, allerdings benötigt man dazu ein Mozilla-Konto.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox`
	- `Poket für Firefox deaktivieren`
	- `Aktiviert` auswählen


# 7. Firefox-Konto-Funktion im Browser deaktivieren
- Verhindern, dass Nutzer sich mit Firefox-Konto anmelden können
	- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox`
	- `Firefox-Konto deaktivieren`
	- `Aktiviert` auswählen


# 8. Datenschutz- und Sicherheitseinstellungen setzen
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Tracking-Schutz`
	- `Aktiviert`
	- `Aktiviert` auswählen

- ggf. zusätzlich noch `Cryptomining`, `Fingerprinter` & `E-Mail-Verfolgung` Schutzeinstellungen `Aktivieren`, um Schutzeinstellungen im Browser auf "Benutzerdefiniert" zu setzen
- Um das Ändern von den Einstellungen durch den Benutzer verhindern, die Einstellung `Änderungen an den Einstellungen ... verbieten` auswählen (Optional)


# 9. Cookies
- Drittanbieter-Cookies/Third-Party-Cookies ablehnen 

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Cookies`
	- `Cookie-Verhalten`
	- `Aktiviert` auswählen
	- Optionen: z.B. `Cookies von Drittanbietern ablehnen` wählen, um Third-Party-Cookies abzulehnen

- Das kann auch noch zusätzlich bzw. eine andere (ggf. strengere Option) für den privaten Modus eingestellt werden.


# 10. Empfehlungen, Onboarding & "Mehr von Mozilla"-Bereich deaktivieren
- Onboarding ist die Einführung, die erscheint, wenn der Browser das erstemal gestartet wird, um dem Nutzer die Einrichtung zu erleichtern, jedoch wird das meist nicht benötigt, wenn der Browser durch Acitve Directory verwaltet wird und kann daher deaktiviert werden.

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Benutzer-Benachrichtigungen`
	- `Mehr von Mozilla`
	- `Deaktiviert` auswählen

- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Benutzer-Benachrichtigungen`
	- `Onboarding`
	- `Aktiviert` auswählen


# 11. Automatische Updates
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Alle Einstellungen`
	- `Automatische Updates`
	- `Aktiviert` auswählen


# 12. SSO mit Microsoft- oder Geschäftskonten verbieten - Windows SSO
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Alle Einstellungen`
	- `Windows SSO`
	- `Deaktiviert` auswählen


# 13. Nur HTTPS-Modus in Fireox aktivieren
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Alle Einstellungen`
	- `Nur HTTPS-Modus`
	- `Aktiviert` auswählen
	- Empfohlen: `Standardmäßig eingeschaltet` oder `Eingeschaltet und gesperrt`


# 14. Willkommensseite (Seite beim allerersten Start von Firefox)
- Im Gruppenrichtlinienverwaltungs-Editor
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Firefox` → `Alle Einstellungen`
	- `Willkommensseite ändern`
	- `Aktiviert` auswählen
	- URL zur gewünschten Seite einfügen


-------------------------------------------------------------------------------------------------------------
