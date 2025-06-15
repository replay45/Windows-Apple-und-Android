# CA-Zertifikate über Active Directory verteilen

`Anleitung erstellt am 18.2.2025`

`Windows-Server - Active Directory`


--------------------------------------------------------------------------------------------------------------


# Zertifikate im Systemspeicher des Betriebssystems
- Anwendungsbereich:
	- Für Programme, die auf dem Betriebssystem installiert sind
	- Für Browser, die auf Chromium basieren
	- In [Firefox](https://www.mozilla.org/de/firefox/new/) nur, wenn man `security.enterprise_roots.enabled` aktiviert ist


- Zertifikate über die Domäne in den Zertifikatsspeicher des Betriebssystems Windows importieren


### GPO - Gruppenrichtlinie erstellen (Computerrichtlinie)
- Zertifikat vorbereiten.
- Zertifikat sollte als `crt`-Datei vorliegen.
- Auf dem Active-Directory-Windows-Server als Administrator einloggen.

- `Gruppenrichtlinienverwaltung` öffnen
- `Gruppenrichtlinienobjekte` wählen
- `Neu`
- Namen vergeben
- Rechtsklick auf das neue Gruppenrichtlinienobjekt und auf `bearbeiten` klicken
- Es öffnet sich der `Gruppenrichtlinienverwaltungs-Editor`
- Nun im Gruppenrichtlinienverwaltungs-Editor zu `Computerkonfiguration` → `Richtlinien` → `Windows-Einstellungen` → `Sicherheitseinstellungen` → `Richtlinien für öffentliche Schlüssel` → `Vertrauenswürdige Stammzertifizierungsstellen` navigieren
- `importieren` wählen
- Assistenten folgen & Zertifikat auswählen
- Zurück zur `Gruppenrichtlinienverwaltung`
    - Unter `Domain.local` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
    - Das gewünschte Objekt auswählen
- Fertig

- In der [CMD](https://de.wikipedia.org/wiki/Cmd.exe) / [PowerShell](https://de.wikipedia.org/wiki/PowerShell) die Gruppen- & Benutzerverwaltung für PCs (Clients) aktualisieren
```
$ gpupdate /force
```

- Überprüfung auf den Clients:
	- `Win+r` drücken
	- `certlm.msc`
	- Überprüfen, ob das Zertifikat unter `Vertrauenswürdige Stammzertifizierungsstellen` erscheint.


--------------------------------------------------------------------------------------------------------------

