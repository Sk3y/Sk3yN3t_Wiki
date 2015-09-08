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
  ["jgkp_get_rank",[player]] call CBA_fnc_clientToServerEvent;
```
