# Der Logistik-Dialog
***
Um die Kisten und Fahrzeug Loadouts der Datenbank tatsächlich verwenden zu können, ist die Funktion [["jgkp_fill_crate" | Funktionen-zur-Logistik-Abfrage#kisten-und-fahrzeuge-einmalig-mit-loadout-befüllen]] gedacht. Diese erfordert aber Kenntnis über die ID, mit der das Loadout in der Datenbank gespeichert ist.

Außerdem soll die Ausrüstung auch während einer Mission gewechselt/angepasst werden können. Hierzu ist ein System notwendig, dass die Loadouts aus der Datenbank genau dann bereit stellt, wenn man sie abfragen möchte. Diese Aufgabe übernimmt der Logistik-Dialog

## Aufruf
Der neue Dialog besteht aus insgesamt vier Einzeldialogen. 
Der Einstiegsdialog kann über den folgenden Befehl
```SQF
createDialog "DBCrateEntry";
```
an beliebiger Stelle erzeugt werden. Dialoge werden im Allgemeinen über die ESC-Taste wieder geschlossen.

So kann man den Aufruf z.B. an einen Add-Action-Menüeintrag binden:
```SQF
object addAction ["Logistik-Portal öffnen", {createDialog "DBCrateEntry";}];
```

## Der Dialog im Spiel
Das folgende Video demonstriert eine aktuelle Version (0.03) des Dialogs. Alle Felder werden aus der DB gespeist, keine Information ist im Dialog selbst als Code hinterlegt!
<https://youtu.be/Cn301ZJoex0>

So sieht der Dialog im Spiel aus:
### Loadout Entry
![Der Dialog Entry im Spiel](http://i.imgur.com/u0O6Hyz.png)

### Loadout Load
![Der Dialog Load im Spiel](http://i.imgur.com/yM0HGtF.png)

Ein Kisten-/Fahrzeug-Loadout kann schrittweise angezeigt werden, indem
 1. Der gewünschte Typ ausgewählt wird (Daten kommen aus der DB)
 2. Die gewünschte Variante ausgewählt wird (Daten kommen aus der DB und richten sich nach 1.)
 3. Auf den "Lade mögl. Loadouts"-Button geklickt wird (wird erst aktiv nach 1. und 2.)

Sodann erscheinen in der zentralen Liste alle Loadouts, die in Typ und Variante mit der Auswahl übereinstimmen.

Die Nummer hinter dem Loadoutnamen in runden Klammern ist die gesuchte ID für die Funktion [["jgkp_fill_crate" |Funktionen-zur-Loadoutabfrage#spieler-mit-loadout-ausrüsten]]. Damit ist es also auch möglich, eine Kiste oder ein Fahrzeug direkt z.B. durch einen Init-Eintrag oder ein addAction-Eintrag auszurüsten, indem man die gewünschte ID an das Skript übergibt. 

### Loadout Save
![Der Dialog Save im Spiel](http://i.imgur.com/fxwh42s.png)

Ein Loadout kann gespeichert werden, indem
 1. Der entsprechende Typ aus dem Menü ausgewählt wird (Daten ausnahmsweise fest im DB verankert...)
 2. Eine Variante für die Kiste eingegeben wird
 3. Ein Name für das Loadout eingegeben wird
 4. Der Button "Loadout speichern" geklickt wird.

### Loadout Edit
![Der Dialog Edit im Spiel](http://i.imgur.com/udNpbfG.png)

Ein Loadout kann editiert werden, indem
 1. Die entsprechende ID des Loadouts aus der DB eingegeben wird (zB über das Load-Menü)
 2. Der Button "Lade Loadout gemäß ID" geklickt wird (es kann zu zwei versch. Fehlern kommen!)
 3. Einer der 7 Buttons unter der Inhalt-Box geklickt wird (man kann jeweils nur eine Spalte gleichzeitig ändern, aber versch. Änderungen speichern)
 4. Die gewünschte Änderung in der zentralen Inhalts-Box vorgenommen wird
 5. Die Änderung mit einem Klick auf den jetzt weiß gewordenen Button "Änderungen speichern" temporär gesichert wird!
 6. Schritte 3-5 beliebig oft wiederholen
 7. Abschließend der Button "Änderungen übernehmen" geklickt wird.

**wichtig**: Die Änderungen werden durch den Button "speichern" nur temporär übernommen. Man kann sich davon überzeugen, indem man zB. bei "Typ" eine Änderung vornimmt, diese speichert und anschließend wieder "Typ" drückt. Die Änderung ist dann im Inhalts-Fenster sichtbar. ABER die Änderung ist noch nicht in der DB und geht beim Schließen auch verloren. Daher muss nach Abschluss der Arbeit noch auf "Änderungen übernehmen" geklickt werden, was alle gemachten Änderungen in die DB überträgt.

**WARNUNG:** Der Edit-Dialog kann nur von Mitgliedern mit entsprechenden Rechten im Kommandostand aufgerufen werden. Danach ist keine weitere Abfrage vorgesehen. Wer das Recht zum Editieren hat (2 im KdtStand), kann ohne Einschränkung alle Loadouts bearbeiten und frei verändern. Wer das Recht zum Löschen hat (3 im KdtStand), kann ohne Einschränkung alle Loadouts löschen. Über jede Aktion wird aber in der log-Tabelle Protokoll geführt, rückgängig gibt es aber nicht!
