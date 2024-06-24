# Windows Firewall & [XAMPP](https://www.apachefriends.org/de/index.html) Webserver


## Inhaltsverzeichnis

### 1. Windows Firewall
   - 1.1. Windows 11 Firewall - Ports öffnen/schließen
   - 1.2. Port(s) öffnen, am Beispiel von Port 80
   - 1.3. Porttest durchführen am Beispiel von Port 80


### 2. Apache-Web-Testserver mit [XAMPP](https://www.apachefriends.org/de/index.html)
   - 2.1. [XAMPP](https://www.apachefriends.org/de/index.html) installieren
   - 2.2. möglicher Fehler - `php intl error`


---------------------------------------------------------------------------------------------------


# 1.1. Windows 11 Firewall - Ports öffnen/schließen

- `Windows Defender Firewall mit erweiterter Sicherheit` öffnen.

- Wenn eine Regel ausgewählt wird, können diverse Anpassungen in der rechten Leiste unter `Aktionen` vorgenommen werden.

- Es können u.a. bestehende Regeln aktiviert/deaktiviert, bearbeitet oder gelöscht werden.

- Außerdem können in der Firewall auch ein/ausgehende Verbindungen, z.B. von bestimmten Apps blockiert, bzw. verboten werden.

- Natürlich empfiehlt es sich die Firewall immer aktiv zu haben und nur die benötigten Ports zu öffnen !!!


---------------------------------------------------------------------------------------------------


# 1.2. Port(s) öffnen, am Beispiel von Port 80


`Port 80` ist nur ein `Beispiel`, die der `Port 80` kann natürlich auch durch `andere Ports ersetzt` werden.


### eingehende Regeln
  - `eingehende Regeln`
  - unter "Aktionen" auf `neue Regel` gehen,

- Folgendes wählen:
	`Port`
	`TCP 80`
	`UDP 80`

- Auf `Verbindung zulassen` klicken !
- Gewünschte Einstellungen vornehmen und Namen vergeben.
- `Fertig stellen`


### ausgehende Regeln
  - `ausgehende Regeln`
  - unter "Aktionen" auf `neue Regel` gehen,

- Folgendes wählen:
	`Port`
	`TCP 80`
	`UDP 80`

- Auf `Verbindung zulassen` klicken !
- Gewünschte Einstellungen vornehmen und Namen vergeben.
- `Fertig stellen`


---------------------------------------------------------------------------------------------------


# 1.3. Porttest durchführen am Beispiel von Port 80


Um zu testen, ob der Standardport 80 frei ist, kann in [PowerShell](https://de.wikipedia.org/wiki/PowerShell) der folgende Befehl eingefügt werden:

```
$ Test-NetConnection localhost -Port 80
```


Wenn der `TcpTestErfolgreich` : `True` ausgibt, ist der Standardport (80) bereits belegt.

Wenn der `TcpTestErfolgreich : `false` ausgibt, ist der Standardport (80) nicht belegt.

Wenn die Ausgabe "failed" erscheint, wurden die Änderungen möglicherweise nicht übernommen und der Port könnte geschlossen sein.


---------------------------------------------------------------------------------------------------


# 2. Apache-Web-Testserver mit [XAMPP](https://www.apachefriends.org/de/index.html)


`Diese Anleitung wurde auf Windows 10 getestet.`


### Vorab:
Der Webserver, der über XAMPP läuft, ist ausschließlich dafür gedacht, `lokal` auf dem PC zu laufen und
ist daher **nicht** von anderen Geräten im Netzwerk erreichbar !
XAMPP dient primär für `Testzwecke` und läuft daher standardmäßig nur lokal !

Daher ist es auch **nicht** nötig, Portfreigaben vorzunehmen.


---------------------------------------------------------------------------------------------------


# 2.1. [XAMPP](https://www.apachefriends.org/de/index.html) installieren


- Die All-in-one Lösung [XAMPP](https://www.apachefriends.org/de/index.html), die den Webserver, php und MySQL unterstützt, installieren.

- Falls der Webserver nicht in unmittelbarer Nähe ist, kann z.B. das Programm [FileZilla](https://filezilla-project.org/) genutzt werden, um Dateien zu verschieben.

- Nun die Dateien für die Webseite (inkl. der `index.html` Datei) auf den Server in den entsprechenden Pfad kopieren:

`C:/individuell/wo/der/ordner/ist/xampp/htdocs`

- In XAMPP den Apache Webserver und ggf. die benötigten Komponenten starten !

- Jetzt kann im Browser [localhost](http://localhost/) aufgerufen werden, um die Webseite zu öffnen.


---------------------------------------------------------------------------------------------------


# 2.2. möglicher Fehler - `php intl error`

Sollte ein `internal error` `PHP extension is required` `required components Please install: intl` auftauchen,
muss in der XAMPP Control App auf den Button `Konfig` unter dem Reiter `Apache` gedrückt werden.

Danach muss `PHP (php.ini)` ausgewählt werden.
Nun öffnet sich eine Textdatei, mit `STRG+F` kann die `Suche geöffnet` werden.
Es gibt mehrere Suchmöglichkeiten, die eingegeben werden können:

1. `extension`
2. `intl`
3. `extension=intl`


- Sobald `extension=intl` gefunden wurde, muss das Simikolon `;` vorne `entfernt` werden.

- Vor dem Speichern, sollte die Datei kopiert werden, um bei möglichen Fehlern die bearbeitete Datei ersetzen zu können.

- Jetzt sollte die Fehlermeldung nicht mehr erscheinen.


---------------------------------------------------------------------------------------------------
