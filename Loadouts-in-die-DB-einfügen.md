# Eigene Loadouts einreichen

Nun also wollt ihr eure eigenen Loadouts für eure Gruppe/euren Zug oder auch Public-Loadouts in die DB einfügen. Kein Problem! Wir haben euch diesen Prozess so angenehm wie möglich gestaltet.

Bitte lest euch aber zuerst durch, wie die [[DB aufgebaut|Datenbank-Layout]] ist. Dadurch versteht ihr den Sinn mancher Felder besser und vor allem das Format.

## Der Einfüge-Prozess

Wir unterscheiden **drei verschiedene** Feldertypen:
1. Felder mit nur einem Klassennamen oder einem String
2. Felder mit mehreren Klassennamen **ohne** Anzahl
3. Felder mit mehreren Klassennamen **und mit** Anzahl

Felder vom Typ 1 werden grundsätzlich nur mit dem Klassennamen befüllt, also z.B. `"BWA3-G36"`.

Felder vom Typ 2 werden grundsätzlich nur mit dem Klassennamen und einem `;` am Ende aufgelistet. Mehrere Klassennamen einfach hintereinander wegschreiben, ohne Leerzeichen. Immer an das letzte Item dann ein `;` anfügen. Auch bei nur einem Item erwartet das Eingabe-Formular ein `;`.

Felder vom Typ 3 werden grundsätzlich mit dem Klassennamen, gefolgt von einem `:`, der Anzahl der Items und einem abschließenden `;` eingetragen. Auch hier können beliebig viele Items hintereinanderweg aufgelistet werden. Alle Einträge müssen aber mit `;`abgeschlossen werden.

Eigene Loadouts:

    zug: enum('I', 'II', 'III')
    gruppe: enum('1.', '2.', '3.', 'HFlg', 'SanTrp', 'Nachschub', 'ZugTrp')
    typ: enum('Flecktarn', 'Tropentarn', 'Besatzung', 'Taucher', 'Nacht')
    name: varchar(255)
    headgear: text
    goggles: text
    vest: text
    vestitems: text
    uniform: text
    uniformitems: text
    backpack: text
    backpackitems: text
    weapons: text
    primaryweaponitems: text
    secondaryweaponitems: text
    handgunitems: text
    assignitems: text
    selectWeapon: text
    isMedic: {0,1}
    isEOD: {0,1,2}
    memberOnly: {0,1}

## Das Loadout-Formular

Um diesen Prozess übersichtlicher und benutzerfreundlicher zu gestalten, haben wir ein Formular entwickelt, dass euch als Eingabemaske dient. Dieses Formular besitzt bei fast jedem Feld über reguläre Prüfausdrücke, die genau die verlangte Form abprüfen und bei Fehlern ein Absenden verbieten. Daher ist es möglich, das Formular quasi die Fehlerüberprüfung durchführen zu lassen. Das Formular erkennt z.B. Namen, die mit Zahlen anfangen, Paare, wie "abc:1", bei denen das ";" am Ende fehlt usw. Natürlich können nicht alle Fehler (z.B. "abc__abc:1;", zwei Mal "_") abgefangen werden, aber es ist dennoch eine große Hilfe. Wir fügen eure Abgabe dann als csv-Datei per Import-Funktion in die DB ein.

Hier also der Link:
https://docs.google.com/forms/d/1gGk9CMg4pjWwtdUKJ3GNcLYqyNFRDtcRJvO3AJ117M0/viewform