# [Active Directory](https://de.wikipedia.org/wiki/Active_Directory) - Windows-Domäne


-----------------------------------------------------------------------------

# 1. Einen Windows PC in eine Domäne (Active Directory) hinzufügen

`Abschnitt verfasst am 11.9.2025`

`verwendetes Betriebssystem: Win11 24H2`

### Netzwerk/Server
- Um einen Windows PC in eine Domäne hinzufügen zu können, muss dieser natürlich im gleichen Netzwerk wie der Domäne/Active-Directory-Server sein, alternativ könnte auch eine [VPN](https://de.wikipedia.org/wiki/Virtual_Private_Network)-Verbindung in das entsprechende Netzwerk Abhilfe schaffen.
- Bevor die Einstellungen vorgenommen werden, sollte daher geprüft werden, ob der PC mit dem richtigen Netzwerk verbunden ist.


### Windows PC in Domäne hinzufügen
- `Windows Einstellungen` öffnen
- `System`
- `Info`
- unter dem Reiter Gerätespezifikationen bei "Verwandte Links" den Punkt `Domäne oder Arbeitsgruppe` auswählen
- Nun öffnet sich ein neues Fenster
- Unter dem Punkt Domäne/Arbeitsgruppe auf `Ändern` gehen.
- Von `Arbeitsgruppe` auf `Domäne` wechseln, `Domänennamen` eingeben und bestätigen.
- ggf. bei Aufforderung mit einem Administratorkonto der Domäne anmelden.


Nach einem Neustart sollte der PC erfolgreich in die Domäne hinzugefügt worden sein.


-----------------------------------------------------------------------------

# 2. Auf einem lokalen (nicht Domänen) Windows-Benuter anmelden (bei Geräten die mit einer Domäne verbunden sind)

`Abschnitt verfasst am 11.9.2025`

`verwendetes Betriebssystem: Win11 24H2`


### auf einem lokalen Benutzer anmelden:
- Damit man sich auf einem lokalen Benuter anmelden kann, also einem Benutzer der lokal auf dem entsprechenden Client ist und kein Domänen-Benutzer ist, kann Foglendes Schema verwendet werden:
- `Hostname\Benutzername`
- Der [Hostname](https://de.wikipedia.org/wiki/Hostname) ist der Netzwerkname des entsprechenden Clients.


-----------------------------------------------------------------------------

# 3. Variable für DomainControler

`Abschnitt verfasst am 8.2.2026`

`verwendetes Betriebssystem: Win11 25H2`

- Da sich [Hostnamen](https://de.wikipedia.org/wiki/Hostname) und [IP-Adressen](https://de.wikipedia.org/wiki/IP-Adresse) ändern können, kann man eine Variable verwenden, um den DomainContoler anzugeben.
- Das hat den Vorteil, wenn ein weiterer/neuer/anderer DomainContoler verwedet werden soll, und die Variable in Dokumentationen, Skripten, Befehlen etc. angibt, dann müssen diese bei einem Wechsel nicht bearbeitet werden.

### aktuellen DomainControler für einen PC in einer Domäne in [CMD](https://de.wikipedia.org/wiki/Cmd.exe) abfragen
- Wichtig: Dieser Befehl funktioniert nur in der [Eingabeaufforderung CMD](https://de.wikipedia.org/wiki/Cmd.exe).
    - Ausgabe sollte der Hostname des aktuellen DomainControlers sein.
```
> echo %logonserver%
```

-----------------------------------------------------------------------------
