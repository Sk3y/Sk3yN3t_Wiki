## XML-Funktionen
Alle Informationen aus der SquadXML können mit dem SQF-Befehl `squadParams`abgerufen werden:
https://community.bistudio.com/wiki/squadParams

### Rangabfrage eines Spielers
```SQF
    ["jgkp_get_rank",[player]] call CBA_fnc_clientToServerEvent;
```
*Beschreibung:* Gibt den Rang des Spielers anhand seiner UID zurück, wie er in der DB steht. Die ausgegebene Information ist IMMER ein String und ist in der Variable "ResultXMLRang" zu finden.

*Übergabewert:* Spieler oder Einheit (unit), deren Rang erfragt werden soll

*Rückgabewert:* ResultXMLInfo (str)

Die Ränge kommen mit folgenden Werten zurück, aber nur als Zahl! Bedeutung:

    1 = Jäger
    2 = Gefreiter
    3 = Obergefreiter
    4 = Hauptgefreiter
    5 = Stabsgefreiter
    6 = Oberstabsgefreiter
    7 = Unteroffizier
    8 = Stabsunteroffizier
    9 = Feldwebel
    10 = Oberfeldwebel
    11 = Hauptfeldwebel
    12 = Stabsfeldwebel
    13 = Oberstabsfeldwebel
    14 = Leutnant
    15 = Oberleutnant
    16 = Hauptmann

### Memberüberprüfung eines Spielers
```SQF
    ["jgkp_is_member",[player]] call CBA_fnc_clientToServerEvent;           
```
*Beschreibung:* Funktion prüft, ob der Spieler bzw. dessen UID in der DB vorhanden ist. 

*Übergabewert:* Spieler oder Einheit (unit), deren Zugehörigkeit geprüft werden soll.

*Rückgabewert:* ResultIsMember (bool): true, falls Spieler in DB, sonst false