# Sicherheit auf Android

`Anleitung erstellt am 8.12.2024, zuletzt bearbeitet am 12.1.2025`

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

- gesunden Menschenverstand mitbringen
- ein gewisses Maß an Skepsis ist immer gut
- Datenminimierung: Nur personenbezogene Daten angeben, wenn unbedingt notwendig
- nur in Online-Accounts einloggen, wenn nötig
- regelmäßiges Installieren von Updates
- nicht mehr benötigte Programme deinstallieren
- keine unbekannten Befehle in einem Terminal (wie [Termux](https://termux.dev/en/)) ausführen
- Backups erstellen
- Werbe-ID löschen, um Tracking zu verhindern - Punkt 10.
- Passwortsperre nutzen (zur automatischen Geräteverschlüsselung bei Android)
- Passwortmanager mit starken Passwörtern nutzen - empfohlen: [KeePassXC](https://keepassxc.org/) oder [BitWarden](https://bitwarden.com/de-de/)
- 2‑Faktor-Authentifizierung nutzen - [2FAS](https://2fas.com/)
- Vorsicht vor Scam-E-Mails und E-Mail Anhänge
- einen guten E-Mail-Client nutzen - [Thunderbird](https://www.thunderbird.net/de/) & [K-9](https://k9mail.app/)
- Acht geben, auf was im Internet heruntergeladen wird und welche Seiten besucht werden
- keine unbekannten/ vermeindlich gefundenen USB-Sticks verwenden
- einen sicheren Browser, wie [Firefox](https://www.mozilla.org/de/firefox/new/) oder [Brave-Browser](https://brave.com/de/) verwenden
- Browser datenschutzfreundlich einstellen
- AdBlocker verwenden - [uBlock Origin](https://ublockorigin.com/de)
    - mehr zu sicher & anonym im Internet surfen unter [ethical hacking & Cyber Security/ Sicherheit im Internet/ anonym & sicher im Internet surfen](https://github.com/replay45/ethical-hacking-und-cybersecurity/tree/main/browser-%26-sicher-surfen)


-----------------------------------------------------------------------------------------------------------------


# 2. DNS-Server auf Android

`Zuletzt getestete Android-Version: 14`

- Hinweis: 
    - Das Ändern des DNS-Servers zu einem sicheren Anbieter, verhindert ohne Implementierung einer Verschlüsselung oder Signierung keine Man in the Middle Angriffe oder Tracking !

### Was ist ein DNS-Server ?
Ein DNS-Server `übersetzt Domainnamen` wie "google.de" `in IP-Adressen`, denn Domains sind für uns Menschen, im Gegensatz zu IP-Adressen, einfacher zu merken.
Außerdem gibt es nicht genügend verfügbare IPv4-Adressen, daher können diese sich auch ändern, was jedoch dank der DNS-Server kein Problem ist.
- [Cloudflare - Was ist ein DNS-Server](https://www.cloudflare.com/de-de/learning/dns/what-is-a-dns-server/)


### Wieso den DNS-Server ändern ?
- Standardmäßig nutzt man die DNS-Server des Internetanbieters, diese sind jedoch häufig eher langsamer und wenn man `verhindern` möchte, dass der `Internetprovider bzw. Mobilfunkanbieter einsehen kann, welche Domains man aufruft`, ist es sehr ratsam, die DNS-Server von [Cloudflare](https://www.cloudflare.com/) zu nutzen.
- Den DNS-Server kann man auf allen gänigen Desktop-Betriebsystemen sowie auf dem Smartphone, als auch in vielen gänigen Routern ändern.
- Wie man seinen eigenen kleinen DNS-Server mit Pi-hole erstellen kann, wird unter [Raspberry-Pi/RaspberryPI-Netzwerk-Projekte](https://github.com/replay45/Linux-RaspberryPI-NextCloud/tree/main/raspberry-pi) gezeigt.
- [Cloudflare](https://www.cloudflare.com/) legt dabei den `Fokus` auf `Datenschutz & Sicherheit` und bietet dennoch sehr `schnelle DNS-Server`.


### Privates DNS - DNS-Server für alle Verbindungen einstellen & DNS-Verschlüsselung
- `Bevorzugten DNS-Server` für `alle Verbindungen` (WLAN & mobile Daten) einstellen und `Verschlüsselung(DoT)` nutzen.
- Diese Einstellungen `überschreibt` alle anderen DNS-Server !
    - `Einstellungen` öffnen
    - `Verbindungen`
    - `Weitere Verbindungseinstellungen`
    - `Privates DNS`
    - `Hostname des Anbieters des privaten DNS`
    - einfügen: `one.one.one.one`
    - `Speichern` klicken


### WLAN - DNS-Server manuell für eine bestimmte Verbindung ändern
- Wenn ein DNS-Server unter der Option `Privates DNS` eingestellt ist, wird diese Option unbrauchbar.
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


### Alternative Möglichkeiten - VPN & Pi-Hole
- Wer selber einen DNS-Server im Heimnetz hosten möchte, kann das z.B. mit [Pi Hole](https://pi-hole.net/) tun.
- Der [Pi Hole](https://pi-hole.net/) kann u.a. als standard-DNS-Server im Router eingestellt werden und über `VPN` in das Heimnetzwerk, kann dieser auch von überall genutzt werden.
- Eine VPN-Verbindung bietet u.a. mehrere Vorteile, wie z.B. eine sichere Verbindung in dasd Heimnetzerk, bei unsicheren WLAN-Verbindungen oder Zugriff auf Geräte in Heimnetzwerk, wie ein NAS/Homeserver.
- Eine weitere Möglichkeit wäre z.B. [Pi Hole](https://pi-hole.net/) über Dyn-DNS aus dem Internet erreichbar zu machen, um Pi-Hole als DNS-Server für die Option `Privates DNS` einzustellen.


### Fazit - die optimale Einstellungen treffen
- Um immer den gewünschten DNS-Server nutzen zu können, die Option `Privates DNS` mit `Hostname des Anbieters des privaten DNS` verwenden (Option überschreibt alle anderen Optionen).
- Dabei empfehlen sich die DNS-Server von [Cloudflare](https://www.cloudflare.com/): `one.one.one.one`
- Alternativ kann ein eigener DNS-Server mit Pi-Hole genutzt werden. Dieser kann wahlweise z.B. über einen VPN zum Heimnetzwerk oder über DynDNS-Domain oder auf einem externen Server eingerichtet werden.
- Mehr zu DNS-Servern und Pi-Hole unter [Linux-RaspberryPI-NextCloud/Raspberry-Pi](https://github.com/replay45/Linux-RaspberryPI-NextCloud/tree/main/raspberry-pi)


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
