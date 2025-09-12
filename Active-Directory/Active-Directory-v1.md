# Active Directory - Domäne - Clients hinzufügen & lokale Benutzerkonten


-----------------------------------------------------------------------------

# 1. Einen Windows PC in eine Domäne (Active Directory) hinzufügen

`Anleitung verfasst am 11.9.2025`

`verwendetes Betriebssystem: Win11 24H2`

### Netzwerk/Server
- Um einen Windows PC in eine Domäne hinzufügen zu können, muss dieser natürlich im gleichen Netzwerk wie der Domäne/Active-Directory-Server sein, alternativ könnte auch eine VPN-Verbindung in das entsprechende Netzwerk Abhilfe schaffen.
- Bevor die Einstellungen vorgenommen werden, sollte daher geprüft werden, ob der PC mit dem richtigen Netzwerk verbunden ist.


### Windows PC in Domäne hinzufügen
- `Windows Einstellungen` öffnen
- `System`
- `Info`
- unter dem Reiter Gerätespezifikationen bei "Verwandte Links" den Punkt `Domäne oder Arbeitsgruppe` auswählen
- Nun öffnet sich ein neues Fenster
- Unter dem Punkt Domäne/Arbeitsgruppe auf `Ändern` gehen.
- Von `Arbeitsgruppe` auf `Domäne` wechseln, `Domänennamen` eingeben und bestätigen.
- ggf. bei Aufforderung mit Administratorkonto der Domäne anmelden.


Nach einem Neustart sollte der PC erfolgreich in die Domäne hinzugefügt worden sein.


-----------------------------------------------------------------------------

# 2. Auf einem lokalen (nicht Domänen) Windows-Benuter anmelden (bei Geräten die mit einer Domäne verbunden sind)

`Anleitung verfasst am 11.9.2025`

`verwendetes Betriebssystem: Win11 24H2`


### auf einem lokalen Benutzer anmelden:
- Damit man sich auf einem lokalen Benuter anmelden kann, also einem Benutzer der lokal auf dem entsprechenden Client ist und kein Domänen-Benutzer ist, kann Foglendes Schema verwendet werden:
- `Hostname\Benutzername`
- Der Hostname ist der Netzwerkname des entsprechenden Clients.


-----------------------------------------------------------------------------
