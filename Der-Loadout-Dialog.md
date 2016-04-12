# Der Loadout-Dialog
***
Um die Loadouts der Datenbank tatsächlich verwenden zu können, ist die Funktion [["jgkp_equip_loadout" |Funktionen-zur-Loadoutabfrage#spieler-mit-loadout-ausrüsten]] gedacht. Diese erfordert aber Kenntnis über die ID, mit der das Loadout in der Datenbank gespeichert ist.

Außerdem soll die Ausrüstung auch während einer Mission gewechselt/angepasst werden können. Hierzu ist ein System notwendig, dass die Loadouts aus der Datenbank genau dann bereit stellt, wenn man sie abfragen möchte. Diese Aufgabe übernimmt der Loadout-Dialog

## Aufruf
Der neue Dialog besteht aus insgesamt vier Einzeldialogen. 
Der Einstiegsdialog kann über den folgenden Befehl
```SQF
createDialog "DBLoadoutEntry";
```
an beliebiger Stelle erzeugt werden. Dialoge werden im Allgemeinen über die ESC-Taste wieder geschlossen.

So kann man den Aufruf z.B. an einen Add-Action-Menüeintrag binden:
```SQF
object addAction ["Waffenkammer öffnen", {createDialog "DBLoadoutEntry";}];
```

## Einschränkung der Loadouts für Missionsbauer

Der Dialog existiert in zwei Varianten: Mit allen Loadouts, die in der DB gespeichert sind (public + nicht public) sowie einer eingeschränkten Variante für die Public-Server. Mithilfe der folgenden Code-Zeile in der initServer.sqf könnt ihr dem Server eure Wunscheinstellung mitteilen:
```SQF
JGKP_DB_onlyPublic = 0|1
["jgkp_refresh_request"] call CBA_fnc_clientToServerEvent;
```
* 0: ist die default-Einstellung und lässt alle Loadouts zu.
* 1: ist die eingeschränkte Einstellung und lässt nur Loadouts zu, die isPublic = 1 besitzen.

**wichtig**: Der zweite Befehl ist wichtig, damit die Änderungen auf dem Server übernommen werden. Denn das Addon startet selbst mit dem Wert 0, d.h. allen Loadouts. Nur die Variable zu ändern, hätte erst eine Auswirkung nach dem Drücken des refresh-Buttons! Mit dem zweiten Befehl kann der Missionsbauer sicherstellen, dass die Änderung gleich übernommen wird.

## Der Dialog in Übersicht
Das folgende Diagramm zeigt den Ablauf, der zur Anzeige der drei Unterdialoge führt. Dabei ist die Entscheidung nicht als exklusives Oder zu verstehen. Jemand mit den höchsten Rechten kann natürlich immer noch Loadouts laden und speichern, er kann nur zusätzlich Loadouts editieren und sogar per Dialog löschen.
![Der Dialog mit Erklärungen]( http://www2.pic-upload.de/img/30245298/Loadout-System.png)
(in groß: http://www2.pic-upload.de/img/30245298/Loadout-System.png)

## Der Dialog im Spiel
Das folgende Video demonstriert eine aktuelle Version (0.03) des Dialogs. Alle Felder werden aus der DB gespeist, keine Information ist im Dialog selbst als Code hinterlegt!
<https://youtu.be/Cn301ZJoex0>

So sieht der Dialog im Spiel aus:
### Loadout Entry
![Der Dialog Entry im Spiel](http://www11.pic-upload.de/26.09.15/onkpentfw.png)

### Loadout Load
![Der Dialog Load im Spiel](http://www11.pic-upload.de/26.09.15/n2jcliifvjt.png)

Ein Loadout kann schrittweise gewählt werden, indem
 1. Der gewünschte Zug ausgewählt wird (Daten kommen aus der DB)
 2. Die gewünschte Gruppe ausgewählt wird (Daten kommen aus der DB und richten sich nach 1.)
 3. Der gewünschte Typ ausgewählt wird (Daten kommen aus der DB und richten sich nach 1. und 2.)
 4. Auf den "Lade mögl. Loadouts"-Button geklickt wird (wird erst aktiv nach 1., 2. und 3.)
 5. Ein Loadout aus der zentralen Liste ausgewählt wird (geht erst nach 4.)
 6. Das gewählte Loadout mit Klick auf den "Lade Loadout"-Button ausgerüstet wird (geht erst nach 5.)


Die Nummer hinter dem Loadoutnamen in runden Klammern ist die gesuchte ID für die Funktion [["jgkp_equip_loadout" |Funktionen-zur-Loadoutabfrage#spieler-mit-loadout-ausrüsten]]. Damit ist es also auch möglich, eine Einheit oder einen Spieler direkt z.B. durch einen Init-Eintrag oder ein addAction-Eintrag auszurüsten, indem man die gewünschte ID an das Skript übergibt. 

### Truppenkörperabzeichen

Die Informationen zu den Truppenkörperabzeichen kommt ebenfalls aus der DB, hierfür gibt es eine ganz einfache kleine zweispaltige Tabelle mit den Spalten name (für die Anzeige im Dialog) und classname (für die Funktion `BIS_fnc_setUnitInsignia`). D.h. auch diese Information muss nicht im Dialog selbst verwaltet werden, sondern kann bequem in der DB angepasst werden. Aber Achtung: Die Insignia kommen aus einem Addon und sind nicht Teil des Standardspiels, daher muss der Inhalt des Addons angepasst werden, wenn man sich andere Patches wünscht.

### Loadout Save
![Der Dialog Save im Spiel](http://i.imgur.com/VfMaNfl.png)

Ein Loadout kann gespeichert werden, indem
 1. Der entsprechende Zug aus dem Menü ausgewählt wird (Daten ausnahmsweise fest im DB verankert...)
 2. Ein Name für die Gruppe eingegeben wird
 3. Ein Name für den Typ eingegeben wird
 4. Ein Name für das Loadout eingegeben wird
 5. Die Sanfähigkeit ausgewählt wird (Wahl zwischen 0, 1 oder 2)
 6. Die Pionier-Fähigkeit ausgewählt wird (an/aus)
 7. Die Member-Only-Option ausgewählt wird (an/aus)
 8. Die Zugriffs-Option ausgewählt wird (public oder nur für Member)
 9. Der Button "Loadout speichern" geklickt wird.

Hierbei heißt *public* nicht, dass das Loadout frei verfügbar ist, das ist es auch ohne eine Auswahl. public bedeutet, dass dieses Loadout immer dann erscheint, wenn der Missionsbauer den Dialog einschränkt mithilfe der Variable ``JGKP_DB_onlyPublic = 1``. Dann werden nur die Loadouts angeboten, die bei der Spalte isPublic eine 1 haben und das bewirkt man genau mit der Auswahl public. *member* hingegen bedeutet, dass das Loadout nur verwendet werden kann, wenn man Mitglied der 3. Jägerkompanie ist. Logischerweise schließen sich beide Optionen aus.

### Loadout Edit
![Der Dialog Edit im Spiel](http://i.imgur.com/4rNdoVk.png)

Ein Loadout kann editiert werden, indem
 1. Die entsprechende ID des Loadouts aus der DB eingegeben wird (zB über das Load-Menü)
 2. Der Button "Lade Loadout gemäß ID" geklickt wird (es kann zu zwei versch. Fehlern kommen!)
 3. Einer der 22 Buttons unter der Inhalt-Box geklickt wird (man kann jeweils nur eine Spalte gleichzeitig ändern, aber versch. Änderungen speichern)
 4. Die gewünschte Änderung in der zentralen Inhalts-Box vorgenommen wird
 5. Die Änderung mit einem Klick auf den jetzt weiß gewordenen Button "Änderungen speichern" temporär gesichert wird!
 6. Schritte 3-5 beliebig oft wiederholen
 7. Abschließend der Button "Änderungen übernehmen" geklickt wird.

**wichtig**: Die Änderungen werden durch den Button "speichern" nur temporär übernommen. Man kann sich davon überzeugen, indem man zB. bei "Zug" eine Änderung vornimmt, diese speichert und anschließend wieder "Zug" drückt. Die Änderung ist dann im Inhalts-Fenster sichtbar. ABER die Änderung ist noch nicht in der DB und geht beim Schließen auch verloren. Daher muss nach Abschluss der Arbeit noch auf "Änderungen übernehmen" geklickt werden, was alle gemachten Änderungen in die DB überträgt.

**WARNUNG:** Der Edit-Dialog kann nur von Mitgliedern mit entsprechenden Rechten im Kommandostand aufgerufen werden. Danach ist keine weitere Abfrage vorgesehen. Wer das Recht zum Editieren hat (2 im KdtStand), kann ohne Einschränkung alle Loadouts bearbeiten und frei verändern. Wer das Recht zum Löschen hat (3 im KdtStand), kann ohne Einschränkung alle Loadouts löschen. Über jede Aktion wird aber in der log-Tabelle Protokoll geführt, rückgängig gibt es aber nicht!
