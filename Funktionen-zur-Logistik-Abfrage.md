## Logistik-Funktionen
Alle folgenden Funktionen dienen dazu, Kisten- oder Fahrzeug-Loadouts aus der DB zur Verfügung zu stellen.

### Kisten und Fahrzeuge einmalig mit Loadout befüllen

```SQF
    ["jgkp_fill_crate",[crate,id]] call CBA_fnc_clientToServerEvent;
```
**Beschreibung:** Mit dieser Zeile könnt ihr per addAction oder Script eine benannte Kiste oder ein Fahrzeug automatisch einmalig mit einem Loadout füllen, das in der DB vorhanden ist (Name "loadout" ist durch den Namen in der DB zu ersetzen)

**Übergabewert:** Kiste oder Fahrzeug (Object) sowie den ID des Loadouts (int), der in der DB vorhanden sein muss.

**Rückghabewert:** Hier gibt es keinen Rückgabewert. Die Kiste bzw. das Fahrzeug wird sofort beladen.

#### Kisten/Fahrzeuge zu Missionsbeginn ausrüsten

In diesem Falle können wir den obigen Befehl nicht 1:1 verwenden und z.B. in die init-Zeile einer Einheit schreiben, da dies nicht JIP-sicher ist. Denn bei jedem neuen Spieler werden Skripte in der Init-Zeile erneut ausgeführt.

Die Lösung nutzt daher einen Auslöser, der sich um die initiale Beladung kümmert:

1. Erstelle einen Auslöser beliebiger Größe, Einstellungen egal und bei der Bedingung: ```isServer && time > 5```

2. Füge dem Auslöser für jede Kiste und jedes Fahrzeug einen Befehl hinzu, der die Kiste bzw. das Fahrzeug mit dem gewünschten Loadout belädt, z.B. : ```["jgkp_fill_crate",[kiste1,1]] call CBA_fnc_clientToServerEvent;```

Der Auslöser sieht dann im Grunde wie folgt aus:
![Auslöser](http://i.imgur.com/prMIO0J.png)

#### Loadouts per Add-Action-Menü

Möchtet ihr ein Loadout z.B. fest mit einem Aktionmenüeintrag verbinden, ist dies wie folgt möglich:

```SQF
this addAction ["<t color='#00ff00' size='1.2'>Loadout GrpFhr</t>", {
["jgkp_equip_loadout",[player,164]] call CBA_fnc_clientToServerEvent;
}];
```

Dieser Befehl kommt in die jeweilige init-Zeile eurer Kiste/eures Fahrzeuges etc. Das erste Argument enthält den Text des Befehls, der dem Spieler angezeigt wird, hier könnt ihr euch beliebig austoben. Das Beispiel nutzt eine Schrift, die um 20 % vergrößert wurde (`size='1.2'`) und grün ist (`color='#00ff00'`). Das zweite Argument ist ein Code-Block, der aufgerufen wird, sobald der Spieler den Befehl auswählt. Dieser Befehl ist mit dem Befehl im obigen Abschnitt fast identisch, **aber** wir fragen natürlich nicht die Loadout-ID des Spielers ab, sondern geben eine Loadout-ID vor, die eben dem gewünschten Loadout entspricht.



