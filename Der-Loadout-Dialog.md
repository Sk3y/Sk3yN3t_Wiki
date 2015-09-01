# Der Loadout-Dialog
***
Um die Loadouts der Datenbank tatsächlich verwenden zu können, ist die Funktion [["jgkp_get_loadout" |Funktionen-zur-Loadoutabfrage#spieler-mit-loadout-ausrüsten]] gedacht. Diese erfordert aber Kenntnis über die ID, mit der das Loadout in der Datenbank gespeichert ist.

Außerdem soll die Ausrüstung auch während einer Mission gewechselt/angepasst werden können. Hierzu ist ein System notwendig, dass die Loadouts aus der Datenbank genau dann bereit stellt, wenn man sie abfragen möchte. Diese Aufgabe übernimmt der Loadout-Dialog

## Der Dialog in Übersicht
![Der Dialog mit Erklärungen](http://www11.pic-upload.de/02.09.15/3idm9cd78sba.png)

## Der Dialog im Spiel
Das folgende Video demonstriert eine frühe Version des Dialogs. Alle Felder werden aus der DB gespeist, keine Information ist im Dialog selbst als Code hinterlegt!
<<https://youtu.be/S_wDeOHSwlE>>
