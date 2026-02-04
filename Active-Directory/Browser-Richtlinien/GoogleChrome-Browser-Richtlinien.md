# [Google-Chrome](https://www.google.com/chrome/) über GPO-Richtlinien konfigurieren - Active Directory

`Anleitung verfasst am 2.9.2025, zuletzt bearbeitet am 6.1.2026`

`Windows-Server - Active Directory`


-------------------------------------------------------------------------------------------------------------


### ADMX/ADML-Vorlagen herunterladen und importieren
- Zunächst müssen natürlich die Vorlagen für den Chrome-Browser in Active-Directory Server hinzugefügt werden, damit die Einstellungen vorgenommen werden können.
- [Vorlagen herunterladen](https://support.google.com/chrome/a/answer/187202?hl=de#zippy=%2Cwindows) und entpacken

- Wofür sind die Dateien ?
	- .admx → Enthält die eigentlichen Richtlinien (Regeln & Einstellungen)
	- .adml → Enthält die sprachspezifischen Beschreibungen für die Benutzeroberfläche

- Für eine Domäne (Active Directory):
	- Windows Explorer auf AD-Server öffnen
	- Wenn der Ordner `PolicyDefinitions` in dem einzufügenden Pfad fehlt, einfach anlegen und innerhalb des Ordners den Ordner `de-DE` erstellen.
	- zip entpacken
	- folgenden Pfad aus der entpackten Datei öffnen: `/policy_templates/windows/adm/de-DE`
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
	- `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Google` → `Google Chrome`
	- Hier sind nun alle Vorlagen.

- zurück zur `Gruppenrichtlinienverwaltung`
	- Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
	- Zum Verknüpfen das gewünschte Objekt auswählen


### Richtlinien im Chrome-Browser überprüfen
- Die Richtlinien können in allen Chrome basierten Browsern unter `chrome://policy` eingesehen werden.


-------------------------------------------------------------------------------------------------------------


# Erweiterungen

### Verfügbarkeit von Erweiterungen steuern, die nicht im Chrome Web Store veröffentlicht sind
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome > Erweiterungen`
- `Verfügbarkeit von Erweiterungen steuern, die nicht im Chrome Web Store veröffentlicht sind` -> Aktiviert
- Wert: `Erweiterungen, deren Veröffentlichung zurückgezogen wurde, deaktivieren`


### Installation von Erweiterungen aus externen Quellen blockieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome > Erweiterungen`
- `Installation externer Erweiterungen blockieren` -> Aktiviert


### Blockieren des Entwicklermodus
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome > Erweiterungen`
- `Verfügbarkeit des Entwicklermodus auf der Seite "Erweiterungen" steuern` -> Aktiviert
- Wert: `Verwendung des Entwicklermodus auf der Seite "Erweiterungen" nicht zulassen`


### Hinzufügen von Erweiterungen durch Nutzer nicht zulassen & für bestimmte Erweiterung Installation erzwingen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome > Erweiterungen`
- `Verwaltungseinstellungen für Erweiterungen` -> Aktiviert
- Wert (JSON-Code)

- Beispielwert - Hinzufügen von Erweiterungen durch Nutzer nicht zulassen & Installation von [uBlockOrigin Lite](https://ublockorigin.com/de) erzwingen:
```
{"*":{"installation_mode":"blocked","blocked_install_message":"Die Installation von Erweiterungen ist nicht erlaubt."},"ddkjiahejlhfcafbddmgiahcphecmpfh":{"installation_mode":"force_installed","update_url":"https://clients2.google.com/service/update2/crx"}}
```

- Beispielwert - Hinzufügen von Erweiterungen durch Nutzer nicht zulassen & Installation von [uBlockOrigin Lite](https://ublockorigin.com/de) & dem [Privacy Badger](https://privacybadger.org/) erzwingen:
```
{"*":{"installation_mode":"blocked","blocked_install_message":"Die Installation von Erweiterungen ist nicht erlaubt."},"ddkjiahejlhfcafbddmgiahcphecmpfh":{"installation_mode":"force_installed","update_url":"https://clients2.google.com/service/update2/crx"},"pkehgijcmpdhfbdbbnkijodmdjhbjlgp":{"installation_mode":"force_installed","update_url":"https://clients2.google.com/service/update2/crx"}}
```


# Zulassungsliste für Installation von Erweiterungen konfigurieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome > Erweiterungen`
- `Zulassungsliste für Installation von Erweiterungen konfigurieren` -> Aktiviert
- Wert: `entsprechene ID der Erweiterung`
	- [Privacy Badger](https://chromewebstore.google.com/detail/privacy-badger/pkehgijcmpdhfbdbbnkijodmdjhbjlgp): pkehgijcmpdhfbdbbnkijodmdjhbjlgp
	- [uBlockOrigin Lite](https://chromewebstore.google.com/detail/ublock-origin-lite/ddkjiahejlhfcafbddmgiahcphecmpfh): ddkjiahejlhfcafbddmgiahcphecmpfh
	- [Dark Reader](https://chromewebstore.google.com/detail/dark-reader/eimadpbcbfnmbkopoojfekhnkhdbieeh): eimadpbcbfnmbkopoojfekhnkhdbieeh
	- [Dark Mode](https://chromewebstore.google.com/detail/dark-mode/dmghijelimhndkbmpgbldicpogfkceaj): dmghijelimhndkbmpgbldicpogfkceaj
	- [KeePassXC-Browser](https://chromewebstore.google.com/detail/keepassxc-browser/oboonakemofpalcgghocfoadofidjkkk): oboonakemofpalcgghocfoadofidjkkk
	- [ChromeKeePass](https://chromewebstore.google.com/detail/chromekeepass/dphoaaiomekdhacmfoblfblmncpnbahm): dphoaaiomekdhacmfoblfblmncpnbahm
	- [Bitwarden Passwortmanager](https://chromewebstore.google.com/detail/bitwarden-password-manage/nngceckbapebfimnlniiiahkandclblb): nngceckbapebfimnlniiiahkandclblb
	- [Startpage - Datenschutz-Suchmaschine](https://chromewebstore.google.com/detail/startpage-%E2%80%94-private-searc/fgmjlmbojbkmdpofahffgcpkhkngfpef): fgmjlmbojbkmdpofahffgcpkhkngfpef
	- [NoScript](https://chromewebstore.google.com/detail/noscript/doojmbjmlfjjnbmnoijecmcbfeoakpjm): doojmbjmlfjjnbmnoijecmcbfeoakpjm
	- [Canvas Blocker - Fingerprint Protect](https://chromewebstore.google.com/detail/canvas-blocker-fingerprin/nomnklagbgmgghhjidfhnoelnjfndfpd): nomnklagbgmgghhjidfhnoelnjfndfpd


### Inkognitomodus deaktivieren (da Erweiterungen standardmäßig nicht im Inkognitomodus aktiv sind)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome`
- `Inkognitomodus - Verfügbarkeit` -> Aktiviert
- Wert: `Inkognitomodus deaktiviert`


-------------------------------------------------------------------------------------------------------------


# KI Einstellungen


### Einstellungen für "Design mit KI erstellen"
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Generative KI`
- `Einstellungen für "Design mit KI erstellen"` -> Aktiviert
- Wert: `"Designs mit KI erstellen" nicht zulasssen`


### Einstellungen für "Formuliere für mich"
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Generative KI`
- `Einstellungen für "Formuliere für mich"` -> Aktiviert
- Wert: `"Formuliere für mich" nicht zulasssen`


### Einstellungen für "Tab Compare"
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Generative KI`
- `Einstellungen für "Tab Compare"` -> Aktiviert
- Wert: `Tab Compare nicht zulasssen`


### Einstellungen für "KI-basierte Verlaufssuche"
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Generative KI`
- `Einstellungen für die KI-basierte Verlaufssuche` -> Aktiviert
- Wert: `KI-basierte Verlaufssuche nicht zulasssen`


### Einstellungen für generative KI-Funktionen in den Entwicklertools
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Generative KI`
- `Einstellungen für generative KI-Funktionen in den Entwicklertools` -> Aktiviert
- Wert: `Auf generativer KI basierende Funktionen der Entwicklertools nicht zulasssen`


### Einstellungen für lokales Foundation Model für generative KI
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Generative KI`
- `Einstellungen für lokales Foundation Model für generative KI` -> Aktiviert
- Wert: `Modell nicht herunterladen`


### Tabs organisieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Generative KI`
- `Einstellungen für "Tabs organisieren"` -> Aktiviert
- Wert: `"Tabs organisieren" nicht zulasssen`


-------------------------------------------------------------------------------------------------------------


### Google Cast deaktivieren
- Google Cast ist ein proprietäres Protokoll mit welchem Inhalte, wie Musik oder Filme gestreamt werden können.
- Wird in einem Unternehmen in der Regel nicht benötigt und kann für mehr Datenschutzfreundlichkeit deaktiviert werden.


- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Cast`
- `Google Cast aktivieren` -> Deaktiviert
- `Symbol von Google Cast in der Symbolleiste anzeigen` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------


# Inhaltseinstellungen

### Standardeinstellungen für "Standordbestimmung"
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Inhaltseinstellungen`
- `Standardeinstellungen für "Standordbestimmung"` -> Aktiviert
- Wert: `Verfolgen des physischen Standorts der Nutzer für keine Webseite zulassen`


### Standardeinstellungen für Pop-ups
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Inhaltseinstellungen`
- `Standardeinstellungen für Pop-ups` -> Aktiviert
- Wert: `Einblenden von Pop-ups auf keiner Webseite zulassen`


### Standardeinstellungen für Sensoren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Inhaltseinstellungen`
- `Standardeinstellungen für Sensoren` -> Aktiviert
- Wert: `Keiner Webseite erlauben, auf Sensoren zuzugreifen`


### Standardeinstellungen für Cookies
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Inhaltseinstellungen`
- `Standardeinstellungen für Cookies` -> Aktiviert
- Wert: `Cookies für die Dauer der Sitzung beibehlaten`


-------------------------------------------------------------------------------------------------------------


### Microsoft ActiveDirectory-Verwaltungseinstellungen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Microsoft ActiveDirectory-Verwaltungseinstellungen`
- `Automatische Anmeldung bei Microsoft-Cloudidentitätsanbietern zulassen` -> Aktiviert
- Wert: `Microsoft-Cloudauthentifizierung deaktivieren`


-------------------------------------------------------------------------------------------------------------


# Passwortmanager

### Speichern von Passwörtern anbieten
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Passwortmanager`
- `Aktiviert das Speichern von Passwörtern im Passwortmanager` -> Deaktiviert


### Datenleck-Erkennung für eingegebene Anmeldedaten
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Passwortmanager`
- `Datenleck-Erkennung für eingegebene Anmeldedaten aktivieren` -> Deaktiviert


### Speichern von Passkeys anbieten
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Passwortmanager`
- `Speichern von Passkeys im Passwortmanager aktivieren` -> Deaktiviert


### Teilen von Nuteranmeldedaten mit anderen Nutzern
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Passwortmanager`
- `Teilen von Nuteranmeldedaten mit anderen Nutzern aktivieren` -> Deaktiviert



-------------------------------------------------------------------------------------------------------------


# Safe-Browsing-Einstellungen

### Safe-Browsing-Umfragen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Safe-Browsing-Einstellungen`
- `Safe-Browsing-Umfragen zulassen` -> Deaktiviert


### Schutzniveau für Safe Browsing
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Safe-Browsing-Einstellungen`
- `Schutzniveau für Safe Browsing` -> Aktiviert
- Wert: `Safe Browsing ist im Standardmodus aktiv`

- Der Standardmodus ist bei Chrome Browsern der beste Kompromiss zwischen Datenschutz und Sicherheit.
- Bei den höheren Sicherheitsstufen muss man große Abstriche beim Datenschutz machen, da dann alle Browsing Daten an Google übermittelt werden.



-------------------------------------------------------------------------------------------------------------


# Standardsuchmaschine

### Name der Standardsuchmaschine
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Standardsuchmaschine`
- `Name der Standardsuchmaschine` -> Aktiviert
- Wert: `entsprechender Name, z.B. Startpage, Qwant, DuckDuckGo, Ecosia ...`


### Parameter für Funktion zur bildgesteuerten Suche
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Standardsuchmaschine`
- `Parameter für Funktion zur bildgesteuerten Suche für Standardsuchanbieter` -> Aktiviert
- Wert: `entsprechender Wert`
- z.B. [Startpage](https://www.startpage.com/): `https://www.startpage.com/images?q={searchTerms}`
- z.B. [Qwant](https://www.qwant.com/): `https://www.qwant.com/search/images?q={searchTerms}`
- z.B. [DuckDuckGo](https://duckduckgo.com/): `https://duckduckgo.com/?q={searchTerms}&iax=images&ia=images`
- z.B. [Ecosia](https://www.ecosia.org/): `https://www.ecosia.org/images?q={searchTerms}`


### Standardsuchmaschine aktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Standardsuchmaschine`
- `Standardsuchmaschine aktivieren` -> Aktiviert


### Standardsuchmaschinen Codierung - OPTIONAL
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Standardsuchmaschine`
- `Standardsuchmaschinen-Codierung` -> Aktiviert
- Wert: `UTF-8`


### Suchbegriff der Standardsuchmaschine
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Standardsuchmaschine`
- `Suchbegriff der Standardsuchmaschine` -> Aktiviert
- Wert: z.B. `startpage.com`, `qwant.com`, `duckduckgo.com` oder `ecosia.org`


### Such-URL der Standardsuchmaschine
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Standardsuchmaschine`
- `Such-URL der Standardsuchmaschine` -> Aktiviert
- Wert: `entsprechender Wert`
- z.B. [Startpage](https://www.startpage.com/): `https://www.startpage.com/search?q={searchTerms}`
- z.B. [Qwant](https://www.qwant.com/): `https://www.qwant.com/search?q={searchTerms}`
- z.B. [DuckDuckGo](https://duckduckgo.com/): `https://duckduckgo.com/?q={searchTerms}`
- z.B. [Ecosia](https://www.ecosia.org/): `https://www.ecosia.org/search?q={searchTerms}`


### Vorschlags-URL für die Standardsuchmaschine
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Standardsuchmaschine`
- `Vorschlags-URL für die Standardsuchmaschine` -> Aktiviert
- Wert: z.B. `https://ac.ecosia.org/autocomplete?q={searchTerms}`


-------------------------------------------------------------------------------------------------------------


# Start, Startseite und Seite "Neuer Tab"


### "Neuer Tab"-Seite als Startseite verwenden
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Start, Startseite und Seite "Neuer Tab"`
- `"Neuer Tab"-Seite als Startseite verwenden` -> Aktiviert


### Aktion beim Start
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Start, Startseite und Seite "Neuer Tab"`
- `Aktion beim Start` -> Aktiviert
- Wert: `"Neue Tab"-Seite öffnen`


### Startseiten-URL konfigurieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Start, Startseite und Seite "Neuer Tab"`
- `Startseiten-URL konfigurieren` -> Aktiviert
- Wert: `entsprechende URL zur gewünschten Seite`


### URL für "Neuer Tab"-Seite konfigurieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Start, Startseite und Seite "Neuer Tab"`
- `URL für "Neuer Tab"-Seite konfigurieren` -> Aktiviert
- Wert: `entsprechende URL zur gewünschten Seite`


-------------------------------------------------------------------------------------------------------------


# Zertifikatseinstellungen

### Nutzer erlauben, installierte CA-Zertifikate zu verwalten.
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Zertifikatverwaltungseinstellungen`
- `Nutzer erlauben, installierte CA-Zertifikate zu verwalten.` -> Aktiviert
- Wert: `Nutzer nicht erlauben, Zertifikate zu verwalten`


-------------------------------------------------------------------------------------------------------------


# Browsereinstellungen


### "Personen hinzufügen" im Nutzermanager aktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `"Personen hinzufügen" im Nutzermanager aktivieren` -> Deaktiviert


### Aktivieren der Funktion "Einkaufsliste" erlauben
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Aktivieren der Funktion "Einkaufsliste" erlauben` -> Deaktiviert


### Nur-HTTPS-Modus
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Aktivieren des Nur-HTTPS-Modus erlauben` -> Aktiviert
- Wert: `Aktivieren des Nur-HTTPS-Modus im strikten Modus erzwingen`


### Aktiviert die passive Authentifizierung für Profiltypen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Aktiviert die passive Authentifizierung für Profiltypen` -> Deaktiviert


### Anmeldungsabfragen aktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Anmeldungsabfragen aktivieren` -> Deaktiviert


### Anonymisierte URL-Datenfassung aktivieren (Übermittlung von URL Eingaben an Google deaktiveren)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Anonymisierte URL-Datenfassung aktivieren` -> Deaktiviert


### Anzeigen von Werbeinhalten aktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Anzeigen von Werbeinhalten aktivieren` -> Deaktiviert


### Apps weiter im Hintergrund ausführen, wenn Google Chrome geschlossen ist
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Apps weiter im Hintergrund ausführen, wenn Google Chrome geschlossen ist` -> Deaktiviert


### Autofill für Adressdaten zulassen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Autofill für Adressdaten zulassen` -> Deaktiviert


### Autofill für Kreditkartendaten zulassen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Autofill für Kreditkartendaten zulassen` -> Deaktiviert


### Automatische HTTPS-Upgrades aktivieren (immer HTTPS)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Automatische HTTPS-Upgrades aktivieren` -> Aktiviert


### Bei erstmaliger Ausführung Autofill-Formulardaten aus Standardbrowser importieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Bei erstmaliger Ausführung Autofill-Formulardaten aus Standardbrowser importieren` -> Deaktiviert


### Berichte mit Nutzungs- und Absturzdaten erstellen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Berichte mit Nutzungs- und Absturzdaten erstellen` -> Deaktiviert


### Browserdaten beim Beenden löschen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Browserdaten beim Beenden löschen` -> Aktiviert
- Wert: z.B. `browsing_history` / `download_history` / `cookies_and_other_site_data` / `cached_images_and_files` / `password_signin` / `autofill` / `site_settings` / `hosted_app_data`


### Browserverlauf bei erster Ausführung aus Standardbrowser importieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Browserverlauf bei erster Ausführung aus Standardbrowser importieren` -> Deaktiviert


### Chrome for Testing zulassen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Chrome for Testing zulassen` -> Deaktiviert


### Drittanbieter Cookies-blockieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Drittanbieter Cookies-blockieren` -> Aktiviert


### Einstellungen für die Anmeldung im Browser
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Einstellungen für die Anmeldung im Browser` -> Aktiviert
- Wert: `Browseranmeldung deaktivieren`


### Einstallungen für Werbung für Websites mit aufdringlichen Werbeanzeigen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Einstallungen für Werbung für Websites mit aufdringlichen Werbeanzeigen` -> Aktiviert
- Wert: `Werbung auf Websites mit aufdringlichen Werbeanzeigen nicht zulassen`


### Festlegen, wo Entwicklertools verwendet werden können
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Festlegen, wo Entwicklertools verwendet werden können` -> Aktiviert
- Wert: `Nutzung der Entwicklertools nicht zulassen`


### Gespeicherte Passwörter bei erster Ausführung aus Standardbrowser importieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Gespeicherte Passwörter bei erster Ausführung aus Standardbrowser importieren` -> Deaktiviert


### Gibt an, ob Nutzern produktinterne Google Chrome-Umfragen angezeigt werden.
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Gibt an, ob Nutzern produktinterne Google Chrome-Umfragen angezeigt werden.` -> Deaktiviert


### Google Chrome als Standardbrowser festlegen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Google Chrome als Standardbrowser festlegen` -> Deaktiviert


### Google Search Side Panel aktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Google Search Side Panel aktivieren` -> Deaktiviert


### Nutzerfeedack zulassen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Nutzerfeedack zulassen` -> Deaktiviert


### Speichern von WebRTC-Ereignisprotokollen aus Google-Diensten zulassen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Speichern von WebRTC-Ereignisprotokollen aus Google-Diensten zulassen` -> Deaktiviert


### Suchmaschinen bei erster Ausführung aus Standardbrowser importieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Suchmaschinen bei erster Ausführung aus Standardbrowser importieren` -> Deaktiviert


### Suchvorschläge aktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Suchvorschläge aktivieren` -> Deaktiviert


### Symbol für experimentelle Browserfunktionen aus der Symbolleiste
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Symbol für experimentelle Browserfunktionen aus der Symbolleiste` -> Deaktiviert


### Syncronisierung der Daten mit Google deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Syncronisierung der Daten mit Google deaktivieren` -> Aktiviert


### Websites erlauben, verfügbare Zahlungsmethoden abzufragen
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome`
- `Websites erlauben, verfügbare Zahlungsmethoden abzufragen.` -> Deaktiviert


-------------------------------------------------------------------------------------------------------------


# um Google Chrome einzuschränken: "Kiosk-Modus" selber bauen

- Um den Google Chrome einzuschränken, können folgende Richtlinien verwendet werden:
    - `Inkognitomodus deaktivieren` > Der Private Modus sollte deaktiviert werden, damit Nutzer nicht den Privaten Modus verweden können, um die Einschränkungen zu umgehen.
    - `URL für die neue Tabseite konfigurieren` > Legt die Seite fest, die beim Öffnen des Browsers erscheint.
    - `leere Suchmaschine hinzufügen` > Da man die Adressleiste in Google Chrome nicht so wie in MS-Edge deaktivieren/Sperren kann, kann man als Alternative eine "leere" Suchmaschine hinzufügen, da man in Chromium-basierten Browsern mindestens eine "Suchmaschine" benötigt. Durch die "leere"-Suchmaschine können keine Suchanfragen verarbeitet werden, da ja keine echte Suchmaschine, sondern nur ein Platzhalter eingestellt ist.
    - `Alle Domains blockieren/bestimmte Domains blockieren` > Damit können entweder alle Domains oder nur bestimmte Domains blockiert werden.
    - `Nur bestimmte Websites zulassen - Liste zulässiger URLs` > Hier können dann z.B. erlaubte Seiten, wie Seiten aus dem Intranet oder Seiten der Organisation etc. eingetragen werden.


### Inkognitomodus deaktivieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome`
- `Inkognitomodus - Verfügbarkeit` -> Aktiviert
- Wert: `Inkognitomodus deaktiviert`


### URL für "Neuer Tab"-Seite konfigurieren
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome > Start, Startseite und Seite "Neuer Tab"`
- `URL für "Neuer Tab"-Seite konfigurieren` -> Aktiviert
- Wert: Die entsprechende URL zur gewünschten Webseite, z.B. Seite aus dem Intranet oder Firmens-/Organisations-Webseite


### leere Suchmaschine hinzufügen (optional)
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Administrative Vorlagen > Google > Google Chrome > Standardsuchmaschine`
- `Such-URL der Standardsuchmaschine` -> Aktiviert
- Wert: `entsprechender Wert`
- z.B.
    - Name: `blank`
    - URL: `https://about.blank?q=%s`


### Alle Domains blockieren/bestimmte Domains blockieren - URL-Blocklist
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome`
- `Zugriff auf aufgelistete URLs blockieren` -> Aktiviert
- Wert: `*` um ALLE Domains zu blockieren, um bestimmte Domains zu erlauben die Richtlinie `Zugriff auf eine Liste mit URLs erlauben` verwenden
- Wert: `entsprechende URL... z.B. "Domain.de"` um nur bestimmte Domains auf die Blacklist zu setzen


### Nur bestimmte Websites zulassen - Zugriff auf eine Liste mit URLs erlauben
- Gruppenrichtlinien-Editor öffnen
- Pfad: `Computerkonfiguration > Richtlinien > Administrative Vorlagen > Google > Google Chrome`
- `Zugriff auf eine Liste mit URLs erlauben` -> Aktiviert
- Wert: `entsprechende URL... z.B. "Domain.de"`


-------------------------------------------------------------------------------------------------------------
