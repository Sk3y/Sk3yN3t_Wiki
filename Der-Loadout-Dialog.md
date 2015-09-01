# Der Loadout-Dialog
***
Um die Loadouts der Datenbank tatsächlich verwenden zu können, ist die Funktion [["jgkp_get_loadout" |Funktionen-zur-Loadoutabfrage#spieler-mit-loadout-ausrüsten]] gedacht. Diese erfordert aber Kenntnis über die ID, mit der das Loadout in der Datenbank gespeichert ist.

Außerdem soll die Ausrüstung auch während einer Mission gewechselt/angepasst werden können. Hierzu ist ein System notwendig, dass die Loadouts aus der Datenbank genau dann bereit stellt, wenn man sie abfragen möchte. Diese Aufgabe übernimmt der Loadout-Dialog

## Der Dialog in Übersicht
![Der Dialog mit Erklärungen](http://www11.pic-upload.de/02.09.15/iv286zia6pil.png)

## Der Dialog im Spiel
Das folgende Video demonstriert eine frühe Version des Dialogs. Alle Felder werden aus der DB gespeist, keine Information ist im Dialog selbst als Code hinterlegt!
<<https://youtu.be/S_wDeOHSwlE>>

So sieht der Dialog im Spiel aus:
![Der Dialog im Spiel](http://www11.pic-upload.de/02.09.15/hg82jo7lwhl.png)

Ein Loadout kann schrittweise gewählt werden, indem
1. Der gewünschte Zug ausgewählt wird (Daten kommen aus der DB)
2. Die gewünschte Gruppe ausgewählt wird (Daten kommen aus der DB und richten sich nach 1.)
3. Der gewünschte Typ ausgewählt wird (Daten kommen aus der DB und richten sich nach 1. und 2.)
4. Auf den Lade mögl. Loadouts-Button geklickt wird (wird erst aktiv nach 1., 2. und 3.)
5. Ein Loadout aus der zentralen Liste ausgewählt wird (geht erst nach 4.)
6. Das gewählte Loadout mit Klick auf den Lade Loadout-Button ausgerüstet wird (geht erst nach 5.)