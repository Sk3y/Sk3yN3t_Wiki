# Datenbank-Layout
Hier erfahr ihr alles, was ihr wissen müsst, um ein Loadout für die Datenbank [[einzureichen|Loadouts-in-die-DB-einfügen]].

## Loadout für Spieler
Die Datenbank verfügt über die folgenden Spalten:
![Tabelle Loadouts in der Datenbank](http://i.imgur.com/MfDkJDM.png)

* `id` ist nur für interne Zwecke
* `zug, gruppe, typ` sind die wichtigsten Textfelder. Der Typ von `zug` ist ENUM, d.h. es ist ein Aufzählungstyp und nur die voreingestellten Werte ("I","II","III") sind zulässig. `gruppe` und `typ` können im Prinzip frei gewählt werden. Braucht ihr weitere Werte, dann bitte mitteilen! Ansonsten versucht euch in das System einzufügen, um unnötige Namen zu vermeiden. Denkt daran, dass diese drei Werte auch im [[Dialog|Der-Loadout-Dialog#der-dialog-im-spiel]] abgefragt werden!
* `name` legt den Anzeigenamen im Dialog fest. Bitte ebenfalls an die gängige Notation halten!
* `headgear...selectweapon` sind alles Textfelder, die eure Ausrüstung enthalten. Das Format ist bei einwertigen Feldern NUR der Itemname, bei mehrwertigen Feldern immer Itemname~Anzahl! Bitte auch bei nur einem einzigen Item Itemname~1 angeben
* `isMedic` kann 0, 1 oder 2 annehmen. Dieses Feld sorgt dafür, dass die Einheit in ACE als Sanitäter oder Arzt erkannt wird. Bei 0 kann sie das San-System quasi nicht verwenden.
* `isEOD, isMember` sind zwei bool'sche Felder, die nur 0 oder 1 sein können, wobei 0 - false und 1 - true entspricht. Die Felder legen fest, ob jemand beim Ausrüsten auch als Medic oder EOD von ACE erkannt wird. isMember legt fest, ob ein Public-Spieler das Loadout laden darf, wenn er nicht in der DB als Mitglied gelistet ist.
* `isPublic` ist ein bool'sches Feld, das festlegt, ob das Loadout in der [[eingeschränkten Version|https://github.com/Jamesadamar/3JGKP_Datenbankfunktionen/wiki/Der-Loadout-Dialog#einschr%C3%A4nkung-der-loadouts-f%C3%BCr-missionsbauer]] zur Verfügung steht.

## Loadout für Kisten und Fahrzeuge
Diese Datenbank wird noch überarbeitet...