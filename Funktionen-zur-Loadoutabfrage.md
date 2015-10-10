## Loadout-Funktionen
Alle folgenden Funktionen dienen dazu, Loadouts aus der DB zur Verfügung zu stellen.

### Kisten und Fahrzeuge einmalig mit Loadout befüllen

```SQF
    ["jgkp_fill_crate",[crate,"loadout"]] call CBA_fnc_clientToServerEvent;
```
*Beschreibung:* Mit dieser Zeile könnt ihr per addAction oder Script eine benannte Kiste oder ein Fahrzeug automatisch einmalig mit einem Loadout füllen, das in der DB vorhanden ist (Name "loadout" ist durch den Namen in der DB zu ersetzen)

*Übergabewert:* Kiste oder Fahrzeug (Object) sowie den Namen des Loadouts (str), der in der DB vorhanden sein muss.

*Rückghabewert:* Hier gibt es keinen Rückgabewert. Die Kiste bzw. das Fahrzeug wird sofort beladen.

Eigenes Kisten-Loadout? Benötigt wird ein Loadoutname, Items, Rucksäcke, Waffen und Magazine.

**Wichtig:** Immer auf das Format achten! "Item"~Anzahl;"Item"~Anzahl! Nicht ~ und ; verwechseln!

Beispiel:

(Items) BWA3_optic_20x50_NSV~1;BWA3_Vector~5;ItemMap~5;AGM_MapTools~5;tf_anprc148jem~5; // 1x NSV + 5x Vector + 5 Karten + 5 Maptools und 5 kleine Funken

(Rucksäcke) tf_anprc155~5

(Waffen) BWA3_Pzf3~4;BWA3_Fliegerfaust~2

(Magazine) Laserbatteries~5;BWA3_DM25~15;SmokeShellGreen~15;BWA3_30Rnd_556x45_G36_SD~12

### Spieler mit Loadout ausrüsten
```SQF
    ["jgkp_equip_loadout",[unit,id]] call CBA_fnc_clientToServerEvent;
```
*Beschreibung:* Rüstet die übergebene Einheit `unit` mit dem Inhalt des Loadouts für die gegebene ID (PK in DB) aus. 

*Übergabewert:*
* unit (object): Einheit, die ausgerüstet werden soll, für den Spieler `player` nutzen oder seinen Variablennamen oder `this` innerhalb der Init-Zeile. 
* ID (int): ID (Primary Key) des Loadouteintrags in der DB. Muss in der DB existieren (s.u.).

*Rückgabewert:* Hier gibt es keinen Rückgabewert. Der Spieler wird automatisch sofort mit dem gewählten Loadout ausgestattet.

**Wichtig**: Die Funktion kann entwederinnerhalb des neu erstellten [[Dialogsystems|Der-Loadout-Dialog]] verwendet werden (Button Lade Loadout), oder auch direkt z.B. in der Init-Zeile einer EInheit, sofern man die ID kennt! Diese kann man aber über besagten Dialog in Erfahrung bringen, denn die ID des Loadouts steht hinter dem Namen des Loadouts in runden Klammern!


