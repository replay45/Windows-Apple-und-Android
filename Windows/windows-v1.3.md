# Windows


# 1. Windows-Sperrbildschirm hacken

## Passwort eines Windows-Benutzerkontos vom Sperrbildschirm aus ändern, um Zugang zum Account zu erhalten.



### Wichtig:
Online-Benutzerkonten oder Geräte, die Benutzerkonten aus einer Domäne nutzen, könnten zu Problemen führen.
Außerdem schützen Sicherheitsmaßnahmen, wie z.B. das Verschlüsseln der Fesplatte über den [Windows-BitLocker](https://de.wikipedia.org/wiki/BitLocker#:~:text=BitLocker%20ist%20eine%20propriet%C3%A4re%20Festplattenverschl%C3%BCsselung,mit%20dieser%20Software%20Daten%20gesch%C3%BCtzt.), vor diesem "Hack".
Auch ein BIOS/UEFI Passwort schützt u.a. davor, die "Bootreihenfolge" zu ändern, womit die Möglichkeiten, über USB-Stick zu booten, verringert werden.


Die Anleitung wurde ausschließlich auf Windows 10 getestet !


-----------------------------------------------------------------------------


1. erste Option

- 1.1) Um in die `erweiterten Optionen` zu gelangen: `Shift Taste drücken`, während auf den `Neustart-Knopf` unten links im Anmeldefenster gedrückt wird.
- 1.2) In den `erweiterten Optionen` zu `Problembehandlung` navigieren, dann zu `erweiterte Optionen` und die `Eingabeaufforderung` öffnen.


### Die erste Option ist leider nicht immer möglich, daher kann auch Option 2 genutzt werden.


2. zweite Option

- 2.1) Daher über einen `win10 Boot USB Stick` booten, anstatt windows zu installieren, jedoch dort mit der Tastenkombination `Shift und F10` CMD öffnen.
- 2.2) Einen Win10-Boot-/ Installations-USB-Stick kann mit dem [Media Creation Tool](https://www.microsoft.com/de-de/software-download/windows10) erstellen werden.


-----------------------------------------------------------------------------


- Das Laufwerk, wo Windows installiert ist, muss angesprochen werden, also z.B. `c:/` (meistens ist es das installations Laufwerk `c:/`).
  
- Befehle, die nacheinander eingegeben werden müssen:		
								
								c:

								cd Windows\System32
							
								rename utilman.exe utilman.exe.lol

								copy cmd.exe utilman.exe


- a) Komandozeile (cmd) mit `$ exit` oder dem Kreuz oben rechts in der Ecke schließen.

- b) Installation beenden (abbrechen)

- c) Der PC wird neu gestartet, dabei den USB Stick entfernen, damit der Sperrbildschirm erscheint.


-----------------------------------------------------------------------------


3. Schutz vor Antischadsoftware-Frühstarts deaktivieren

- In die automatischen Reparatureinstellungen von win 10 kommen: `Shift Taste und Neustart-Knopf unten rechts auf dem Sperbildschirm gleichzeitig drücken.`

- Zuerst zu `Problembehandlung` dann zu `erweiterten Optionen` und `Starteinstellungen` auswählen.

- Anschließend auf `Neu starten` klicken.

- `Option 8` auswählen (Schutz des Antischadsoftware-Frühstarts deaktivieren)

- Unten rechts auf die erleichterte Bedienung klicken und es sollte sich die Kommandozeile öffnen.


-----------------------------------------------------------------------------


4. Passwort ändern

- Um das Passwort nun in CMD auf dem Sperrbildschirm zu ändern:
```
$ net user "(hier kommt der name des Benutzers rein und die Anführungszeichen nicht vergessen)" *
```
- (Beispiel: `$ net user "User" *` )


- Nun das neue Passwort eingeben !


-----------------------------------------------------------------------------


5.  Einen neuen Benutzer anlegen

```
$ net user DEN BENUTZERNAMEN HIER REIN SCHREIBEN HIER PASSWORT SCHREIBEN /add    
```
- (Beispiel: `$ net user Hacker 1234 /add`)


Den hinzugefügten Nutzer zum Admin machen:
```
$ net localgroup administrators HIER DER BENUTZERNAME /add
```
- (Beispiel: `$ net localgroup administrators Hacker /add`)


-----------------------------------------------------------------------------


# 2. Einen gewöhnlichen USB-Stick als Schlüssel zur Windows-Anmeldung nutzen:

## Dafür kann z.B. das Tool [USB-LOGON](https://usblogon.quadsoft.org/de/) verwendet werden.


Ein handelsüblicher USB-Stick kann zu einem Schlüssel, für die Anmeldung an einem Windows PC konfiguriert werden.
Nach der Konfiguration kann der USB-Stick als alternative Anmeldemethode zum Passwort in Windows verwendet werden.
Zudem kann eingestellt werden, ob beim Einsetzen des USB-Sticks zusätzlich ein Passwort abgefragt werden soll,
oder das Einsetzen des konfigurierten USB-Sticks ausreicht.
Außerdem kann separat eingestellt werden, was passieren soll, wenn der USB-Stick entfernt wird.



-----------------------------------------------------------------------------


# 3. Windows PC in eine Domäne hinzufügen


Um einen Windows PC in eine Domäne hinzufügen zu können, muss dieser natürlich im gleichen Netzwerk wie der Domäne-Server sein.
Bevor die Einstellungen vorgenommen werden, sollte daher geprüft werden, ob der PC in dem richtigen Netzwerk ist.


- Folgende Schritte durchführen:
	- Windows Einstellungen öffnen
	- System
	- Info
	- rechts unter `Verwandte Einstellungen`
	- auf `Diesen PC umbenennen (fortgeschritten)` klicken

- Nun öffnet sich ein neues Fenster
	- Unter dem Punkt Domäne/Arbeitsgruppe auf `Ändern` gehen.
	- Von `Arbeitsgruppe` auf `Domäne` wechseln und diese eingeben sowie bestätigen.


Nach einem Neustart sollte der PC erfolgreich in die Domäne hinzugefügt worden sein.


----------------------------------------------------------------------------------------------------------


# 4. Cortana über PowerShell deinstallieren

## Den Sprachassistenten [Cortana](https://support.microsoft.com/de-de/topic/was-ist-cortana-953e648d-5668-e017-1341-7f26f7d0f825), per PowerShell vollständig entfernen:


- In die Windows-Suche `PowerShell` eigeben und als Administrator mit Rechtsklick öffnen.

- Bestätigen der Frage, ob durch diese App Änderungen an dem Gerät vorgenommen werden dürfen, mit `Ja`.



- Hier nun hinter der Information zum System (z.B.” \system32>”) den folgenden Befehl eingeben:
```
$ Get-AppxPackage -allusers Microsoft.549981C3F5F10 | Remove-AppxPackage
```




- Bestätigen mit der Return-Taste – "Cortana" wird daraufhin für alle Benutzer des PCs deinstalliert.

- Es erscheint kurz eine grün hinterlegte Statusmeldung, die anzeigt, dass Powershell arbeitet.
Danach erscheint wieder die vorherige Anzeige.


- "Cortana" ist nun erfolgreich deinstalliert.


-----------------------------------------------------------------------------


# 5. Microsoft Edge deinstallieren


## WICHTIG !

## Update-1: Microsoft hat ein Update veröffentlicht, mit dem der Edge-Browser trotz Deinstallation und Blockung zurückkehrt und sich NICHT mehr mit dem Befehl entfernen lässt !!!

## Update-2: Dank eines neuen EU Gesetzes muss der Edge Browser nun jedoch auch benutzerfreundlich deinstalliert werden können. Dies ist jedoch nur möglich, wenn bei der Ersteinrichtung von Windows auch die Region eines EU Landes ausgewählt wurde, da zum aktuellen Zeitpunkt dieses Updates nur in der EU das Gesetz gilt.



1. anderen Browser installieren (z.B. Firefox oder Brave)

2. Explorer öffnen  

        a) auf Laufwerk C gehen

        b) Programme (x86)

        c) Microsoft

        d) Edge

        e) Application

        f) den Ordner mit der Versionierung öffnen (z.B.90.0.818.62)

        g) Installer

        h) oben links auf Datei (blaues Kästchen) 

        i) mit Windows Powershell als Administrator ausführen



3. In Windows Powershell Edge deinstallieren:
```
$ .\setup.exe --uninstall --system-level --verbose-logging –force-uninstall
```



-------------------------------------------------------------------------------------------------------------



### Microsoft Edges automatische Installation blocken:


__WICHTIG__: 
Optionaler Teil, nicht für die eigentliche Deinstallation erforderlich ! -> Verhindert, dass Edge erneut installiert wird !



1. [Edge Blocker herunterladen](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbnJfNVA5cmpfWG5wY2lBQlhoem9BTWFOS3Ntd3xBQ3Jtc0ttTmJjbTk5VU1UQVY2LU9iR1o1R0J5UWI4cUpyeUhPNU5rcVdQTDEwMG9vMXllVEpaOVdiRFpIOWJ3N2U5dzgyWndpNWdCSGIyb2Z3QU9EdFJ0WkEtOFhQSE9oYjF1dEtQRHlyRDdDMExGS1plcWp6Yw&q=https%3A%2F%2Fmsedgeblockertoolkit.blob.core.windows.net%2Fblockertoolkit%2FMicrosoftEdgeChromiumBlockerToolkit.exe)


2. a) Editor öffnen und den Eintrag einfügen:

Windows Registry Editor Version 5.00

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\EdgeUpdate]
“DoNotUpdateToEdgeWithChromium”=dword:00000001
```


        b) Datei als Block.reg speichern und Dateityp als "alle Datein" auswählen.

        c) Zusätzlich auf desktop speichern.

        d) Doppelklick auf die "Block.reg" Datei bestätigen mit JA.

        e) Den runtergeladenen Blocker ausführen und Ordner auswählen.

        f) cmd in start öffnen als administrator ausführen !!!

        g) Ordnerverzeichnis in cmd eingeben:

```
cd c:\edge Blocker
```
```
dir 
```

        h) Als nächstes in CMD eingeben:
(zur eventuellen Überprüfung in CMD eingeben, um zu erfahren welcher der richtige Befehl ist: `$ EdgeChromium_Blocker.cmd \?`)

```
$ EdgeChromium_Blocker.cmd /b
```

i) Nun sollte dort stehen: `"Der Vorgang wurde erfolgreich beendet."`.



------------------------------------------------------
