# Android

`Anleitung erstellt am 20.8.2024, zuletzt bearbeitet am 15.10.2024`


# Inhaltsverzeichnis
1. Entwicklermodus in den Einstellungen aktivieren (Samsung)
2. Sicherer Ordner (Samsung)
3. Gerätewartung (Samsung)
4. Fenster anheften / App anheften (Samsung)
5. Samsung Cloud
6. Spionageschutz: Kamera, Mikrofon & Sensoren vollständig & systemweit blockieren (Sicherheitsrichtlinie)
7. Intelligent Wi-Fi - Connectivity labs (Samsung)
8. Benachrichtigungsverlauf (Samsung)


-----------------------------------------------------------------------------------------------------------------


# 1. Entwicklermodus in den Einstellungen aktivieren (Samsung)

`Zuletzt getestete Android-Version: 14`


### Disclaimer
Die Nutzung des Entwicklermodus unter Android erfolgt auf eigene Gefahr !
Die Nutzung kann zu Instabilitäten, Datenverlust oder Sicherheitsrisiken führen.
Außerdem können die Garantieleistungen beeinträchtigt werden.
Die Optionen sollten daher unter besonderer Vorsicht genutzt werden.


### Was ist der Entwicklermodus ?
Die Entwickleroptionen sind versteckte Einstellungen, die häufig von Entwicklern und Testern genutzt werden.
Dort können z.B. Debugging Optionen genutzt werden.


- Aktivieren:
    - Einstellungen öffnen.
    - `Telefoninfo`
    - `Softwareinformationen`
    - auf `Buildnummer` drücken bis zur PIN/Passwortabfrage 
    - Unter "Telefoninfo" erscheint nun ein neuer Reiter, der"Entwicklermodus".


- Deaktivieren:
    - Um den Entwicklermodus zu deaktivieren, in die Entwickleroptionen gehen und den Regler auf "Aus" stellen.


### nützliche Optionen aus dem EntEntwicklermodus

- ausführliche WLAN Protokollierung & Scan-Drosselung
    - Mehr Details wie Verbindungsinformationen im WLAN Menü anzeigen.
    - Scan-Drosselung verbessert die Netzwerkleistung und spart Akkuladung.

- Animationsfaktor (Animationen im System verkürzen/deaktivieren)
    - unter `Fensteranimationsfaktor`, `Übergangsanimationsfaktor` & `Animationsdauerfaktor` können die Faktoren für die Animationen eingestellt werden. Mit `aus` werden die Animationen deaktiviert, was häufig bei älteren Geräten dafür sorgt, dass sich das Gerät etwas schneller anfühlt.



-----------------------------------------------------------------------------------------------------------------


# 2. Sicherer Ordner (Samsung)

`Zuletzt getestete Android-Version: 14`


### Was ist der [sichere Ordner](https://www.samsungknox.com/de/solutions/personal-apps/secure-folder) ?

Der sichere Ordner ist ein Bereich auf Samsung Smartphones, in dem man passwortgeschützt Dateien, Bilder, Videos usw. sicher speichern kann, ohne dass diese in der normalen Galerie oder im Dateimanager zu finden sind.
Außerdem können auch Apps separat installiert werden, ohne dass diese im App Menü erscheinen.
    
Das heißt, dass alle Aktionen, Dateien, sowie Apps keinen Einfluss auf den normalen Bereich des Smartphones haben.
Das ist z.B. besonders praktisch, wenn man sich mit zwei Accounts in einer App anmelden möchte, auch wenn  diese die Dual Messenger-Funktion nicht unterstützt.

- In den Einstellungen unter `Sicherheit & Datenschutz` -> `Weitere Sicherheitseinstellungen` kann der sichere Ordner aktiviert werden. Danach ist er im App-Menü zu finden.


-----------------------------------------------------------------------------------------------------------------


# 3. Gerätewartung (Samsung)

`Zuletzt getestete Android-Version: 14`

### Was ist die [Gerätewartung](https://www.samsung.com/de/support/mobile-devices/galaxy-geraetewartung/) ?

In der Gerätewartung kann man die `Leistung` des Smartphones `optimieren`, den `RAM-Speicher leeren` und den `Zustanad des Akkus`, sowie die `Nutzung des Speichers` überprüfen.
Man findet ebenfalls die Option `App-Schutz` mit der man das Smartphone auf schädliche Apps prüfen kann.


-----------------------------------------------------------------------------------------------------------------


# 4. Fenster anheften / App anheften (Samsung)

`Zuletzt getestete Android-Version: 14`

- Mit der Funktion App anheften, bei früheren Android Versionen auch als "Fenster anheften" bekannt, kann man eine App anheften und wenn man diese App verlassen will, muss das Gerät erneut entsperrt werden. Damit kann man jemand anderem sein Gerät geben, ohne dass dieser die App wieder verlassen kann und das Gerät durchsuchen kann.
Wenn man daher die Funktion nutzt, ist man auf die angeheftete App beschränkt.

- Die Funktion kann unter `Sicherheit und Datenschutz` -> `Weitere Sicherheitseinstelllungen` und `App Anheften` aktiviert werden.

- Um die Funktion nun nutzen zu können, muss man in die Übersicht `Aktuelle Anwendungen` wechseln und dann auf das App-Symbol klicken.
In dem Menü erscheint nun die Option `Diese App anheften`.


-----------------------------------------------------------------------------------------------------------------


# 5. Samsung Cloud & Samsung Account

# a) [Samsung Cloud](https://www.samsung.com/de/apps/samsung-cloud/) Ende-Zu-Ende Verschlüsselung


### Warnung:
Auf die von Samsung angebotene Option zur Verschlüsselung der Cloud sollte man sich niemals verlassen. Da bei proprietären Angeboten nicht garantiert werden kann, dass trotz Verschlüsselung nicht doch eine Hintertür offen bleibt.

Auch wenn es sich unbedingt empfiehlt, die Verschlüsselung zu aktivieren, sollte man sich dessen bewusst sein, dass man auch nach Aktivierung der Verschlüsselung keine absolute Sicherheit erhält.
Dies gilt natürlich für alle proprietären Verschlüsselungsoptionen, nicht nur für die Samsung Cloud.


### sichere Cloud
Wer nach einer sicheren Cloud-Lösung sucht, kann sich einen [NAS (Homeserver)](https://de.wikipedia.org/wiki/Network_Attached_Storage) im Heimnetzwerk einrichten, oder wer kein NAS kaufen möchte, kann auch z.B. einen [SFTP-](https://de.wikipedia.org/wiki/SSH_File_Transfer_Protocol) oder [SMB](https://de.wikipedia.org/wiki/Server_Message_Block)-Server auf einem handelsüblichen Computer oder auch auf einem [RaspberryPI](https://www.raspberrypi.com/) installieren und diesen als Homeserver betreiben.

Eine alternative Cloud-Lösung ist die [Nextcloud](https://nextcloud.com/), die man zuhause wahlweise auf einem NAS oder einem handelsüblichen Computer, sowie auch bei einem externen Hosting-Anbieter einrichten kann.

Dabei behält man selbst die Kontrolle über seine Daten und kann sichere Verschlüsselungsmethoden wählen.
Außerdem kann man ein NAS, einen Homeserver, oder die [Nextcloud](https://nextcloud.com/) für weitaus mehr verwenden, als nur für das Datei-Backup.


### Samsung Cloud Verschlüsselung aktivieren
Dafür in die Einstellungen gehen und den Reiter `Samsung Account` auswählen.
Danach unter `Apps und Funktionen` `Samsung Cloud` wählen und auf die 3 Punkte oben rechts klicken und unter dem Punkt `Sicherheit` den `erweiterten Schutz` auswählen.
Nun kann die Verschlüsselung für die Sicherungsdaten und/oder für die synchronisierten Daten aktiviert werden.

- Achtung:
Auf älteren Geräten ist die Verschlüsselung möglicherweise nicht oder nur zum Teil verfügbar.


### Wiederherstellungsschlüssel
Es ist sehr wichtig, den Wiedererstellungsschlüssel gut aufzubewahren, um die Daten entschlüsseln zu können.
Am besten sichert man den Wiederherstellungsschlüssel in einem separaten Passwortmanager, der auch unabhängig von der Samsung Cloud funktioniert.

-----------------------------------------------------------------------------------------------------------------

# b) [Samsung Account](https://v3.account.samsung.com/dashboard/intro) Einstellungen / Funktionen


### Profilinfos / Geräte
- Hier können Informationen angegeben werden und angemeldete Geräte verwaltet werden.


### Sicherheit und Datenschutz
- Hier sollte die Option "Verbesserung von personalisierter Werbung" unbedingt `deaktiviert` sein.
- Außerdem kann hier die Zwei-Faktor-Verifizierung aktiviert werden, was ebenfalls die Sicherheit des Kontos erhöht.
- Es können auch Kontoaktivitäten eingesehen und das Passwort geändert werden.


### Apps & Funktionen
- Über den Reiter Samsung Cloud können die Apps, die synchronisiert, verwaltet werden.


### Hinweis
- Wer eine sichere Cloud für seine Daten sucht, findet unter dem Punkt 5.a) `sichere Cloud` einige Hinweise zu alternativen Möglichkeiten, die sicherer und datenschutzfreundlicher sind.


-----------------------------------------------------------------------------------------------------------------


## 6. Spionageschutz: Kamera, Mikrofon & Sensoren vollständig & systemweit blockieren (Sicherheitsrichtlinie)

`Zuletzt getestete Android-Version: 14`

### Kamera, Mikrofon & andere Sensoren über das QuickPanel nach Belieben deaktivieren und wieder aktivieren
Wer Angst vor Spionage hat, oder verhindern möchte, dass Andrid oder Apps auf die Sensoren zugreifen können, kann `Sensors Off` nutzen, um eine Sicherheitsrichtline zu aktivieren, die den Zugriff auf Sensoren, Mikrofon oder Kamera systemweit blockiert.

Dabei sollte beachtet werden, dass einige Funktionen, wie z.B. "Bildschirm drehen" von der Deaktivierung der Sensoren beeinträchtigt werden können.


- Überprüfen, ob die `Sensors Off` Funktion aktiv ist:

Wenn man also nach der Deaktivierung der Sensoren versucht, die Kamera App zu öffnen, wird man feststellen, dass diese sich nicht mehr öffnen lässt.


### Schnelleinstellung aktivieren
- In den `Entwicklermodus` gehen - wie dieser aktiviert werden kann, ist in `Punkt 1` beschrieben.
- Zu `Entwicklerkacheln f. Schnelleinst.` scrollen.
- Nun die Option `Sensors Off` auswählen.
- Jetzt sollte eine Verknüpfung im QuickPanel erscheinen.


-----------------------------------------------------------------------------------------------------------------


## 7. Intelligent Wi-Fi - Connectivity labs (Samsung)

`Zuletzt getestete Android-Version: 14`

### Was sind die Connectivity Labs Funktionen in den "Intelligent Wi-Fi" Optionen ?
Die Connectivity Labs Funktionen sind Netzwerkeinstellungen, zur Verbesserung und Analyse der Leistung, sowie Verbindungsqualität.
Neben dem `weekly report` für die Datennutzung ist `Wi-Fi inspection` eine interessante Option, mit der man die Verbindungsqualität einsehen kann.


### Aktivieren der Optionen
- Einstellungen öffnen
- Verbindungen
- WLAN
- Auf die 3 Punkte rechts oben klicken
- Intelligent Wi-Fi
- Auf den Schriftzug `Intelligent Wi-Fi` mit der Versionsnummer tippen, bis die `Connectivity labs` Option erscheint.


### Wi-Fi inspection
- `Wi-Fi inspection`
- Auf `Start` klicken und `WLAN` auswählen.
- Durch das Menü klicken und Analyse starten.
- Nun kann die Verbindungsqualität detailliert eingesehen und der Standort mit der besten Verbindungsqualität bestimmt werden.


-----------------------------------------------------------------------------------------------------------------


# 8. Benachrichtigungsverlauf (Samsung)


### Was ist der Benachrichtigungsverlauf ?
Im Benachrichtigungsverlauf werden Benachrichtigungen aufgezeichnet, um sie auch einsehen zu können, wenn die Benachrichtigung bereits aus der Benachrichtigungsleiste gelöscht wurde.


### Den Benachrichtigungsverlauf aktivieren / deaktivieren
In den Einstellungen unter `Erweiterte Einstellungen` kann der `Benachrichtigungsverlauf` aktiviert oder deaktiviert werden.


-----------------------------------------------------------------------------------------------------------------
