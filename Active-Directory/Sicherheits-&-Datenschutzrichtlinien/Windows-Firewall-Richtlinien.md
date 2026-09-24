# [Windows-Defender-Firewall](https://de.wikipedia.org/wiki/Windows-Firewall) über [Microsoft Active Directory](https://de.wikipedia.org/wiki/Active_Directory) konfigurieren

`Anleitung verfasst am 20.9.2026`

`Windows-Server - Active Directory`

- [windowspro.de - Firewall-Regeln](https://www.windowspro.de/wolfgang-sommergut/firewall-regeln-ueber-gruppenrichtlinien-konfigurieren)

------------------------------------------------------------------------------------------------------------------------------


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
  - `Computerkonfiguration` → `Richtlinien` → `Administrative Vorlagen` → `Windows-Komponenten`
  - Hier sind nun alle Vorlagen.
- zurück zur `Gruppenrichtlinienverwaltung`
  - Unter `Domain.local` -> `Domäne` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
  - Zum Verknüpfen das gewünschte Objekt auswählen


------------------------------------------------------------------------------------------------------------------------------


# Firewall-Profile für öffentliches, privates und Domänennetzwerk konfigurieren 
- Über diese Richtlinien kann man die `Windows-Firewall` und die `dazugehörigen Profile` konfigurieren, sodass festgelegt werden kann, in welchem Profil Ein- & Ausgehende Verbindungen erlaubt/verboten sind und es können Firewall Regeln für bestimmte Ports und Programme angelegt werden.
- Zudem können auch `Protokolleinstellungen` gesetzt werden.
- Folgend wird die Einrichtung einer Konfiguration gezeigt, ggf. sind individuelle Anpassungen je nach Umgebung notwendig.


### Wofür die Firewall-Profile ?
- Der Vorteil durch unterschiedliche Profile ist, dass man Firewallregeln einfacher für bestimmte Netzwerke konfigurieren kann.
- Somit erleichert sich die Härtung der Firewall z.B. in öffentlichen Netzwerken ohne die Funktionalität im Domänen-Netzwerk einzuschränken.


### empfohlene Einstellungen
- Grundsätzlich empfiehlt es sich die Windows-Firewall auf allen Profilen auf "Aktiv" zu setzen und es kann aus Sicherheitsgründen im öffentlichen Profil angewählt werden, dass `alle eingehenden Verbindungen blockiert` werden (überschreibt Regeln die Traffic erlauben würden).
- So sollte die Angriffsfläche z.B. bei Laptops in öffentlichen Netzwerken stark verringert werden.
- GGf. könnte man das je nach Situation, in streng kontrollierten Umgebungen auf das private Profil erweitern.


### nicht empfohlen, es sei denn man weiß was man tut:
- Es ist auch möglich über die Richtlinien alle lokalen Firewalleinstellungen zu deaktivieren und nur über die GPO eingestellte Regeln zu erlauben, das sollte man allerdings eher bei Servern einsetzen, denn das kann zu Beeinträchtigungen der Funktionalität führen.


### Richtlinien (z.B. für Clients wie PCs, Laptops...)
- `Computerkonfiguration > Richtlinien > Windows-Einstellungen > Sicherheitseinstellungen > Windows Defender Firewall mit erweiterter Sicherheit > Windows Defender Firewall mit erweiterter Sicherheit - LDAP...`
- Rechtsklick auf `Windows Defender Firewall mit erweiterter Sicherheit - LDAP...` > `Eigenschaften`
- `Domänenprofil`
    - Firewallstatus: `Ein (empfohlen)`
    - Eingehende Verbindungen: `Blockieren (Standard)`
    - Ausgehende Verbindungen: `Zulassen (Standard)`
    - `Einstellungen > Anpassen`: Unicastantworten zulassen : JA
- `Privates Profil`
    - Firewallstatus: `Ein (empfohlen)`
    - Eingehende Verbindungen: `Blockieren (Standard)`
    - Ausgehende Verbindungen: `Zulassen (Standard)`
    - `Einstellungen > Anpassen`: Unicastantworten zulassen : JA
- `Öffentliches Profil`
    - Firewallstatus: `Ein (empfohlen)`
    - Eingehende Verbindungen: `Alle Blockieren`
    - Ausgehende Verbindungen: `Zulassen (Standard)`
    - `Einstellungen > Anpassen`: Unicastantworten zulassen : NEIN

- Unter jedem Profil (Domäne/privat/öffentlich) `Protokollierung > Anpassen` (Optional)
    - verworfene Pakete protokollieren: `Ja`
    - Größenlimit aktivieren durch entfernen des Häkchens
    - z.B. `16.384` eintragen (Wert in KB)


### Richtlinien (z.B. für Windows-Server)
- Es empfiehlt sich eine separate Richtlinie in einer OU für Server anzulegen, dort könnte man dann separate Einstellungen setzen.
- Wenn die (Windows)-Server, die ebenfalls in der Domäne sind nicht öffentlich erreichbar sein sollen, kann das öffentliche Profil (ggf. auch das private Profil) mit `Eingehende Verbindungen`: `Alle Blockieren`
- Unicastantworten für interne Server im öffentlichen Profil auf `NEIN`
- Vorsicht: Wenn lokale Firewallregeln deaktiviert werden, dann müssen alle benötigten Portfreigaben manuell in der Richtlinie unter `Eingehende Regeln` und `Ausgehende Regeln` erstellt werden !


------------------------------------------------------------------------------------------------------------------------------


# Firewallprofile, standardprofile, Netzwerkinterfaces
- Standardmäßig aktivert Windows in öffentlichen Netzwerken das öffentliche Profil.
- Man kann auch via GPO sicherstellen, dass das der Fall ist: `Computerkonfiguration > Richtlinien > Windows-Einstellungen > Sicherheitseinstellungen > Netzwerklisten-Manager-Richtlinien`
    - Nicht identifizierte Netzwerke: `öffentlich`
    - Netzwerke werden identifiziert: `öffentlich`


- Die derzeit aktiven Profile auf den jeweiligen Schnittstellen lassen sich mit folgendem Befehl in der [PowerShell](https://de.wikipedia.org/wiki/PowerShell) überprüfen:
```
> Get-NetConnectionProfile
```

### [VPNs](https://de.wikipedia.org/wiki/Virtual_Private_Network)
- Allerdings gelten die Profile separat für jedes Netzwerkinterface, also wenn in einem öffentlichen Netzwerk eine VPN-Verbindung in das Domänen-Netzwerk hergestellt wird, dann gilt auf dem virtuellen Interface der VPN-Verbindung das Domänen-Firewall-Profil, aber auf dem Interface welches direkt mit dem öffentlichen Netzwerk verbunden ist, wird das öffentliche Profil genutzt.
- Dabei kann es je nach eingesetzter Protokollart vom VPN evtl. auch Abweichungen geben, hier muss ggf. geprüft werden welches VPN-Protokoll eingesetzt wird und ob der Domain-Controller über die VPN-Verbindung erreichbar ist, denn nur wenn der Server auf dem der Domain-Controller läuft erreichbar ist und die Authentifizierung erfolgreich ist, kann das Domänen-Firewall-Profil geladen werden.
- Je nach Umgebung ist das jedoch nicht zwingend problematisch wenn auf dem VPN-Interface das öffentliche Firewall-Profil aktiv ist, hier kommt es ggf. etwas auf die spezifische Umgebung an.


------------------------------------------------------------------------------------------------------------------------------


# Richtlinien prüfen (auf dem Client)
- [Terminal](https://de.wikipedia.org/wiki/Windows_Terminal)/[PowerShell](https://de.wikipedia.org/wiki/PowerShell) öffnen
- GPOs aktualisieren: 
    - `> gpupdate /force`
- Systemsteuerung öffnen: 
    - `> firewall.cpl`
- Es sollte sich die Systemsteuerung öffnen (hier sieht man schon einen Überblick)
- Nun auf `Erweiterte Einstellungen`
- Es öffnet sich ein neues Fenster (Windows Defender Firewall mit erweiterter Sicherheit)
- Hier sollte man in der Übersicht sehen, dass die Firewall in allen Profilen aktiv ist und im besten Fall im öffentlichen Profil alle Eingehenden Verbindungen blockiert (ohne Außnahame) werden.
- Unter `Überwachung` können weitere Details zu den Profilen eingesehen werden (Allgemeine Einstellungen, Protokollierung etc.).


------------------------------------------------------------------------------------------------------------------------------
