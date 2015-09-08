# Datenbank-Layout
Hier erfahr ihr alles, was ihr wissen müsst, um ein Loadout für die Datenbank [[einzureichen|Loadouts-in-die-DB-einfügen]].

## Loadout für Spieler
Die Datenbank verfügt über die folgenden Spalten:
![Tabelle Loadouts in der Datenbank](http://www11.pic-upload.de/02.09.15/6dw94rxag934.png)

* `id` ist nur für interne Zwecke
* `zug, gruppe, typ` sind die wichtigsten Textfelder. Der Typ ist ENUM, d.h. es sind Aufzählungstypen und nur die voreingestellten Werte sind zulässig. Braucht ihr weitere Werte (z.B. für Typ), dann bitte mitteilen! Ansonsten versucht euch in das System einzufügen, um unnötige Namen zu vermeiden. Denkt dran, dass diese drei Werte auch im [[Dialog|Der-Loadout-Dialog#der-dialog-im-spiel]] abgefragt werden!
* `name` legt den Anzeigenamen im Dialog fest. Bitte ebenfalls an die gängige Notation halten!
* `headgear...selectweapon` sind alles Textfelder, die eure Ausrüstung enthalten. Das Format ist bei einwertigen Feldern NUR der Itemname, bei mehrwertigen Feldern immer Itemname:Anzahl! Bitte auch bei nur einem einzigen Item Itemname:1 angeben
* `isMedic, isEOD, isMember` sind drei bool'sche Felder, die nur 0 oder 1 sein können, wobei 0 - false und 1 - true entspricht. Die Felder legen fest, ob jemand beim Ausrüsten auch als Medic oder EOD von ACE erkannt wird. isMember legt fest, ob ein Public-Spieler das Loadout laden darf, wenn er nicht in der DB als Mitglied gelistet ist.

## Loadout für Kisten und Fahrzeuge
Diese Datenbank wird noch überarbeitet...