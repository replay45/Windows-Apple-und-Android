# lokalen Windows 11 Benutzer erstellen - Kontozwang umgehen


`Anleitung verfasst am 20.6.2024`

`Windows Version: Win11 23H2`



# Windows 11 Pro

- Bei der Ersteinrichtung des PCs in dem Ersteinrichtungsassistenten unter `Wie möchten Sie dieses Gerät einrichten?` auf `Für Arbeit oder Schule/Uni einrichten` klicken, um ein lokales Konto erstellen zu können.

- Nun anstatt mit einem Konto sich anzumelden, auf `Anmeldeoptionen` gehen und `Stattdessen der Domäne beitreten` auswählen (Es ist nicht nötig einer Domäne beizutreten, die Option ein lokales Konto anzulegen ist lediglich hinter diesem Punkt versteckt).

- Jetzt einfach ein Benutzername vergeben und ein Passwort wählen. Danach wie gewohnt die Sicherheitsfragen beantworten und die Datenschutzoptionen setzen.




# Windows 11 Home

- Internetverbindung trennen (Ethernet Kabel trennen / WLAN Verbindung gar nicht erst herstellen).

- Bei Windows 11 Home ist ein anderes Vorgehen als bei Windows 11 Pro nötig, da die Home-Versionen keinen Zugang zu einer Domäne ermöglichen.

- Bei der Ersteinrichtung des PCs in dem Ersteinrichtungsassistenten `SHIFT + F10` drücken (auf Notebooks könnte das drücken der FN-Taste zusätzlich nötig sein), um Terminal zu öffnen.

- Folgendes in das Terminal eingeben:

```
oobe\BypassNRO.cmd
```

- Einrichtungsassistenten folgen und bei dem Punkt `Netzwerk verbinden` auf `Ich habe kein Internet` klicken.

- Danach `Mit eingeschränkter Ersteinrichtung fortfahren` auswählen.

- Jetzt einfach ein Benutzername vergeben und ein Passwort wählen. Danach wie gewohnt die Sicherheitsfragen beantworten und die Datenschutzoptionen setzen.

-----------------------------------------------------------------------------------------------------------------
