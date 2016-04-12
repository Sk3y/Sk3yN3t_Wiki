## Logistik-Funktionen
Alle folgenden Funktionen dienen dazu, Kisten- oder Fahrzeug-Loadouts aus der DB zur Verfügung zu stellen.

### Kisten und Fahrzeuge einmalig mit Loadout befüllen

```SQF
    ["jgkp_fill_crate", [crate, id]] call CBA_fnc_clientToServerEvent;
```
**Beschreibung:** Mit dieser Zeile könnt ihr per addAction oder Script eine benannte Kiste oder ein Fahrzeug automatisch einmalig mit einem Loadout füllen, das in der DB vorhanden ist (Name "loadout" ist durch den Namen in der DB zu ersetzen)

**Übergabewert:** Kiste oder Fahrzeug (Object) sowie den ID des Loadouts (int), der in der DB vorhanden sein muss.

**Rückghabewert:** Hier gibt es keinen Rückgabewert. Die Kiste bzw. das Fahrzeug wird sofort beladen.

#### Kisten/Fahrzeuge zu Missionsbeginn ausrüsten

In diesem Falle können wir den obigen Befehl nicht 1:1 verwenden und z.B. in die init-Zeile einer Einheit schreiben, da dies nicht JIP-sicher ist. Denn bei jedem neuen Spieler werden Skripte in der Init-Zeile erneut ausgeführt.

Die Lösung nutzt daher einen Auslöser, der sich um die initiale Beladung kümmert:

1. Erstelle einen Auslöser beliebiger Größe, Einstellungen egal und bei der Bedingung: ```isServer && time > 5```

2. Füge dem Auslöser für jede Kiste und jedes Fahrzeug einen Befehl hinzu, der die Kiste bzw. das Fahrzeug mit dem gewünschten Loadout belädt, z.B. : ```["jgkp_fill_crate", [kiste1, 1]] call CBA_fnc_clientToServerEvent;```

Der Auslöser sieht dann im Grunde wie folgt aus:
![Auslöser](http://i.imgur.com/prMIO0J.png)

Damit führt der Server einmalig nach 5 Sekunden die Befehle in der Aktivierungszeile aus und alle Kisten sind beladen. Alterantiv können die Befehle natürlich auch in die `initServer.sqf` geschrieben werden, hier gibt es mehrere Möglichkeiten. Ihr müsst nur sicherstellen, dass die Befehle einmalig ausgeführt werden und JIP-sicher sind.

#### Loadouts per Add-Action-Menü

Möchtet ihr ein Loadout z.B. fest mit einem Aktionmenüeintrag verbinden, ist dies wie folgt möglich:

```SQF
this addAction ["<t color='#00ff00' size='1.2'>Loadout GrpFhr</t>", {
["jgkp_fill_crate", [crate, id]] call CBA_fnc_clientToServerEvent;
}];
```
Dieser Befehl kommt in die Init-Zeile eines beliebigen Objektes, dass den Aktioneintrag besitzen soll. Wird er ausgeführt, so wird die Kiste mit dem Namen `crate` mit dem Loadout mit der angegebenen `id` befüllt.



