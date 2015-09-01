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

**Wichtig:** Immer auf das Format achten! "Item":Anzahl;"Item":Anzahl! Nicht : und ; verwechseln!

Beispiel:

(Items) BWA3_optic_20x50_NSV:1;BWA3_Vector:5;ItemMap:5;AGM_MapTools:5;tf_anprc148jem:5 // 1x NSV + 5x Vector + 5 Karten + 5 Maptools und 5 kleine Funken

(Rucksäcke) tf_anprc155:5

(Waffen) BWA3_Pzf3:4;BWA3_Fliegerfaust:2

(Magazine) Laserbatteries:5;BWA3_DM25:15;SmokeShellGreen:15;BWA3_30Rnd_556x45_G36_SD:12

### Spieler mit Loadout ausrüsten
```SQF
    ["jgkp_get_loadout",[player,id]] call CBA_fnc_clientToServerEvent;
```
*Beschreibung:* Liefert den Inhalt des Loadouts für die gegebene ID (PK in DB). 

*Übergabewert:* ID (int)! ID (Primary Key) des Loadouteintrags in der DB. Muss in der DB existieren (s.u.).

*Rückgabewert:* Hier gibt es keinen Rückgabewert. Der Spieler wird automatisch sofort mit dem gewählten Loadout ausgestattet.

**Wichtig**: Die Funktion kann einmal innerhalb des neu erstellten Dialogsystems verwendet werden (Button Lade Loadout), oder auch direkt z.B. in der Init-Zeile einer EInheit, sofern man die ID kennt! Diese kann man aber über besagten Dialog in Erfahrung bringen, denn die ID des Loadouts steht hinter dem Namen des Loadouts in runden Klammern!

Eintrag in der DB: Bitte alle Felder, die nur ein Item enthalten (headgear, uniform, vest, selectWeapon, ...) nur mit dem Klassennamen füllen, also "BWA3_G36" z.B.

Für alle Listenfelder (uniformitems, vestitems, backpackitems, weapons, ...) ist die Schreibweise IMMER "Klassname":Anzahl. Also auch bei nur 1 Item immer :1 angeben!

Eigene Loadouts:

    zug: enum('I', 'II', 'III')
    gruppe: enum('1.', '2.', '3.', 'HFlg', 'SanTrp', 'Nachschub', 'ZugTrp')
    typ: enum('Flecktarn', 'Tropentarn', 'Besatzung', 'Taucher', 'Nacht')
    name: varchar(255)
    headgear: text
    goggles: text
    vest: text
    vestitems: text
    uniform: text
    uniformitems: text
    backpack: text
    backpackitems: text
    weapons: text
    primaryweaponitems: text
    secondaryweaponitems: text
    handgunitems: text
    assignitems: text
    selectWeapon: text
    isMedict: inyint(1)
    isEOD: tinyint(1)
    memberOnly: tinyint(1)

