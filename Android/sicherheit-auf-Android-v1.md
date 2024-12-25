# Sicherheit auf Android

`Anleitung erstellt am 8.12.2024`


## Inhaltsverzeichnis
1. grundlegende Sicherheitstipps
2. Spionageschutz: Kamera, Mikrofon & Sensoren vollständig & systemweit blockieren (Sicherheitsrichtlinie)
3. folgt in Kürze
4. Einstellungen: Sicherheit und Datenschutz (Samsung)
5. "Passwörter sichtbar machen" - Funktion deaktivieren
6. Sperrbildschirm: Verhindern, dass Netzwerk- & Sicherheitseinstellungen geändert werden können (Samsung)
7. Spezieller Zugriff & Berechtigungsverwaltung für Apps (Samsung)
8. auf schädliche Apps prüfen (PlayStore & Gerätewartung)
9. Standort: Scan Opttionen ausschalten (WLAN & Bluetooth)
10. google WerbeID löschen & Diagnosedaten deaktivieren (google Konto auf Android)
11. Galaxy-AI - Verarbeitung nur auf dem Gerät (Samsung)


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


# 2. Spionageschutz: Kamera, Mikrofon & Sensoren vollständig & systemweit blockieren (Sicherheitsrichtlinie)

`Zuletzt getestete Android-Version: 14`

### Kamera, Mikrofon & andere Sensoren über das QuickPanel nach Belieben deaktivieren und wieder aktivieren
- Was bringt die Funktion (Sicherheitsrichtline)
    - Wer Angst vor `Spionage` hat oder `unbefugten Zugriff` auf Kamera oder Mikrofon verhindern möchte, kann `Sensors Off` nutzen, um eine Sicherheitsrichtline zu aktivieren, die den `Zugriff auf Sensoren`, wie Mikrofon oder Kamera `systemweit blockiert`.

- Beeinträchtigungen
    - Dabei sollte beachtet werden, dass einige Funktionen, wie z.B. "Bildschirm drehen" von der Deaktivierung der Sensoren beeinträchtigt werden können.


- `Sensors Off`-Funktion überprüfen
    - Wenn man also nach der Deaktivierung der Sensoren versucht, die Kamera App zu öffnen, wird man feststellen, dass diese sich nicht mehr öffnen lässt.


### Schnelleinstellung freischalten
- In den `Entwicklermodus` gehen - wie dieser aktiviert werden kann, ist in diesem Ordner in der Datei [android]() unter `Punkt 1` beschrieben.
- Zu `Entwicklerkacheln f. Schnelleinst.` scrollen.
- Nun die Option `Sensors Off` auswählen.
- Jetzt sollte eine neue Verknüpfung im `QuickPanel` erscheinen.


-----------------------------------------------------------------------------------------------------------------


# 3. folgt in Kürze


-----------------------------------------------------------------------------------------------------------------


# 4. Einstellungen: Sicherheit und Datenschutz (Samsung)

`Zuletzt getestete Android-Version: 14`

### Sicherheit und Datenschutz
- Unter diesem Reiter können einige Optionen zur Sicherheit und zum Datenschutz in einer Übersicht eingesehen werden.


### Übersicht (Vorschläge)
- Hier werden vorgeschlagene Einstellungen angezeigt.
- Die Punkte `Sperrbildschirm`, `App-Sicherheit` und `Updates` sollten erfüllt werden, da sie zur elementaren Sicherheit beitragen.


### weitere Sicherheitseinstellungen
- `Verbesserter Datenschutz` (sofern ein Samsung-Konto verwendet wird)
- `SD-Karte verschlüsseln` (sofern eine SD-Karte verwendet wird)
- `USB-Verbindung blockieren, wenn gesperrt`, verhindert Angriffe über den USB-Port bei gesperrtem Bildschirm
- `Trusted Agents`: Deaktivierung bewirkt mehr Sicherheit


### Datenschutz
- `Berechtigungsverwaltung`: Hier können die Berechtigungen für Apps gesetzt werden. Mehr Berechtigungen können unter `Apps/Spezieller Zugriff` (Punkt 7) gesetzt werden.
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


# 5. "Passwörter sichtbar machen" - Funktion deaktivieren

`Zuletzt getestete Android-Version: 14`

### Was ist die "Passwörter sichtbar machen" Option ?
Wenn die Funktion aktiviert ist, wird bei der Eingabe von Passwörtern die Eingabe kurz angezeigt, bevor sie mit einem Punkt "verdeckt" wird.


### Funktion deaktivieren
In den Einstellungen unter `Sicherheit und Datenschutz`, `Weitere Sicherheitseinstellungen` und nun die Option `Passwörter sichtbar machen` deaktivieren, damit Passwörter bei der Eingabe nicht mehr angezeigt werden und direkt mit dem Punkt "verdeckt" werden.


-----------------------------------------------------------------------------------------------------------------


# 6. Sperrbildschirm: Verhindern, dass Netzwerk- & Sicherheitseinstellungen geändert werden können (Samsung)

`Zuletzt getestete Android-Version: 14`

- Die Funktion sollte standartmäßig aktiv sein.

### Netzwerk und Sicherheit Sperren - Funktion für den Sperrbildschirm
Die Funktion verhindert, dass WLAN, mobile Daten oder Standort mit gesperrtem Display ausgeschaltet werden können.
Das Aktivieren der Funktion ist besonders für den Diebstahlschutz wichtig.


### Funktion aktivieren/deaktivieren
In den Einstellungen zu `Sperrbildschirm und AOD` wechseln und unter `Sichere Sperreinstellungen` überprüfen, ob Funktion aktiv ist und die gewünschte Einstellung setzen.


-----------------------------------------------------------------------------------------------------------------


# 7. Spezieller Zugriff & Berechtigungsverwaltung für Apps (Samsung)

`Zuletzt getestete Android-Version: 14`

### Berechtigungen setzten
- Allgemein gilt: So `wenige Berechtigung wie möglich` und so `viele wie nötig`.
- Jedoch gibt es Apps, z.B. wie die Kamera App, die nunmal Zugriff auf Kamera und Mikrofon benötigt, um Fotos und Videos aufzunehmen.
- Daher muss individuell geprüft werden, ob die App die Berechtigung benötigt.


### Was ist der Spezieller Zugriff und die Berechtigungsverwaltung ?
- Über den speziellen Zugriff können spezielle Berechtigungen für gesetzt werden.
- Dazu gehören kritische Optionen, jedoch benötigen viele Apps weniger Berechtigungen als meistens standartmäßig gesetzt.
- Bei Apps die nicht verwendet werden, können meistens alle Berechtigungen entfernt werden.
- In der Berechtigungsverwaltung können dann die üblichen Berechtigungen für Apps gesetzt werden.


### Berechtigungen über den speziellen Zugriff & die Berechtigungsverwaltung verwalten
- Einstellungen öffen
- Apps
- 3-Punkte Menü (Weitere Optionen)
- Spezieller Zugriff oder Berechtigungsverwaltung auswählen
- Nun gewünschte Einstellungen vornehmen.


-----------------------------------------------------------------------------------------------------------------


# 8. auf schädliche Apps prüfen (PlayStore & Gerätewartung)

`Zuletzt getestete Android-Version: 14`

- Man kann sowie im PlayStore als auch in der Gerätewartung alle Apps auf "schädlich Apps" prüfen.
- `App Schutz` (Gerätewartung):
    - Einstellungen öffnen,
    - Gerätewartung auswählen,
    - Mit der Option `App-Schutz` kann man den Scan starten.
    - Dabei werden Apps auf Maleware und verdächtigen Aktivitäten gescannt.
- Auch im GooglePlay-Store können Apps über `PlayProtect` geprüft werden.
    - Dafür den GooglePlay-Store öffnen,
    - auf das Icon des Google Accounts (oben rechts) klicken und `PlayProtect` auswählen.
    - Hier kann nun ein Scan durchgeführt werden.
    - In den `Einstellungen von PlayProtect` kann man noch die `Erkennung schädlicher Apps verbessern` (Senden von Daten an Google) ausschalten. 

-----------------------------------------------------------------------------------------------------------------


# 9. Standort: Scan Optionen ausschalten (WLAN & Bluetooth)

`Zuletzt getestete Android-Version: 14`

# Wieso diese Optionen deaktivieren ?
- Wenn die Optionen zur Verbesserung der Genauigkeit nicht ausgeschaltet sind, werden WLAN & Bluetooth nie richtig abgeschaltet, auch wenn man sie manuell im Quick-Panel deaktiviert.
- Vorteile beim ausschalten der beiden Optionen:
    - weniger Akkuverbrauch
    - Kontrolle darüber, wann WLAN & Bluetooth ein-/ ausgeschaltet sind
    - Apps das bestimmen des genauen Standortes erschwehren
    
# Ausschalten der beiden Optionen
- Einstellungen öffnen,
- Standort auswählen,
- auf `Standortdienste` klicken,
- `WLAN-Scan` & `Bluetooth-Scanning` deaktivieren.


-----------------------------------------------------------------------------------------------------------------


# 10. google Werbe-ID löschen (google Konto auf Android)

`Zuletzt getestete Android-Version: 14`

# Was ist die Werbe-ID und wieso sollte man sie löschen ?
- Die Werbe-ID ist eine `ID zur Identifizierung` eines `Android-Smartphones` - "Google Advertising ID" (GAID) und bei Apple „Identifier for Advertisers“ (IDFA), ähnlich wie ein Nummernschild, die für `Werbezwecke` genutzt wird.
- Da die Werbe-ID für `Tracking` und `Werbung` verwendet wird, sollte man diese unbedingt löschen.
- Dritte können mit der Werbe-ID Nutzer `online, sowie offline` `tracken`, `Standortdaten` und `Suchanfragen` verknüpfen und speichern, oder `geziehlte Werbung` schalten.
- Daher ist das `Risiko` für `Identitätsdiebstahl`, `Betrug` oder `Manipulation` extrem hoch.


# WerbeID löschen
- Einstellungen öffnen,
- Google auswählen,
- `Alle-Dienste`,
- `Werbung`,
- `Werbe-ID löschen`


-----------------------------------------------------------------------------------------------------------------


# 11. Galaxy-AI - Verarbeitung nur auf dem Gerät (Samsung)

`Zuletzt getestete Android-Version: 14 mit OneUI 6.1.1`

### Wieso sollte man die Option "Daten nur auf Gerät verarbeiten" aktivieren ?
- Beim aktivieren der Option, werden Inhalte nur noch auf dem Gerät, also lokal verarbeitet.
- Um die Inhalte zu verarbeiten werden diese häufig in die Cloud hochgeladen, was potenziell unwerünscht ist.
- Auch wenn dadurch manche Funktionen nicht mehr verfügbar sind, sollte der Datenschutz und der Schutz der Privatsphäre unbedingt ernst genommen werden und daher ist es sehr ratsam die Option zu aktivieren. 


### Option aktivieren
- Einstellungen
- Galaxy AI
- Option `Daten nur auf Gerät verarbeiten` aktivieren.


-----------------------------------------------------------------------------------------------------------------
