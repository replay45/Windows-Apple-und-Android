# Sicherheit auf Windows


## Inhaltsverzeichnis
1. grundlegende Sicherheitstipps
2. DNS Server - [Cloudflare DNS](https://www.cloudflare.com/)
3. [BitLocker](https://de.wikipedia.org/wiki/BitLocker) aktivieren (mit [TPM](https://de.wikipedia.org/wiki/Trusted_Platform_Module)) - [Festplattenverschlüsselung](https://de.wikipedia.org/wiki/Festplattenverschl%C3%BCsselung)


----------------------------------------------------------------------------------------------------------------------------------------------------------


# 1. grundlegende Sicherheitstipps

### die Grundlagen & allgemeies Verhalten
- Absolute Sicherheit gibt es nie ! - Aufklärung ist der beste Schutz !
- Man sollte immer den gesunden Menschenverstand einschalten.
- Ein gewisses Maß an Skepsis ist immer gut.
- Sicherung von Systemen gegen Diebstahl oder Manipulationen.
- Keine unbekannten/ vermeindlich gefundenen USB-Sticks verwenden !

### Datenschutz & Tracking
- Datenminimierung: Nur personenbezogene Daten angeben, wenn unbedingt notwendig.
- Man sollte sich nur in online-Accounts einloggen, wenn notwendig.
- Die `Werbe-ID löschen` & `personalisierte Werbung deaktivieren`, um Tracking zu minimieren und zu erschweren.
- Cloud-Dienste meiden - eigene Cloud, wie Nextcloud oder NAS im Heimnetz nutzen.
- Sichere und datenschutzfreundliche DNS-Server nutzen.

### Browser & Verhalten im Internet
- Acht geben, auf was im Internet heruntergeladen wird und welche Webseiten besucht werden.
- Einen sicheren Browser, wie [Firefox](https://www.mozilla.org/de/firefox/new/) oder den [Brave-Browser](https://brave.com/de/) verwenden.
- Browser datenschutzfreundlich einstellen und Cookies von Dritt-Anbietern blockieren.
- AdBlocker verwenden - [uBlock Origin](https://ublockorigin.com/de)

### E-Mail
- Vorsicht vor Scam-E-Mails und schädlichen Anhängen.
- Einen sicheren E-Mail-Client ohne Tracker nutzen - [Thunderbird](https://www.thunderbird.net/de/) & [K-9](https://k9mail.app/).

### Authentifizierung & Verschlüsselung
- Festplatten-/ Geräteverschlüsselung aktivieren & Passwortsperre nutzen.
- Passwortmanager mit starken Passwörtern nutzen - empfohlen: [KeePassXC](https://keepassxc.org/) oder [BitWarden](https://bitwarden.com/de-de/)
- 2‑Faktor-Authentifizierung nutzen - [2FAS](https://2fas.com/)

### Software & Daten schützen
- [Open Source](https://de.wikipedia.org/wiki/Open_Source) Software bevorzugen.
- Regelmäßiges Installieren von Updates.
- Nicht mehr benötigte Programme entfernen.
- Backups erstellen.

### Betriebsystem spezifisch (Windows)
- Keine unbekannten Befehle im Terminal ausführen.
- Ein lokales Nutzerkonto verwenden - KEIN Microsoft-Konto nutzen, um Cloudzwang und Tracking zu minimieren ! 


#### Mehr zu `sicher & anonym im Internet surfen` unter [ethical hacking & Cyber Security/Cyber-Security/anonym & sicher im Internet surfen](https://github.com/replay45/ethical-hacking-und-cybersecurity/tree/main/browser-%26-sicher-surfen)


----------------------------------------------------------------------------------------------------------------------------------------------------------


# 2. DNS Server - [Cloudflare DNS](https://www.cloudflare.com/)

`Anleitung zu "DNS Server" am 20.11.2024 erstellt`

- `mehr zu DNS-Servern` unter [Raspberry-Pi/Pi-hole](https://github.com/replay45/Linux-RaspberryPI-NextCloud/tree/main/raspberry-pi)


## Was ist ein DNS Server ?
Ein DNS-Server `übersetzt Domainnamen` wie "google.de" `in IP-Adressen`, denn Domains sind für uns Menschen, im Gegensatz zu IP-Adressen, einfacher zu merken.
Außerdem gibt es nicht genügend verfügbare IPv4 Adressen, daher können diese sich auch ändern, was jedoch dank der DNS-Server kein Problem ist.
- [Cloudflare - Was ist ein DNS-Server](https://www.cloudflare.com/de-de/learning/dns/what-is-a-dns-server/)


## Wieso den DNS Server ändern ?
- Standardmäßig nutzt man die DNS-Server des Internetanbieters, diese sind jedoch häufig eher langsamer und wenn man `verhindern` möchte, dass der `Internetprovider bzw. Mobilfunkanbieter einsehen kann, welche Domains man aufruft` ist es sehr ratsam, die DNS-Server von [Cloudflare](https://www.cloudflare.com/) zu nutzen.
- Den DNS-Server kann man auf allen gänigen Desktop-Betriebsystemen, sowie auf dem Smartphone, als auch in vielen gänigen Routern ändern.

- Wie man seinen eigenen kleinen DNS-Server mit Pi-hole erstellen kann, wird unter [Raspberry-Pi/Pi-hole](https://github.com/replay45/Linux-RaspberryPI-NextCloud/tree/main/raspberry-pi) gezeigt.

- [Cloudflare](https://www.cloudflare.com/) legt dabei den `Fokus` auf `Datenschutz & Sicherheit` und bietet dennoch sehr `schnelle DNS-Server`.

## Hier die Vorteile der [Cloudflare](https://www.cloudflare.com/) DNS-Server
- empfehlenswerter Anbieter, weite Verbreitung
- Geschwindigkeit (schnelle Server)
- Server auf der ganzen Welt
- Fokus auf Datenschutz & Sicherheit
- kein Logging
- ideal für private Nutzer & Haushalte


## DNS Server ändern

- Windows:
    - Einstellungen öffnen
    - Unter `Netzwerk und Internet` die gewünschte WLAN / LAN Verbinung auswählen.
    - Eigenschaften der Verbindung auswählen.
    - In dem Pop-Up `IPv4` aktivieren und IP-Adresse des DNS-Servers einfügen. ([Cloudflare DNS](https://www.cloudflare.com/): primär: `1.1.1.1`, sekundär: `1.0.0.1`).
    - Optional `IPv6` aktivieren und DNS-Servers einfügen.
    - Verschlüsselung über HTTPS (DoH) optional, aber empfohlen, auf `Ein` `(automatische Vorlage)` stellen.

- Router:
    - Wenn man nicht für jedes Gerät den DNS-Server einzeln einstellen möchte, kann man dies auch im Router tun.
    - Je nach Hersteller und Modell können die Optionen abweichen (Vodafone Easy-Boxen unterstützen das Ändern des DNS-Servers in der Regel nicht.)
    - Um den DNS-Server zu ändern, die Option finden, wo der primäre und der sekundäre-DNS-Server festgelegt werden können. Dabei können der primäre- als auch der sekundäre- DNS-Server unterschildliche Server vom gleichen Anbieter sein, oder der sekundäre Server kann wahlweise auch von dem primären Anbieter abweichen, um eine hohe Ausfallsicherheit zu gewährleisten.


----------------------------------------------------------------------------------------------------------------------------------------------------------


# 3. [BitLocker](https://de.wikipedia.org/wiki/BitLocker) aktivieren (mit [TPM](https://de.wikipedia.org/wiki/Trusted_Platform_Module)) - [Festplattenverschlüsselung](https://de.wikipedia.org/wiki/Festplattenverschl%C3%BCsselung)

`Anleitung zu "BitLocker" am 2.5.2025 erstellt`


## Was ist [BitLocker](https://de.wikipedia.org/wiki/BitLocker) ?
- BitLocker ist eine proprietäre Software zur [Festplattenverschlüsselung](https://de.wikipedia.org/wiki/Festplattenverschl%C3%BCsselung) unter Windows, die die gesamte Festplatte verschlüsselt, um Daten bei physischem Diebstahl der Festplatte zu schützen.
- Voraussetzungen:
	- Windows 10/11 Pro, Enterprise oder Education
	- Secure Boot aktiviert
	- [TPM](https://de.wikipedia.org/wiki/Trusted_Platform_Module) muss im [UEFI](https://de.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface) aktiviert sein

- Sobald Änderungen an der Hardware oder dem UEFI vorgenommen werden, fordert Windows beim Boot den Wiederherstellungsschlüssel.


### Windows-Version prüfen
- `Windows + R`
- `winver` eingeben
- Enter
- Version überprüfen


### [TPM](https://de.wikipedia.org/wiki/Trusted_Platform_Module)-Verfügbarkeit prüfen
- `Windows + R`
- `tpm.msc` eingeben
- Enter
- Version überprüfen


## BitLocker auf Windows aktivieren (Festplatte verschlüsseln)
- `Systemsteuerung` öffnen
- `BitLocker`
- Systemlaufwerk wählen (meist `C:`)
- `BitLocker aktivieren`
- Setup-Assistenten folgen
- Empfohlen: `"Gesamtes Laufwerk verschlüsseln (sicherer bei gebrauchten Geräten)"`. Damit wird die gesamte Festplatte verschlüsselt.
- Wiederherstellungsschlüssel auf einem Wechseldatenträger (z.B. USB-Stick) sichern und anschließend am besten in einem Passwortmanager speichern
- Nach der Sicherung des Wiederherstellungsschlüssels den USB-Stick am besten formatieren
- Windows sollte TPM automatisch erkennen.
- Neu starten.


### Hinweis:
- Es wird dringend davon `abgeraten` den Wiederherstellungsschlüssel bei Microsoft zu sichern !
- Dieser sollte langfristig am besten in einem Passwortmanager wie [KeePassXC](https://keepassxc.org/) oder [BitWarden](https://bitwarden.com/de-de/) gesichert werden.


## Prüfen, ob TPM für [BitLocker](https://de.wikipedia.org/wiki/BitLocker) verwendet wird
- [Terminal](https://de.wikipedia.org/wiki/Windows_Terminal) / [PowerShell](https://de.wikipedia.org/wiki/PowerShell) als `Administrator` öffnen
```
$ manage-bde -status C:
```
- Dort sollte unter Schlüsselschutzvorrichtungen `TPM` und `Numerisches Kennwort` stehen.


----------------------------------------------------------------------------------------------------------------------------------------------------------
