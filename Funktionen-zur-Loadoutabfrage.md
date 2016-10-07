## Loadout-Funktionen
Alle folgenden Funktionen dienen dazu, Loadouts aus der DB zur Verfügung zu stellen.

### Spieler mit Loadout ausrüsten
```SQF
    ["jgkp_equip_loadout", [unit, id]] call CBA_fnc_serverEvent;
```
**Beschreibung:** Rüstet die übergebene Einheit `unit` mit dem Inhalt des Loadouts für die gegebene ID (PK in DB) aus. 

**Übergabewert:**

* unit (object): Einheit, die ausgerüstet werden soll, für den Spieler `player` nutzen oder seinen Variablennamen oder `this` innerhalb der Init-Zeile. 
* ID (int): ID (Primary Key) des Loadouteintrags in der DB. Muss in der DB existieren (s.u.).

**Rückgabewert:** Hier gibt es keinen Rückgabewert. Der Spieler wird automatisch sofort mit dem gewählten Loadout ausgestattet.

**Wichtig**: Die Funktion kann entweder innerhalb des neu erstellten [[Dialogsystems|Der-Loadout-Dialog]] verwendet werden (Button Lade Loadout), oder auch direkt z.B. in der Init-Zeile einer Einheit, sofern man die ID kennt! Diese kann man aber über besagten [[Dialog|Der-Loadout-Dialog#loadout-load]] in Erfahrung bringen, denn die ID des Loadouts steht hinter dem Namen des Loadouts in runden Klammern!

#### Spieler zu Missionsbeginn ausrüsten

In diesem Falle können wir den obigen Befehl nicht 1:1 verwenden und z.B. in die init-Zeile einer Einheit schreiben, da dies nicht JIP-sicher ist. Denn bei jedem neuen Spieler werden Skripte in der Init-Zeile erneut ausgeführt.

Die Lösung sieht daher zweigeteilt aus:

1. Erstelle eine `onPlayerRespawn.sqf` mit dem folgenden Inhalt:

    ```SQF
    ["jgkp_equip_loadout", [player, player getVariable ["LoadoutID", 164]]] call CBA_fnc_serverEvent;;
    ```
    Diese Zeile bewirkt, dass jeder Spieler beim Respawn und zu Missionsbeginn diese Zeile ausführt, die vom Server  das entsprechende Loadout abfragt. Dazu muss der Spieler aber die Variable `LoadoutID` besitzen. Deshalb folgt nun noch der zweite Schritt:

2. Füge bei jeder Einheit, die zu Missionsbeginn ausgerüstet werden soll, folgende Zeile in die init-Zeile ein:
    ```SQF
    this setVariable ["LoadoutID", id];
    ```   

    Diese Zeile fügt jeder Einheit eine Variable `LoadoutID` hinzu. Der Inhalt wird im zweiten Argument `id` festgelegt. Hier müsst ihr natürlich **eine korrekte ID aus der DB** vergeben. D.h. ihr überlegt euch, welches Loadout die Einheit zu Missionsbeginn erhalten soll und speichert die zugehörige ID mit dem Befehl `setVariable` mit der Einheit. Diese erhält dann bei jedem Respawn das angegebene Loadout.

**ACHTUNG**: Die Zahl 164 beim Befehl `getVariable` im 1. Schritt sorgt dafür, dass jede Einheit bzw. genauer jeder Spieler, bei dem der zweite Schritt vergessen wurde, standardmäßig das Loadout mit der ID 164 erhält (und damit keinen Fehler produziert).

#### Loadouts per Add-Action-Menü

Möchtet ihr ein Loadout z.B. fest mit einem Aktionmenüeintrag verbinden, ist dies wie folgt möglich:

```SQF
this addAction ["<t color='#00ff00' size='1.2'>Loadout GrpFhr</t>", {
["jgkp_equip_loadout",[player,164]] call CBA_fnc_serverEvent;;
}];
```

Dieser Befehl kommt in die jeweilige init-Zeile eurer Kiste/eures Fahrzeuges etc. Das erste Argument enthält den Text des Befehls, der dem Spieler angezeigt wird, hier könnt ihr euch beliebig austoben. Das Beispiel nutzt eine Schrift, die um 20 % vergrößert wurde (`size='1.2'`) und grün ist (`color='#00ff00'`). Das zweite Argument ist ein Code-Block, der aufgerufen wird, sobald der Spieler den Befehl auswählt. Dieser Befehl ist mit dem Befehl im obigen Abschnitt fast identisch, **aber** wir fragen natürlich nicht die Loadout-ID des Spielers ab, sondern geben eine Loadout-ID vor, die eben dem gewünschten Loadout entspricht.



