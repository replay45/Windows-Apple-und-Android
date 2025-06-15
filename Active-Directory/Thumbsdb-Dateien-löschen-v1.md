# Thumbs.db-Dateien von einem Netzlaufwerk löschen

`Anleitung erstellt am 13.2.2025`

`Windows-Server - Active Directory`


-------------------------------------------------------------------------------------------------------------


### Was sind Thumbs.db-Dateien ?
- Thumbs.db-Dateien sind Systemdateien, die von Windows angelegt werden.
- Diese werden dazu verwendet, um Miniaturansichten von Medien zu speichern, damit Windows beim erneuten Öffnen schneller eine Vorschau zeigen kann.
- Man kann diese Dateien bedenkenlos löschen, Windows legt sie dann ggf. erneut an.

### Was ist das Problem mit den Thumbs.db-Dateien auf den Netzlaufwerken ?
- Häufig lassen sich die Thumbs.db-Dateien auf den Netzlaufwerken nicht entfernen, da sie von Prozessen blockiert werden.
- In einem größeren Netzwerk führt das dazu, dass unglaublich viele Thumbs.db-Dateien angelegt werden und diese sich nicht löschen lassen.
- Dabei lässt sich der ganze Ordnerpfad nicht entfernen und das kann dann schnell unübersichtlich werden.



-------------------------------------------------------------------------------------------------------------

# Thumbs.db-Dateien manuell von einem Netzlaufwerk löschen

- [PowerShell](https://de.wikipedia.org/wiki/PowerShell) als `Administrator` öffnen
- Zum Netzlaufwerk navigieren
```
$ cd \\SERVER\PFAD\ORDNER
```

- Überprüfen, ob Thumbs.db-Datei vorhanden ist
```
$  Get-ChildItem -Hidden
```

- Thumbs.db löschen
```
$ Remove-Item -Path "Thumbs.db" -Force
```



# Mehrere Thumbs.db-Dateien aus einem Pfad löschen

- [PowerShell](https://de.wikipedia.org/wiki/PowerShell) als `Administrator` öffnen
- Zum Netzlaufwerk navigieren
```
$ cd \\SERVER\PFAD\ORDNER
```

- Mit `dir` oder `ls` kann der Inhalt eines Ordners angezeigt werden 
```
$ dir
$ ls
```

- Überprüfen, ob Thumbs.db-Datei vorhanden ist
```
$  Get-ChildItem -Hidden
```

- Mehrere Thumbs.db aus einem Pfad löschen
```
$ Get-ChildItem -Path "\\SERVER\PFAD\ORDNER" -Filter "Thumbs.db" -Recurse | Remove-Item -Force
```



### Wenn das Löschen von mehreren Thumbs.db-Dateien fehl schlägt
- Dann mit diesem Befehl überprüfen, ob [PowerShell](https://de.wikipedia.org/wiki/PowerShell) die Dateien findet
```
$ Get-ChildItem -Path "\\SERVER\PFAD\ORDNER" -Filter "Thumbs.db" -Recurse -Force
```


- Danach Attribute zurücksetzen und löschen mit folgendem Befehl
```
$ Get-ChildItem -Path "\\SERVER\PFAD\ORDNER" -Filter "Thumbs.db" -Recurse -Force | ForEach-Object {
    $_.Attributes = 'Normal'
    Remove-Item $_.FullName -Force
}
```


### Falls auch das Zurücksetzten der Attribute fehlschlägt, dann Prozesse beenden
- Überprüfen, wer die Datei verwendet (Freigabe-Sperren ermitteln)
- Auf `Windows-Server` (vom entsprechenden Netzlaufwerk) `einloggen`
- [CMD](https://de.wikipedia.org/wiki/Cmd.exe) öffnen
```
$ openfiles /query | findstr "Thumbs.db"
```

- Falls „openfiles“ nicht aktiviert ist, aktivieren:
```
$ openfiles /local on
```


- Benutzer aus der Datei werfen (Netzwerksperre aufheben)
	- Eingabeaufforderung als Administrator öffnen
```
$ net file
```
```
$ net file [ID] /close
```
Beispiel
```
$ net file 1234 /close
```


### Ein Neustart des Servers kann auch durchaus hilfreich sein.



-------------------------------------------------------------------------------------------------------------


# Entstehung von Thumbs.db-Dateien durch Gruppenrichtlinie verhindern (Active Directory)


### Gruppenrichtlinie über die Domäne erstellen, um Entstehung von Thumbs.db-Dateien zu verhindern
- Auf dem Active-Directory-Windows-Server als Administrator einloggen.
- `Gruppenrichtlinienverwaltung` öffnen
- `Gruppenrichtlinienobjekte` in der `Gruppenrichtlinienverwaltung`
    - `Gruppenrichtlinienobjekte` wählen
    - `Neu`
    - Namen vergeben
    - Rechtsklick auf das neue Gruppenrichtlinienobjekt und auf `bearbeiten` klicken
    - Es öffnet sich der `Gruppenrichtlinienverwaltungs-Editor`
    - `Benutzerkonfiguration`, `Richtlinien`, `Administrative Vorlagen`, `Windows-Komponenten`, `Datei-Explorer`
- Nun nach `Zwischenspeicherung von Miniaturansichten im versteckten Thumbs.db deaktivieren` suchen
- Mit einem `Doppelklick` öffnen
- `Aktiviert`
- `Übernehmen`
- `OK`
- Zurück zur `Gruppenrichtlinienverwaltung`
    - Unter `domain.local` -> `Domäne` -> `Benutzer` auswählen, `Rechtsklick` und `vorhandenes Gruppenrichtlinienobjekt verknüpfen`
    - Zum verknüpfen das gewünschte Objekt auswählen


```
$ gpupdate /force
```
- Clients ggf. neu starten


- Durch das Einstellen dieser Richtlinie werden keine bestehenden Thumbs.db-Dateien entfernt, es wird lediglich die Entstehung neuer Thumbs.db-Dateien verhindert.


-------------------------------------------------------------------------------------------------------------

