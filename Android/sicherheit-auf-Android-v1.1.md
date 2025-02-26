# Sicherheit auf Android

`Anleitung erstellt am 8.12.2024, zuletzt bearbeitet am 7.2.2025`

## Inhaltsverzeichnis
1. grundlegende Sicherheitstipps
2. DNS-Server auf Android
3. Spionageschutz: Kamera, Mikrofon & Sensoren vollständig & systemweit blockieren (Sicherheitsrichtlinie)
4. Googles WerbeID löschen & Diagnosedaten deaktivieren (Google auf Android)
5. Einstellungen: Sicherheit und Datenschutz (Samsung)
6. "Passwörter sichtbar machen" - Funktion deaktivieren
7. Sperrbildschirm: Verhindern, dass Netzwerk- & Sicherheitseinstellungen geändert werden können (Samsung)
8. Geräteverschlüsselung & Sperrbildschirm
9. Für Apps zugelassene Netzwerke (WLAN/MOBILE-DATEN) (Samsung)
10. Spezieller Zugriff & Berechtigungsverwaltung für Apps (Samsung)
11. App-Sicherheit: auf schädliche Apps prüfen (PlayStore & Gerätewartung)
12. Standort: Scan Optionen ausschalten (WLAN & Bluetooth)
13. Galaxy-AI - Verarbeitung nur auf dem Gerät (Samsung)
14. Gerätestatus prüfen: offiziell/inoffiziell


-----------------------------------------------------------------------------------------------------------------


# 1. grundlegende Sicherheitstipps
- die Grundlagen & allgemeies Verhalten
    - Absolute Sicherheit gibt es nie ! - Aufklärung ist der beste Schutz !
    - Man sollte immer den gesunden Menschenverstand einschalten.
    - Ein gewisses Maß an Skepsis ist immer gut.
    - Sicherung von Systemen gegen Diebstahl oder Manipulationen.
    - Keine unbekannten/ vermeindlich gefundenen USB-Sticks verwenden !

- Datenschutz & Tracking
    - Datenminimierung: Nur personenbezogene Daten angeben, wenn unbedingt notwendig.
    - Man sollte sich nur in online-Accounts einloggen, wenn notwendig.
    - Die `Werbe-ID löschen` & `personalisierte Werbung deaktivieren`, um Tracking zu minimieren und zu erschweren.
    - Cloud-Dienste meiden - eigene Cloud oder [NAS (Homeserver)](https://de.wikipedia.org/wiki/Network_Attached_Storage) nutzen.
    - Sichere und datenschutzfreundliche DNS-Server nutzen.

- Browser & Verhalten im Internet
    - Acht geben, auf was im Internet heruntergeladen wird und welche Webseiten besucht werden.
    - Einen sicheren Browser, wie [Firefox](https://www.mozilla.org/de/firefox/new/) oder den [Brave-Browser](https://brave.com/de/) verwenden.
    - Browser datenschutzfreundlich einstellen und Cookies von Dritt-Anbietern blockieren.
    - AdBlocker verwenden - [uBlock Origin](https://ublockorigin.com/de)

- E-Mail
    - Vorsicht vor Scam-E-Mails und schädlichen Anhängen.
    - Einen sicheren E-Mail-Client ohne Tracker nutzen - [Thunderbird](https://www.thunderbird.net/de/) & [K-9](https://k9mail.app/).

- Authentifizierung & Verschlüsselung
    - Festplatten-/ Geräteverschlüsselung aktivieren & Passwortsperre nutzen.
    - Passwortmanager mit starken Passwörtern nutzen - empfohlen: [KeePassXC](https://keepassxc.org/) oder [BitWarden](https://bitwarden.com/de-de/)
    - 2‑Faktor-Authentifizierung nutzen - [2FAS](https://2fas.com/)

- Software & Daten schützen
    - [Open Source](https://de.wikipedia.org/wiki/Open_Source) Software bevorzugen.
    - Regelmäßiges Installieren von Updates.
    - Nicht mehr benötigte Programme entfernen.
    - Backups erstellen.
    - Keine unbekannten Befehle in einem Terminal (wie z.B. [Termux](https://termux.dev/en/)) ausführen.

- Mehr zu `sicher & anonym im Internet surfen` unter [ethical hacking & Cyber Security/Cyber-Security/anonym & sicher im Internet surfen](https://github.com/replay45/ethical-hacking-und-cybersecurity/tree/main/cyber-security)


-----------------------------------------------------------------------------------------------------------------


# 2. DNS-Server auf Android

`Zuletzt getestete Android-Version: 14`

- Hinweis: 
    - Das Ändern des DNS-Servers zu einem sicheren Anbieter, verhindert ohne Implementierung einer Verschlüsselung oder Signierung keine [Man-in-the-Middle-Angriffe](https://de.wikipedia.org/wiki/Man-in-the-Middle-Angriff) oder Tracking !

### Was ist ein DNS-Server ?
Ein DNS-Server `übersetzt Domainnamen` wie "google.de" `in IP-Adressen`, denn Domains sind für uns Menschen, im Gegensatz zu IP-Adressen, einfacher zu merken.
Außerdem gibt es nicht genügend verfügbare IPv4-Adressen, daher können diese sich auch ändern, was jedoch dank der DNS-Server kein Problem ist.
- [Cloudflare - Was ist ein DNS-Server](https://www.cloudflare.com/de-de/learning/dns/what-is-a-dns-server/)


### Wieso den DNS-Server ändern ?
- Standardmäßig nutzt man die DNS-Server des Internetanbieters, diese sind jedoch häufig eher langsamer und wenn man `verhindern` möchte, dass der `Internetprovider bzw. Mobilfunkanbieter einsehen kann, welche Domains man aufruft`, ist es sehr ratsam, die DNS-Server von [Cloudflare](https://www.cloudflare.com/) zu nutzen.
- Den DNS-Server kann man auf allen gänigen Desktop-Betriebsystemen sowie auf dem Smartphone, als auch in vielen gänigen Routern ändern.
- Wie man seinen eigenen kleinen DNS-Server mit [Pi hole](https://pi-hole.net/) erstellen kann, wird unter [Raspberry-Pi/Pi-hole](https://github.com/replay45/Linux-RaspberryPI-NextCloud/tree/main/raspberry-pi) gezeigt.
- [Cloudflare](https://www.cloudflare.com/) legt dabei den `Fokus` auf `Datenschutz & Sicherheit`, verspricht `kein Logging` von Daten die zur Identifizierung genutzt werden können und bietet dennoch sehr `schnelle DNS-Server`.


### Privates DNS - DNS-Server für alle Verbindungen einstellen & DNS-Verschlüsselung
- `Bevorzugten DNS-Server` für `alle Verbindungen` (WLAN & mobile Daten) einstellen und `Verschlüsselung(DoT) nutzen`.
- Diese Einstellungen `überschreibt alle anderen Optionen` zu den DNS-Servern !

Für wen eignet sich diese Option ?
    - Diese Option ist `besonders für wenig erfahrene Nutzer` oder die jenigen `die keinen eigenen DNS-Server wie Pi hole betreiben` `sinnvoll`.


- "Privates DNS" - aktivieren
    - `Einstellungen` öffnen
    - `Verbindungen`
    - `Weitere Verbindungseinstellungen`
    - `Privates DNS`
    - `Hostname des Anbieters des privaten DNS`
    - einfügen: `one.one.one.one`
    - `Speichern` klicken


### WLAN - DNS-Server manuell für eine bestimmte Verbindung ändern
- Wenn ein DNS-Server unter der Option `Privates DNS` eingestellt ist, wird diese Option `unbrauchbar`.
- Verschlüsselung der DNS-Anfragen ist hier NICHT möglich.
    - `Einstellungen` öffnen
    - `Verbindungen`
    - `WLAN`
    - mit einem WLAN-Netzwerk verbinden
    - auf das `Einstellungen-Symbol` am rechten Rand klicken
    - `Mehr anzeigen` auswählen
    - `IP-Einstellungen`: `Statisch` auswählen
    - `DNS 1`: `1.1.1.1`
    - `DNS 2`: `1.0.0.1`


### Mobile Daten
- Das manuelle Einstellen bevorzugter DNS-Server für mobiles Internet ist nur bei gerooteten Android-Smartphones möglich.
- Um auch bei mobilem Internet einen beforzugten DNS-Server nutzen zu können, muss `Privates DNS` genutzt werden.
- Lediglich eine VPN-Verbindung stellt hier eine Ausnahme dar, denn bei einer VPN-Verbindung sollte standardmäßig der bevorzugte DNS-Server des VPN-Servers verwendet werden (sofern diese nicht ggf. von der Option `Privates DNS` überschrieben werden).
    - Das wären bei einem externen Anbietern die entsprechenden DNS-Servers des VPN-Providers oder bei einer VPN-Verbindung in das eigene Heimnetz die entsprechenden Einstellungen im Router.


### Alternative Möglichkeiten - VPN & Pi hole
- Wer selber einen DNS-Server im Heimnetz hosten möchte, kann das z.B. mit [Pi hole](https://pi-hole.net/) tun.
- Der [Pi hole](https://pi-hole.net/) kann u.a. als standard-DNS-Server im Router eingestellt werden und über `VPN` in das Heimnetzwerk, kann dieser auch von überall genutzt werden.
- Eine VPN-Verbindung bietet u.a. mehrere Vorteile, wie z.B. eine sichere Verbindung in das Heimnetzwerk, bei unsicheren WLAN-Verbindungen oder Zugriff auf Geräte in Heimnetzwerk, wie ein NAS/Homeserver.
- Eine weitere Möglichkeit wäre z.B. [Pi hole](https://pi-hole.net/) über Dyn-DNS aus dem Internet erreichbar zu machen/ extern zu hosten, um Pi hole als DNS-Server für die Option `Privates DNS` einzustellen.


### Fazit - die optimalen Einstellungen treffen
- `weniger erfahrene Nutzer`
    - Für weniger erfahrene Nutzer ist die Einstellung `Privates DNS` (inkl. Verschlüsselung DoT) mit `Hostname des Anbieters des privaten DNS` die beste Option, um immer den gewünschten DNS-Server nutzen zu können (Option überschreibt alle anderen Optionen).
    - Dabei empfehlen sich die DNS-Server von [Cloudflare](https://www.cloudflare.com/): `one.one.one.one`

- `erfahrene Nutzer`
    - Für erfahrene Nutzer empfiehlt sich die Option `Privates DNS` `nur wenn KEIN eigener DNS-Server, wie Pi hole im Heimnetzwerk betrieben` wird.
    - Wenn ein `eigener DNS-Server` wie [Pi hole](https://pi-hole.net/) betrieben wird, kann `abgewogen werden`, ob `Android Geräte durch "Privates DNS" ausgeschlossen` oder ob z.B. von außerhalb eine `VPN-Verbindung` in das `Heimnetzwerk (bzw. zum DNS-Server)` eine Möglichkeit wäre, dabei muss man sich jedoch bewusst sein, dass nur bei entsprechender VPN-Verbindung auch der gewünschte DNS-Server genutzt wird.
    - Eine andere Möglichkeit wäre z.B. [Pi hole](https://pi-hole.net/) über Dyn-DNS aus dem Internet erreichbar zu machen/ extern zu hosten, um Pi hole als DNS-Server einzustellen (nur für sehr erfahrene Nutzer geeignet).


### Mehr zu DNS-Servern und Pi hole unter [Linux-RaspberryPI-NextCloud/Raspberry-Pi](https://github.com/replay45/Linux-RaspberryPI-NextCloud/tree/main/raspberry-pi)


-----------------------------------------------------------------------------------------------------------------


# 3. Spionageschutz: Kamera, Mikrofon & Sensoren vollständig & systemweit blockieren (Sicherheitsrichtlinie)

`Zuletzt getestete Android-Version: 14`

### Kamera, Mikrofon & andere Sensoren über das QuickPanel nach Belieben deaktivieren und wieder aktivieren
- Was bringt die Funktion (Sicherheitsrichtline)
    - Wer Angst vor `Spionage` hat oder `unbefugten Zugriff` auf Kamera oder Mikrofon verhindern möchte, kann `Sensors Off` nutzen, um eine Sicherheitsrichtline zu aktivieren, die den `Zugriff auf Sensoren`, wie Mikrofon oder Kamera `systemweit blockiert`.

- Beeinträchtigungen
    - Dabei sollte beachtet werden, dass einige Funktionen, wie z.B. "Bildschirm drehen" von der Deaktivierung der Sensoren beeinträchtigt werden können.

- `Sensors Off`-Funktion überprüfen
    - Wenn man also nach der Deaktivierung der Sensoren versucht, die Kamera App zu öffnen, wird man feststellen, dass diese sich nicht mehr öffnen lässt.


### Schnelleinstellung freischalten
- In den `Entwicklermodus` gehen - wie dieser aktiviert werden kann, ist in diesem Ordner in der Datei [android](https://github.com/replay45/Windows-Apple-und-Android/tree/main/Android) unter `Punkt 1` beschrieben.
- Zu `Entwicklerkacheln f. Schnelleinst.` scrollen.
- Nun die Option `Sensors Off` auswählen.
- Jetzt sollte eine neue Verknüpfung im `QuickPanel` erscheinen.


-----------------------------------------------------------------------------------------------------------------


# 4. Googles WerbeID löschen & Diagnosedaten deaktivieren (Google auf Android)

`Zuletzt getestete Android-Version: 14`

## Was ist die Werbe-ID und wieso sollte man sie löschen ?
- Die Werbe-ID ist eine `ID zur Identifizierung` eines `Android-Smartphones` - "Google Advertising ID" (GAID) und bei Apple „Identifier for Advertisers“ (IDFA), ähnlich wie ein Nummernschild, die für `Werbezwecke` genutzt wird.
- Da die Werbe-ID für `Tracking` und `Werbung` verwendet wird, sollte man diese unbedingt löschen.
- Dritte können mit der Werbe-ID Nutzer `online, sowie offline` `tracken`, `Standortdaten` und `Suchanfragen` verknüpfen und speichern, oder `geziehlte Werbung` schalten.
- Daher ist das `Risiko` für `Identitätsdiebstahl`, `Betrug` oder `Manipulation` extrem hoch.


## WerbeID löschen
- `Einstellungen` öffnen
- `Google` auswählen
- `Alle-Dienste`
- `Werbung`
- `Werbe-ID löschen`


## Senden von Diagnosedaten deaktivieren
- `Einstellungen` öffnen
- `Google` auswählen
- `Alle-Dienste`
- `Nutzung & Diagnose`
- Option `deaktivieren`


-----------------------------------------------------------------------------------------------------------------


# 5. Einstellungen: Sicherheit und Datenschutz (Samsung)

`Zuletzt getestete Android-Version: 14`

### Sicherheit und Datenschutz
- Unter diesem Reiter können einige Optionen zur Sicherheit und zum Datenschutz in einer Übersicht eingesehen werden.


### Übersicht (Vorschläge)
- Hier werden vorgeschlagene Einstellungen angezeigt.
- Die Punkte `Sperrbildschirm`, `App-Sicherheit` und `Updates` sollten erfüllt werden, da sie zur elementaren Sicherheit beitragen.


### weitere Sicherheitseinstellungen
- `Verbesserter Datenschutz`, Verschlüsselung von Samsung Cloud (sofern ein Samsung-Konto verwendet wird)
- `SD-Karte verschlüsseln`, verschlüsselt eine SD-Karte (sofern eine SD-Karte verwendet wird)
- `USB-Verbindung blockieren, wenn gesperrt`, verhindert Angriffe über den USB-Port bei gesperrtem Bildschirm.
- `Trusted Agents`: Deaktivierung bewirkt mehr Sicherheit.


### Datenschutz
- `Berechtigungsverwaltung`: Hier können die Berechtigungen für Apps gesetzt werden. Mehr Berechtigungen können unter `Apps/Spezieller Zugriff` (Punkt 7) entzogen/gesetzt werden.
- `weitere Datenschutzeinstellungen`
    - Samsung:
        - personalisierten Dienst abschalten
        - erhalten von Nachrichten/Angeboten ablehnen
        - Personalisierte Werbung deaktivieren
        - Diagnosedaten senden ausschalten
    - Google:
        - Android-Personalisierungsdienst deaktivieren
        - System Intelligent - Aufzeichnung von Eingaben über die Tastatur
        - Werbung - WerbeID löschen
        - Nutzung & Diagnose ausschalten


-----------------------------------------------------------------------------------------------------------------


# 6. "Passwörter sichtbar machen" - Funktion deaktivieren

`Zuletzt getestete Android-Version: 14`

### Was ist die "Passwörter sichtbar machen" Option ?
Wenn die Funktion aktiviert ist, wird bei der Eingabe von Passwörtern die Eingabe kurz angezeigt, bevor sie mit einem Punkt "verdeckt" wird.


### Funktion deaktivieren
In den Einstellungen unter `Sicherheit und Datenschutz`, `Weitere Sicherheitseinstellungen` und nun die Option `Passwörter sichtbar machen` deaktivieren, damit Passwörter bei der Eingabe nicht mehr angezeigt werden und direkt mit dem Punkt "verdeckt" werden.


-----------------------------------------------------------------------------------------------------------------


# 7. Sperrbildschirm: Verhindern, dass Netzwerk- & Sicherheitseinstellungen geändert werden können (Samsung)

`Zuletzt getestete Android-Version: 14`

- Die Funktion sollte standardmäßig aktiv sein.

### Netzwerk und Sicherheit sperren - Funktion für den Sperrbildschirm
Die Funktion verhindert, dass WLAN, mobile Daten oder Standort mit gesperrtem Display ausgeschaltet werden können.
Das Aktivieren der Funktion ist besonders für den Diebstahlschutz wichtig.


### Funktion aktivieren/deaktivieren
In den Einstellungen zu `Sperrbildschirm und AOD` wechseln und unter `Sichere Sperreinstellungen` überprüfen, ob die Funktion aktiv ist und die gewünschte Einstellung setzen.


-----------------------------------------------------------------------------------------------------------------


# 8. Geräteverschlüsselung & Sperrbildschirm

- Glücklicherweise sind `moderne Android-Geräte standardmäßig` mit der `dateibasierten Verschlüsselung` (File-Based Encryption, FBE) verschlüsselt.
- Dabei wird der `Speicher auf Dateiebene verschlüsselt` und Dateien können unabhänig voneinander mit unterschiedlichen Schlüsseln verschlüsselt werden.
- Unter Android gibt es zwei Bereiche, einen der erst nach der Authentifizierung verfügbar ist (z.B. Dateien) und der andere, der auch im gesperrten Zustand zugänglich ist (z.B. für Telefonanrufe).
- Android verwendet ein `mehrstufiges Schlüsselmanagement`, wobei vereinfacht gesagt die `Verschlüsselungsschlüssel` mit dem `PIN oder Passwort` für den `Sperrbildschirm` zugänglich gemacht werden.
- Daher ist die Wahl eines `starken Passworts für den Sperrbildschirm entscheidend`, denn dieser schützt die Verschlüsselungsschlüssel der dateibasierten Verschlüsselung.


### Funktionsweise der dateibasierten Verschlüsselung unter Android
- Verschlüsselung auf Dateiebene (File-Based Encryption, FBE) mit 2 Bereichen (CE, DE)
- Verwendung von unterschiedlichen Schlüsseln
- Hardware-basierte Speicherung von Verschlüsselungsschlüsseln
- Schutz der Schlüssel durch Passwort auf dem Sperrbildschirm


### Fazit
- Zusammengefasst schützt ein starkes Passwort über den Sperrbildschirm die Verschlüsselungsschlüssel.
- Daher ist die standardmäßige Verschlüsselung von der Wahl des Passworts zum Schutz der Verschlüsselungsschlüssel abhängig.
- Je `stärker das Passwort`, desto `sicherer` ist die `Verschlüsselung unter Android`.


### Was muss ich nun tun ?
- Die dateibasierte Verschlüsselung ist unter Android standardmäßig aktiv.
- Zum Schutz der Verschlüsselungsschlüssel sollte ein starkes Passwort auf dem Sperrbildschirm verwendet werden.


-----------------------------------------------------------------------------------------------------------------


# 9. Für Apps zugelassene Netzwerke (WLAN/MOBILE-DATEN) (Samsung)

`Zuletzt getestete Android-Version: 14`

- Hier kann festgelegt werden, welche Netzwerke eine App verwenden darf.
    - `Einstellungen` öffnen
    - `Verbindungen`
    - `Datennutzung`
    - `Für Apps zugelassene Netzwerke`
    - Nun wählen, ob eine App WLAN, mobile Daten oder beides nutzen darf.


-----------------------------------------------------------------------------------------------------------------


# 10. Spezieller Zugriff & Berechtigungsverwaltung für Apps (Samsung)

`Zuletzt getestete Android-Version: 14`

### Berechtigungen setzen
- Allgemein gilt: So `wenige Berechtigung wie möglich` und so `viele wie nötig`.
- Jedoch gibt es Apps, z.B. wie die Kamera App, die nun mal Zugriff auf Kamera und Mikrofon benötigt, um Fotos und Videos aufzunehmen.
- Daher muss individuell geprüft werden, ob die App die Berechtigung benötigt.


### Was ist der Spezielle Zugriff und die Berechtigungsverwaltung ?
- Über den speziellen Zugriff können spezielle Berechtigungen für Apps gesetzt werden.
- Dazu gehören kritische Optionen, jedoch benötigen viele Apps weniger Berechtigungen als meistens standardmäßig gesetzt.
- Bei Apps, die nicht verwendet werden, können meistens alle Berechtigungen entfernt werden.
- In der Berechtigungsverwaltung können dann die üblichen Berechtigungen für Apps gesetzt werden.


### Berechtigungen über den speziellen Zugriff & die Berechtigungsverwaltung verwalten
- `Einstellungen` öffnen
- `Apps`
- `3-Punkte Menü` (Weitere Optionen)
- `Spezieller Zugriff` oder `Berechtigungsverwaltung` auswählen
- Nun gewünschte Einstellungen vornehmen.


-----------------------------------------------------------------------------------------------------------------


# 11. App-Sicherheit: auf schädliche Apps prüfen (PlayStore & Gerätewartung)

`Zuletzt getestete Android-Version: 14`

- Man kann sowohl im PlayStore als auch in der Gerätewartung alle Apps auf `"schädliche Apps"` prüfen.
- `App Schutz` (Gerätewartung):
    - `Einstellungen` öffnen,
    - `Gerätewartung` auswählen,
    - Mit der Option `App-Schutz` kann man den Scan starten.
    - Dabei werden Apps auf Malware und verdächtige Aktivitäten gescannt.

- Auch im GooglePlay-Store können Apps über `PlayProtect` geprüft werden.
    - Dafür den `GooglePlay-Store` öffnen,
    - auf das Icon des Google Accounts (oben rechts) klicken und `PlayProtect` auswählen.
    - Hier kann nun ein `Scan` durchgeführt werden.
    - In den `Einstellungen von PlayProtect` kann man noch die `Erkennung schädlicher Apps verbessern` (Senden von Daten an Google) ausschalten.


-----------------------------------------------------------------------------------------------------------------


# 12. Standort: Scan-Optionen ausschalten (WLAN & Bluetooth)

`Zuletzt getestete Android-Version: 14`

# Wieso diese Optionen deaktivieren ?
- Wenn die Optionen zur Verbesserung der Genauigkeit nicht ausgeschaltet sind, werden WLAN & Bluetooth nie richtig abgeschaltet, auch wenn man sie manuell im Quick-Panel deaktiviert.
- Vorteile beim ausschalten der beiden Optionen:
    - weniger Akkuverbrauch
    - Kontrolle darüber, wann WLAN & Bluetooth ein-/ ausgeschaltet sind
    - Apps das Bestimmen des genauen Standortes erschweren

- Das Deaktivieren der Scan-Optionen hat keine Auswirkung auf die normale Verwenung von WLAN oder Bluetooth Verbindungen !

# Ausschalten der beiden Optionen
- `Einstellungen` öffnen
- Standort auswählen
- auf `Standortdienste` klicken
- `WLAN-Scan` & `Bluetooth-Scanning` deaktivieren


-----------------------------------------------------------------------------------------------------------------


# 13. Galaxy-AI - Verarbeitung nur auf dem Gerät (Samsung)

`Zuletzt getestete Android-Version: 14 mit OneUI 6.1.1`

### Wieso sollte man die Option "Daten nur auf Gerät verarbeiten" aktivieren ?
- Beim aktivieren der Option, werden Inhalte nur noch auf dem Gerät, also lokal verarbeitet.
- Um die Inhalte zu verarbeiten werden diese häufig in die Cloud hochgeladen, was potenziell unwerünscht ist.
- Auch wenn dadurch manche Funktionen nicht mehr verfügbar sind, sollte der Datenschutz und der Schutz der Privatsphäre unbedingt ernst genommen werden und daher ist es sehr ratsam die Option zu aktivieren. 


### Option aktivieren
- `Einstellungen` öffnen
- `Galaxy AI`
- Option `Daten nur auf Gerät verarbeiten` aktivieren


-----------------------------------------------------------------------------------------------------------------


# 14. Gerätestatus prüfen: offiziell/inoffiziell

- Über den Gerätestatus kann geprüft werden, ob ein Android-Smartphone die `offizielle Software` `des Herstellers` oder eine `inoffizielle Software (Custom ROMs)` installiert ist.
- Aus Sicherheitsgründen sollten NUR erfahrene Nutzer Geräte mit inoffizieller Software (Custom ROMs) nutzen.
- Außerdem sollte man gebrauchte Geräte nur mit offizieller Software kaufen.
- Status prüfen:
    - `Einstellungen` öffnen
    - `Telefoninfo`
    - `Statusinformationen`
    - `Telefonstatus`


-----------------------------------------------------------------------------------------------------------------
