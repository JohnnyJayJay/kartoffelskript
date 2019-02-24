1. Allgemein

2. Variablen

3. Datentypen

   1. Ganzzahl

   2. Fließkommazahl

   3. Zeichen

   4. Zeichenkette

   5. Wahrheitswert

4. Felder (Arrays)

5. Nichts

6. Operationen

   1. Vergleiche
      1. (Un)gleichheit
      2. Größer als, kleiner als
      3. Boolesche Operatoren
   2. Arithmetische Operationen
   3. Ausgabe
   4. Eingabe
   5. Umwandlung

7. Kontrollstrukturen

   1. if / if-else / if-elseif

   2. while

   3. for-each

8. Funktionen

9. Fehler

# 1. Allgemein

Kartoffelskript ist eine interpretierte, imperative Sprache, welche eine, vollständig der deutschen Sprache angepasste, Syntax besitzt. Sie ist stark und statisch typisiert, allerdings nicht objektorientiert.

Quelltext besteht aus einer Reihe von Anweisungen und Definitionen. Zu Anweisungen gehören Deklarationen, Zuweisungen, Kontrollstrukturen sowie Ausdrücke. Die Anweisungen sind syntaktisch alle dem deutschen Imperativ angepasst.

Anweisungen werden mit einem Punkt `.` beendet **oder** mit einer anderen Anweisung durch ein `und` verknüpft. Satzanfänge  (nach einem Punkt) sollten immer großgeschrieben sein, das gilt auch für sämtliche, normalerweise klein geschriebene, Schlüsselwörter. Zeilenumbrüche können und sollten an den Stellen genutzt werden, an denen sie Sinn ergeben. 

In Kartoffelskript ist besonders eine Sache wichtig: **Der Quelltext sollte sich nach Möglichkeit wie ein deutscher, grammatikalisch korrekter Text lesen.**

# 2. Variablen

Variablen müssen mit expliziter Typangabe deklariert werden. Sie können zwar nicht im gleichen Zuge initialisiert werden, also einen Wert erhalten, die Anweisungen können jedoch über ein `und` verknüpft werden. Der Typ einer Variablen ist nicht mehr veränderbar, der Wert einer Variable schon. Eine Variable kann nicht denselben Namen wie eine bereits existierende haben. Ein Variablenname darf keine Leerzeichen beeinhalten. Zu den Benennungskonventionen, siehe Style Guide.

Grundsätzlich wird die Schlüsselwortkombination `setze <Variable> auf <Wert>` benutzt, um Variablen einen Wert zuzuweisen. Die Deklaration findet nur einmal am Anfang statt und hat die Form `deklariere <Variable> als <Typ>`. 

Nach einer Deklaration bekommt jede Variable den Standardwert `nichts` (s.u.).

Beispiele:

```
Deklariere Nummer als Ganzzahl und setze Nummer auf 5.

Deklariere Begrüßung als Zeichenkette.
Setze Begrüßung auf "Hallo, Welt".
```

Für Zahlentypen (`Ganzzahl`, `Fließkommazahl`) gibt es noch zwei zusätzliche Zuweisungsmöglichkeiten:

```
Deklariere x als Ganzzahl und setze x auf 1.
Erhöhe x um 1.
Verringere x um 1.
```

Dies ist äquivalent zu:

```
Deklariere x als Ganzzahl und setze x auf 1.
Setze x auf x + 1.
Setze x auf x - 1.
```

**Variablen können zu jedem Zeitpunkt einen bestimmten Artikel im Nominativ (der, die, das), im Dativ (dem, der, dem) oder im Akkusativ (den, die, das) als Präfix erhalten, um grammatikalisch korrekte Sätze zu ermöglichen.**

Leider kann es zu Komplikationen kommen, da gerade die männliche Form (der) im Akkusativ und Dativ häufig angeglichen werden muss. Beispiel: *der* Buchstabe, aber *den* Buchstaben.

**Potentielle Lösungen hierfür: Trennzeichen (unsichtbar), escapen, Wörterbuch-Resource (bei Variablen mit mehreren Wörtern letztes Wort nutzen - ansonsten auch _ und - erlauben) // TODO**

Diese drei Fälle sollten für gewöhnlich die einzigen sein, die in Bezug auf eine Variable vorkommen. Ausnahmen gibt es bei nativen Funktionen wie bei Zeichenketten (s.u.), diese fallen jedoch nicht darunter.

Erstes Beispiel (mit Artikeln):

```
Deklariere die Nummer als Ganzzahl und setze die Nummer auf 5.
Deklariere die Begrüßung als Zeichenkette.

Setze die Begrüßung auf "Hallo, Welt".
```

# 3. Datentypen

In Kartoffelskript gibt es ein paar grundlegende Datentypen, die für Variablen genutzt werden können. Jede Variable und jeder Ausdruck hat einen dieser Datentypen. Alle Datentypen können per Umwandlung in einen anderen umgewandelt werden.

## 3.1. Ganzzahl

Der Typ `Ganzzahl` beschreibt einen signed Integer mit einer Größe von 32 Bit. Die Reichweite ist also -2^31 - 2^31 - 1. Er ist das Äquivalent zu `int` aus anderen Sprachen.

Auf Ausdrücke dieses Typens können die 5 arithmetischen Grundoperationen angewendet werden.

Direkte Ausdrücke (literal expressions) werden als einfache Zahl dargestellt. Für negative Zahlen muss davor ein `-` stehen. Da es sich um eine Ganzzahl handelt, sind Kommata nicht erlaubt.

Beispiel:

```
Deklariere x als Ganzzahl und setze x auf -12.
Setze x auf 765443.
```

## 3.2. Fließkommazahl

Der Typ `Fließkommazahl` beschreibt wie `Ganzzahl` eine 32-Bit große Zahl, nur, dass diese auch Kommazahlen ermöglicht. Er ist das Äquivalent zu `float` aus anderen Sprachen.

Auf Ausdrücke dieses Typens können die 5 arithmetischen Grundoperationen angewendet werden.

Direkte Ausdrücke werden entweder wie als Ganzzahl dargestellt oder im Falle einer Kommazahl mit einem Komma `,`. 

Beispiel:

```
Deklariere Pi als Fließkommazahl und setze Pi auf 3,14159.
```

## 3.3. Zeichen

Der Typ `Zeichen` beschreibt ein 16-Bit großes Zeichen. Er ist das Äquivalent zu `char` aus anderen Sprachen.

Direkte Ausdrücke werden in Hochkommata `'` eingeschlossen. Sie dürfen maximal ein Zeichen enthalten. Unicode wird unterstützt.

Beispiel:

```
Deklariere Buchstabe als Zeichen und setze Buchstabe auf 'X'.
```

## 3.4. Zeichenkette

Der Typ `Zeichenkette` ist das Äquivalent zu `string` aus anderen Sprachen.

Direkte Ausdrücke werden in Anführungszeichen `"` eingeschlossen. Zeichenketten können mit dem Operator `+` konkateniert werden.

Beispiel:

```
Deklariere das Grußwort als Zeichenkette und setze das Grußwort auf "Hallo".
Deklariere den Namen als Zeichenkette und setze den Namen auf "Johnny".

Deklariere die Begrüßung als Zeichenkette.
Setze die Begrüßung auf das Grußwort + ", " + den Namen.
```

Außerdem bieten Zeichenketten eine native Funktion. Die Zeichen einer Zeichenkette können mit dem Ausdruck `Zeichen in <Zeichenkette>`  erhalten werden. Die Rückgabe dieses Ausdrucks ist ein `Feld mit Zeichen-Werten`.

## 3.5 Wahrheitswert

Der Typ `Wahrheitswert` beschreibt einen simplen, binären Wert. Er ist das Äquivalent zu `boolean` oder `bool` aus anderen Sprachen.

Er kann nur einen von genau zwei Werten besitzen: `wahr` oder `falsch`. Außerdem können Werte dieses Typs direkt in Bedingungen für Kontrollstrukturen verwendet werden (dazu später mehr).

Beispiel:

```
Deklariere die Bedingung als Wahrheitswert und setze die Bedingung auf wahr.
```

# 4. Felder (Arrays)

Felder sind Ansammlungen fester Größe von Werten desselben Datentyps und das Äquivalent zu Arrays in anderen Sprachen.

Sie werden deklariert als `<Typ>-Feld`. Der Zugriff auf einzelne Elemente eines Feldes erfolgt über Indizes in der Form `Element <Index> aus <Feld>`. Dieser Ausdruck gibt einen Wert des Feld-Typen zurück oder verursacht einen Fehler, wenn der Index außerhalb der Grenzen des Feldes liegt.

Felder fangen bei 1 an, nicht bei 0 wie in anderen Sprachen.

Ein neues Feld wird so erzeugt: `neues Feld der Größe <Größe>`. Der Typ des Feldes wird inferiert. Die Größe gibt an, wie viele Elemente das Feld beinhaltet. Ein leeres Feld beinhaltet an jeder Position `nichts`.

So wird ein Feld erzeugt:

```
Deklariere das Array als Ganzzahl-Feld und setze das Array auf neues Feld der Größe 5.
```

So werden Werte eingetragen:

```
Setze das Element 1 aus Array auf -10.
Setze das Element 2 aus Array auf 42.
```

So werden Werte ausgelesen:

```
Deklariere die Antwort als Ganzzahl.
Setze die Antwort auf Element 2 aus Array.
```

# 5. Nichts

Das Schlüsselwort `nichts` beschreibt einen fehlenden Wert und ist äquivalent zu `null` aus Java. Jedoch ist `nichts`  in Kartoffelskript ein gültiger Wert für jeden Datentypen und der Standardwert für jede neu deklarierte Variable.

Wird eine Operation wie Umwandlung oder eine arithmetische Operation oder eine Funktion auf einen `nichts`-Wert angewendet, so kommt es zu einem Fehler.

Beispiel:

```
Deklariere das Wort als Zeichenkette.
Deklariere den Inhalt als Zeichen-Feld.
Setze den Inhalt auf die Zeichen in dem Wort.  <-- Fehler
```

# 6. Operationen

## 6.1. Vergleiche

Vergleiche sind Operationen, die immer auf zwei Operanden mithilfe eines Operators angewendet werden und einen `Wahrheitswert` zurückgeben. Sie sind also Ausdrücke.
