# Performancemessung

Das Serveraddon bietet euch ebenfalls eine Funktion zur Messung und Speicherung von Performance-Messwerten, aktuell FPS.

Dazu kann die Funktion
```SQF
["jgkp_log_fps", [time]] call CBA_fnc_clientToServerEvent;
```

time (int): Zeit in Sekunden, die geloggt werden.

Die Funktion loggt während der angegebenen Zeitspanne von `time` Sekunden die FPS aller Spieler, der headless clients sowie des Servers und speichert das Ergebnis in der Datenbank. Bei Interesse an den Daten kann Sk3y kontaktiert werden, der für uns eine Visualisierung der Rohdaten geschrieben hat!