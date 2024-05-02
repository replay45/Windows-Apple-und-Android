# MacOS

# SIP (System Integrity Protection) ein-/ ausschalten

### Intel-Mac:


1. In den Wiederherstellungsmodus gelangen

- a) über einen Neustart:
	- den Mac ausschalten
	- Ein/Aus-Taste drücken und Befehl-R gedrückt halten
	- warten, bis das Apple-Logo erscheint und dann Befehl-R los lassen
	- Nun sollte das Fenster macOS-Dienstprogrammen zu sehen sein.


- b) über das Terminal:

	```
	$ sudo nvram "recovery-boot-mode=unused
	```
	```
	$ sudo reboot recovery
	```




2. SIP deaktivieren:

	- über die obere Leiste auf "Dienstprogramme" klicken und das Terminal öffnen
	- nun den folgenden Befehl im Terminal einfügen:

	```
	$ csrutil disable
	```

	- Mac neu starten




3. Status prüfen

	Terminal auf dem Desktop öffnen und Befehl eingeben:

	```
	$ csrutil status
	```



4. SIP wieder aktivieren:

	- erneut in den Wiederherstellungsmodus und das Terminal öffnen
	- dann folgenden Befehl im Terminal einfügen:

	```
	$ csrutil enable
	```

	- Mac neu starten


---------------------------------------------------------------------------------------------
