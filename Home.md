# 3JGKP_Datenbankfunktionen
Diese Datei beschreibt die möglichen Funktionalitäten, um mit der Datenbank zu interagieren

## Funktionen
Hier werde ich nach und nach für euch Funktionsaufrufe posten, mit dennen ihr eure Missionen ausstatten könnt.

[[Funktionen-zur-Userabfrage]]
[[Funktionen-zur-Loadoutabfrage]]

**Wichtig:** Alle Rückgabewerte beginnen mit Result und sind mal String, mal Bool und manchmal vielleicht auch Zahl, daher lest euch unten den Rückgabewert durch!

Ebenso solltet ihr darauf achten, nach einer DB-Abfrage den Rückgabewert mit `Result = nil`wieder zu löschen, da ihr ansonsten bei einer erneuten Abfrage nicht entscheiden könnt, ob diese wirklich funktioniert hat oder ihr nicht noch mit dem alten Wert weiterarbeitet!

Aktueller Stand des Dialogs:
<https://youtu.be/S_wDeOHSwlE>

### Legende
str = String

int = Integer

bool = Boolean

### Bisherige Funktionen
- Abfrage, ob ein Spieler Mitglied der 3.JgKp ist
- Abfrage des Ranges eines Spielers
- Befüllen einer Kiste oder eines Fahrzeugs mit einem DB-Loadout
- Ausrüsten eines Spielers mit einem DB-Loadout
- Dialog zur Anzeige aller Loadouts
