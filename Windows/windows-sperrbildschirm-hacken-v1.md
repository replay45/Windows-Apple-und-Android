# Windows-Sperrbildschirm hacken

## Passwort eines Windows-Benutzerkontos vom Sperrbildschirm aus ändern, um Zugang zum Account zu erhalten.

### Wichtig:
Online-Benutzerkonten oder Geräte, die Benutzerkonten aus einer Domäne nutzen, könnten zu Problemen führen.
Außerdem schützen Sicherheitsmaßnahmen, wie z.B. das Verschlüsseln der Fesplatte über den [Windows-BitLocker](https://de.wikipedia.org/wiki/BitLocker#:~:text=BitLocker%20ist%20eine%20propriet%C3%A4re%20Festplattenverschl%C3%BCsselung,mit%20dieser%20Software%20Daten%20gesch%C3%BCtzt.), vor diesem "Hack".
Auch ein BIOS/UEFI Passwort schützt u.a. davor, die "Bootreihenfolge" zu ändern, womit die Möglichkeiten, über einen USB-Stick zu booten, ggf. erschwert werden.


Die Anleitung wurde ausschließlich auf Windows 10 getestet !


-----------------------------------------------------------------------------


1.1. erste Option

- a) Um in die `erweiterten Optionen` zu gelangen: `Shift Taste drücken`, während auf den `Neustart-Knopf` unten links im Anmeldefenster gedrückt wird.
- b) In den `erweiterten Optionen` zu `Problembehandlung` navigieren, dann zu `erweiterte Optionen` und die `Eingabeaufforderung` öffnen.


### Die erste Option ist leider nicht immer möglich, daher kann auch Option 2 genutzt werden.


1.2. zweite Option

- a) Daher über einen `win10 Boot USB Stick` booten, anstatt windows zu installieren, jedoch dort mit der Tastenkombination `Shift und F10` CMD öffnen.
- b) Einen Win10-Boot-/ Installations-USB-Stick kann mit dem [Media Creation Tool](https://www.microsoft.com/de-de/software-download/windows10) erstellen werden.


-----------------------------------------------------------------------------


- Das Laufwerk, wo Windows installiert ist, muss angesprochen werden, also z.B. `c:/` (meistens ist es das installations Laufwerk `c:/`).
  
- Befehle, die nacheinander eingegeben werden müssen:		
								
								c:

								cd Windows\System32
							
								rename utilman.exe utilman.exe.lol

								copy cmd.exe utilman.exe


- c) Komandozeile (cmd) mit `$ exit` oder dem Kreuz oben rechts in der Ecke schließen.

- d) Installation beenden (abbrechen)

- f) Der PC wird neu gestartet, dabei den USB Stick entfernen, damit der Sperrbildschirm erscheint.


-----------------------------------------------------------------------------


1.3. Schutz vor Antischadsoftware-Frühstarts deaktivieren

- In die automatischen Reparatureinstellungen von win 10 kommen: `Shift Taste und Neustart-Knopf unten rechts auf dem Sperbildschirm gleichzeitig drücken.`

- Zuerst zu `Problembehandlung` dann zu `erweiterten Optionen` und `Starteinstellungen` auswählen.

- Anschließend auf `Neu starten` klicken.

- `Option 8` auswählen (Schutz des Antischadsoftware-Frühstarts deaktivieren)

- Unten rechts auf die erleichterte Bedienung klicken und es sollte sich die Kommandozeile öffnen.


-----------------------------------------------------------------------------


1.4. Passwort ändern

- Um das Passwort nun in CMD auf dem Sperrbildschirm zu ändern:
```
$ net user "(hier kommt der name des Benutzers rein und die Anführungszeichen nicht vergessen)" *
```
- (Beispiel: `$ net user "User" *` )


- Nun das neue Passwort eingeben !


-----------------------------------------------------------------------------


1.5.  Einen neuen Benutzer anlegen

```
$ net user DEN BENUTZERNAMEN HIER REIN SCHREIBEN HIER PASSWORT SCHREIBEN /add    

```
- (Beispiel: `$ net user Hacker 1234 /add`)


Den hinzugefügten Nutzer zum Admin machen:
```
$ net localgroup administrators HIER DER BENUTZERNAME /add
```
- (Beispiel: `$ net localgroup administrators Hacker /add`)

