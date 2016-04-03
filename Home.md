# 3JGKP Datenbankfunktionen
Diese Datei beschreibt die möglichen Funktionalitäten, um mit der Datenbank zu interagieren

# Version
V 1.00

## Funktionen
Hier werde ich nach und nach für euch Funktionsaufrufe posten, mit denen ihr eure Missionen ausstatten könnt.

**neu** Bitte bei wenig SQF-Erfahrung zuerst den kurzen Abschnitt über [[Funktionen im Allgemeinen|Funktionen im Allgemeinen]] durchlesen!

Ihr kommt zu den Funktionen, indem ihr diesen Links folgt oder rechts die Unterseiten auswählt:
[[Funktionen-zur-Userabfrage]] | 
[[Funktionen-zur-Loadoutabfrage]]

**Wichtig:** Alle Rückgabewerte beginnen mit Result und sind mal String, mal Bool und manchmal vielleicht auch Zahl, daher lest euch unten den Rückgabewert durch!

Ebenso solltet ihr darauf achten, nach einer DB-Abfrage den Rückgabewert mit `Result<name> = nil`wieder zu löschen, da ihr ansonsten bei einer erneuten Abfrage nicht entscheiden könnt, ob diese wirklich funktioniert hat oder ihr nicht noch mit dem alten Wert weiterarbeitet!

Aktueller Stand des Dialogs:
<https://youtu.be/Cn301ZJoex0>

### Legende
str = String

int = Integer

bool = Boolean

### Bisherige Funktionen
- [[Abfrage, ob ein Spieler Mitglied der 3.JgKp ist|Funktionen-zur-Userabfrage#memberüberprüfung-eines-spielers]]
- [[Abfrage des Ranges eines Spielers|Funktionen-zur-Userabfrage#rangabfrage-eines-spielers]]
- [[Befüllen einer Kiste oder eines Fahrzeugs mit einem DB-Loadout|Funktionen-zur-Loadoutabfrage#kisten-und-fahrzeuge-einmalig-mit-loadout-befüllen]]
- [[Ausrüsten eines Spielers mit einem DB-Loadout|Funktionen-zur-Loadoutabfrage#spieler-mit-loadout-ausrüsten]]
- [[Dialog zur Anzeige aller Loadouts|Der-Loadout-Dialog]]

### Der Loadout-Dialog im Spiel
- [[Der-Loadout-Dialog|Der-Loadout-Dialog]]

### Wie ist die DB aufgebaut?
- [[Datenbank-Layout|Datenbank-Layout]]
