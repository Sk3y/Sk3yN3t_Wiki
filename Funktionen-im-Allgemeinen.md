# Was ist eine Funktion
In diesem Wiki dreht sich alles um Funktionen. Dabei geht es um mehr oder weniger kompakte SQF-Codefragmente, die unter einem Namen im Spiel abgespeichert sind und eine bestimmte Aufgabe ausführen. 

## Einführung

SQF nennt man die Programmier- oder Skriptsprache im Spiel, die die Befehle bereitstellt.

Funktionen können also benannte Skripte sein, die einfach nur in einer festgelegten Art und Weise etwas ausführen oder unter Umständen auch etwas berechnen und danach zurückgeben. Allgemein spricht man von Funktionen, wenn Dinge berechnet und an den Aufrufer zurückgegeben werden. So sind Funktionen ja auch jedem noch aus der Schule bekannt:
```Java
add(zahl1,zahl2) {
 return zahl1 + zahl2;
}
```
Dieses Beispiel illustriert, wie eine Funktion `add(arg1,arg2)` in einer bel. Programmiersprache aussehen könnte. Funktionen besitzen einen Namen (hier `add`), mögliche Argumente (hier `zahl1,zahl2`), einen Rumpf (hier `return zahl1 + zahl2;`) sowie einen möglichen Rückgabewert (hier `zahl1+zahl2`). Mit anderen Worten akzeptiert die Funktion also zwei Werte, bildet die Summe durch Addition und gibt dem Aufrufer das Resultat, nämlich die Summe, wieder zurück. Wir erwarten also durch Aufruf der Funktion `add(4,6)` einen Rückgabewert von `10`. 

Das soll als Vorbemerkung genügen. Jetzt schauen wir uns eine Funktion für die DB-Verwendung an und gehen das Gelernte an diesem Beispiel durch

## Die DB-Funktionen
```SQF
  ["jgkp_get_rank",[player]] call CBA_fnc_serverEvent;
```

Obwohl wir im Spiel für die DB-Funktionen das System der Event-Handler verwenden, ist es für euch als Benutzer nicht wichtig, sich mit Event-Handlern auszukennen.

Zunächst muss eine Funktion aufgerufen werden. In unserem obigen Beispiel geschah dies durch Angabe des Namens `add()` und Angabe der Übergabewerte. In SQF wird eine Funktion, wenn es ein Event-Handler ist, über `call CBA_fnc_clientToServerEvent` aufgerufen, jedenfalls wenn die Funktion auf dem Server laufen soll, was unsere Absicht ist. Dieser Abschnitt ist also für **alle** Funktionen gleich! Ihr braucht diesen Code folglich nicht weiter zu beachten.

Was bleibt dann noch? Wir müssen über den "Namen" der Funktion, die Übergabewerte und die Rückgabewerte sprechen. Der Aufruf mittels `call` erwartet zunächst einmal eckige Klammern, daher muss vor jedem call ein `[...]` stehen. Der erste Wert nach der eckigen Klammer ist dann der Name der Funktion bzw. des Event-Handlers. In unserem Beispiel ist das `"jgkp_get_rank"`. Damit sagen wir dem Spiel bzw. dem Server, dass wir bitte die Funktion `"jgkp_get_rank"` auf dem Server ausführen möchten. Diese Funktion, wie im Abschnitt [[Rangabfrage eines Spielers|Funktionen-zur-Userabfrage#rangabfrage-eines-spielers]] beschrieben, gibt uns Auskunft darüber, ob ein Spieler Mitglied der 3. Jägerkompanie ist. Also erwartet die Funktion einen Übergabewert. Dies muss nicht so sein. Andere Funktionen können auch gar keinen Übergabewert erwarten.

**Übergabewerte folgen immer nach dem Funktionsnamen in einem weiteren Paar eckige Klammern.**

Das sorgt dafür, dass die Übergabewerte stets als Liste, Array genannt, übergeben werden. In unserem Beispiel ist der einzige Übergabewert der Spieler selbst, daher übergeben wir `[player]` als Übergabewert. Damit hat die Funktion alles, was sie braucht, um zu arbeiten.

**Keine DB-Funktion gibt direkt an den Aufrufer einen Rückgabewert zurück. DIeser wird immer in einer separaten Variable gesendet**

Weil wir die Funktion auf dem Server ausführen lassen, hätte es keinen Sinn, die Funktion direkt etwas zurückgeben zu lassen, davon könnte nur der Server profitieren. Stattdessen erzeugt die Funktion eine nur für sie reservierte Variable, die immer mit `Result` anfängt, sofern die Funktion einen Rückgabewert besitzt. Einige Funktionen haben nur Übergabewerte, aber keine Rückgabewerte, andere genau andersherum. Sofern eine Funktion aber einen Rückgabewert besitzt, könnt ihr in diesem Wiki nachlesen, wie dieser heißt. Nach dem Aufruf der Funktion wird das Ergebnis dann in diese Variable gespeichert. Wie wir bei der Funktion nachlesen können, wird das Ergebnis in `ResultXMLRang` gespeichert.

Damit ist der Ablauf wie folgt:

1. Ihr sucht euch die gewünschte Funktion aus dem Wiki

2. Ihr lest euch die Übergabewerte durch. Dazu könnt ihr meist den gegebenen Aufruf einfach kopieren und die Werte in den inneren eckigen Klammern durch eure Objekte/Werte ersetzen.

3. Ihr führt die Funktion auf dem Server aus.

4. Falls die Funktion einen Rückgabewert besitzt, lest ihr diesen im Wiki nach und arbeitet damit weiter.

Ihr könnt also z.B. den Rang abfragen und dann `ResultXMLRang` weiter benutzen. Wichtig ist, dass der Rückgabewert ein String ist:
```SQF
ResultXMLRang = nil; // Var leeren vor Abfrage!
["jgkp_get_rank", [player]] call CBA_fnc_serverEvent;
waitUntil{!isNil "ResultXMLRang"};
_rang = parseNumber ResultXMLRang; //Überführt String in Number
if ( _rang > 6) then {
   hint "Du darfst das hier tun...";
   ... // weiterer Code
} else {
   hint "Dein Rang ist nicht hoch genug...";
};
```

In diesem Beispiel frage ich den Rang eines Spielers (also mir) zunächst ab und warte, bis die Information verfügbar ist. Danach wandle in den Text in eine Zahl um und führe den weiteren Code nur aus, wenn der Rang größer als 6 ist. Andernfalls teile ich dem Spieler mit, dass er leider nicht den erforderlichen Rang besitzt. Am Ende müssen wir die Variable leeren, da in einem nächsten Aufruf durchaus ein Fehler passieren könnte, z.B. wenn wir ein falsches Objekt übergeben. Der Server kann aber keine Fehler an uns zurückmelden, daher wird er einfach gar nichts tun und wir erhalten keine Fehlermeldung. Hätten wir die Variable `ResultXMLRang` jetzt nicht klugerweise geleert, so hätte sie immer noch den Rang vom ersten Aufruf gespeichert und wir könnten nie feststellen, ob das ein alter oder der neue Wert ist.