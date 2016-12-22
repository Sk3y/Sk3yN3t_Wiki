# Funktionen abschalten

Missionsbauer haben die Möglichkeit, bestimmte Funktionen abzuschalten. Solange der Missionsbauer nichts tut, gelten grundsätzlich die default-Werte, die im Addon hinterlegt sind und das heißt: Alles ist erlaubt (DebugConsole + San-Zelte für Sanitäter und an Fahrzeugen).

## Debug-Konsole abschalten

Der Missionsbauer kann die Debug-Konsole für reguläre Mitglieder bis Zugangslevel 2 deaktivieren. Admins mit Stufe 3 haben aber immer Zugang zur Konsole, was auch nicht abgeschaltet werden soll. Dazu muss der Missionsbauer lediglich in die ``init.sqf`` folgenden Befehl schreiben:
```SQF
// deaktiviert DC außer für Admins
JGKP_DC_disabled = true;
```

## San-Zelte abschalten

Der Missionsbauer kann den Aufbau der San-Zelte sowohl für die Sanitäter als auch an den Fahrzeugen abschalten. Dazu stehen die beiden folgenden Befehle zur Verfügung. Diese kommen in die ``init.sqf`` der Mission:
```SQF
// deaktiviert San-Zelte für Sanitäter und an Fahrzeugen
JGKP_FH_small_disabled = true; // für Sanitäter
JGKP_FH_big_disabled = true; // für Fahrzeuge
```

## Ändern während der Mission

Da die Variablen für den Zugriff im condition-Eintrag der ACE-Actionen vorkommen, ist es möglich, die obigen Variablen auch während der Mission zu ändern. Damit kann also auch während des Spiels der Zugriff verwehrt oder wieder erlaubt werden (z.B. die San-Zelte als Missionsziel nach der Eroberung einer Basis)
