1. Allgemein

2. Variablen

3. Datentypen

   1. Ganzzahl

   2. Fließkommazahl

   3. Zeichen

   4. Zeichenkette

   5. Wahrheitswert

4. Felder (Arrays)

5. Blöcke

6. Nichts

7. Operationen

   1. Vergleiche
      1. (Un)gleichheit
      2. Größer als, kleiner als
      3. Logische Operationen
   2. Arithmetische Operationen
      1. Addition
      2. Subtraktion
      3. Multiplikation
      4. Division
      5. Divisionsrest
   3. Umwandlung

8. Kontrollstrukturen

   1. Blöcke

   2. if 

   3. while

   4. for

9. Kommentare

10. Funktionen

    1. Native Funktionen
       1. Ausgabe

       2. Eingabe
    2. Sonstige

11. Fehler

# 1. Allgemein

Kartoffelskript ist eine imperative Sprache, welche eine, vollständig der deutschen Sprache angepasste, Syntax besitzt. Sie ist stark und statisch typisiert, allerdings nicht objektorientiert.

Quelltext besteht aus einer Reihe von Anweisungen und Definitionen. Zu Anweisungen gehören Deklarationen, Zuweisungen, Kontrollstrukturen sowie Ausdrücke. Die Anweisungen sind syntaktisch alle dem deutschen Imperativ angepasst.

Anweisungen werden mit einem Punkt `.` beendet. Zeilenumbrüche können und sollten an den Stellen genutzt werden, an denen sie Sinn ergeben. 

In Kartoffelskript ist besonders eine Sache wichtig: **Der Quelltext sollte sich nach Möglichkeit wie ein deutscher, grammatikalisch korrekter Text lesen.**

# 2. Variablen

Variablen müssen mit expliziter Typangabe deklariert werden. Sie können, müssen aber nicht im gleichen Zuge initialisiert werden. Der Typ einer Variablen ist nicht mehr veränderbar, der Wert einer Variable schon. Eine Variable kann nicht denselben Namen wie eine bereits existierende haben. Variablen dürfen aus mehreren Wörtern bestehen. Zu den Benennungskonventionen, siehe Style Guide.

Grundsätzlich wird die Schlüsselwortkombination `setze <Variable> auf <Wert>` benutzt, um Variablen einen Wert zuzuweisen. Die Deklaration findet nur einmal am Anfang statt und hat die Form `sei[en] <Variable> ein <Typ>`.  Um eine Variable zu initialisieren, muss an die Deklaration `mit dem Wert <Wert>` gehängt werden.

Nach einer Deklaration bekommt jede Variable den Standardwert `nichts`, sofern sie nicht initialisiert wurde. (s.u.).

Beispiele:

```
Sei Nummer eine Ganzzahl.

Sei Begrüßung eine Zeichenkette mit dem Wert "Hallo, Welt".
```

Für Zahlentypen (`Ganzzahl`, `Fließkommazahl`) gibt es noch zwei zusätzliche Zuweisungsmöglichkeiten:

```
Sei x eine Ganzzahl.
Setze x auf 0.
Erhöhe x um 1.
Verringere x um 1.
```

Dies ist äquivalent zu:

```
Sei x eine Ganzzahl.
Setze x auf 0.
Setze x auf x + 1.
Setze x auf x - 1.
```

**Variablen können zu jedem Zeitpunkt einen bestimmten Artikel als Präfix und eine Angleichung zu einem bestimmten Fall erhalten, um grammatikalisch korrekte Sätze zu ermöglichen.**

*Implementation note: Nutzung eines [Morphologie-Wörterbuchs](http://www.danielnaber.de/morphologie/)*

Sollte ein Artikel bei der Deklaration genutzt werden, zählt dieser effektiv nicht mit zum Namen der Variable. Stattdessen wird der Nominativ aus dem, dem Artikel folgenden, Wort (sofern es existiert, korrekte Komposita gehen auch) gebildet und als Variablenname genutzt. Bei Substantiven mit Adjektiven werden letztere auch mit einbezogen. Wird kein Artikel verwendet, so findet dies nicht statt. Auch in späteren Referenzen kann auf den Artikel verzichtet werden. Nur, wenn einer benutzt wird, wird der eigentliche Name aus der auf den Artikel folgenden Form rekonstruiert. 

Erstes Beispiel (mit Artikeln):

```
Sei die Nummer eine Ganzzahl mit dem Wert 5.

Sei die Begrüßung eine Zeichenkette mit dem Wert "Hallo, Welt".
```

Damit auch bei Angleichung immer noch die richtigen Variablen referenziert werden, wird über ein Wörterbuch nach dem passenden Wort für eine angeglichene Form gesucht. Sollte die Form trotz Artikel falsch sein, wird ein Grammatikfehler geworfen. Wörter, die nicht Teil der deutschen Sprache sind, können somit keine Artikel erhalten.

# 3. Datentypen

In Kartoffelskript gibt es ein paar grundlegende Datentypen, die für Variablen genutzt werden können. Jede Variable und jeder Ausdruck hat einen dieser Datentypen (Felder fallen genau genommen auch darunter, werden hier aber als Spezialfall gelistet). Alle Datentypen können per Umwandlung in einen anderen umgewandelt werden (s.u.).

Alle Ausdrücke können als Präfix ein `<Artikel> <Typ>` erhalten, um die Grammatik an einigen Punkten zu verbessern. Die Artikel können entsprechend des Falls natürlich auch variieren.

```
Setze w auf 4 ist ungleich 5. 
Setze w auf die Aussage 4 ist ungleich 5.
```

## 3.1. Ganzzahl

Der Typ `Ganzzahl` (`eine Ganzzahl`) beschreibt einen signed Integer mit einer Größe von 32 Bit. Die Reichweite ist also -2^31 - 2^31 - 1. Er ist das Äquivalent zu `int` aus Java.

Auf Ausdrücke dieses Typens können die 4 arithmetischen Grundoperationen sowie die Divison mit Rest angewendet werden.

Direkte Ausdrücke (literal expressions) werden als einfache Zahl dargestellt. Für negative Zahlen muss davor ein `-` stehen. Da es sich um eine Ganzzahl handelt, sind Kommata nicht erlaubt.

Beispiel:

```
Sei x eine Ganzzahl mit dem Wert 765443.
```

## 3.2. Gleitkommazahl

Der Typ `Gleitkommazahl` (`eine Gleitkommazahl`) beschreibt wie `Ganzzahl` eine 32-Bit große Zahl, nur, dass diese auch Kommazahlen ermöglicht. Er ist das Äquivalent zu `float` aus Java.

Auf Ausdrücke dieses Typens können die 4 arithmetischen Grundoperationen angewendet werden.

Direkte Ausdrücke werden entweder wie als Ganzzahl dargestellt oder im Falle einer Kommazahl mit einem Komma `,`. 

Beispiel:

```
Sei Pi eine Gleitkommazahl mit dem Wert 3,14159.
```

## 3.3. Zeichen

Der Typ `Zeichen` beschreibt ein 16-Bit großes Zeichen. Er ist das Äquivalent zu `char` aus Java.

Direkte Ausdrücke werden in Hochkommata `'` eingeschlossen. Sie dürfen maximal ein Zeichen enthalten. 

Beispiel:

```
Sei der Buchstabe ein Zeichen mit dem Wert 'X'.
```

## 3.4. Zeichenkette

Der Typ `Zeichenkette` ist das Äquivalent zu `string` aus anderen Sprachen.

Direkte Ausdrücke werden in Anführungszeichen `"` eingeschlossen. Zeichenketten können mit dem Operator `+` konkateniert werden.

Beispiel:

```
Sei das Grußwort eine Zeichenkette mit dem Wert "Hallo".
Sei der Name eine Zeichenkette mit dem Wert "Johnny".

Sei die Begrüßung eine Zeichenkette.
Setze die Begrüßung auf das Grußwort + ", " + den Namen.
```

Außerdem bieten Zeichenketten eine native Funktion. Die Zeichen einer Zeichenkette können mit dem Ausdruck `Zeichen in <Zeichenkette>`  erhalten werden. Die Rückgabe dieses Ausdrucks ist ein `Zeichen-Feld`.

## 3.5. Aussage

Der Typ `Aussage` beschreibt einen simplen, binären Wert. Er ist das Äquivalent zu `boolean` oder `bool` aus anderen Sprachen.

Er kann nur einen von genau zwei Werten besitzen: `wahr` oder `falsch`. Außerdem werden Ausdrücke dieses Typs für Bedingungen in Kontrollstrukturen verwendet (dazu später mehr).

Beispiel:

```
Sei die Bedingung eine Aussage mit dem Wert wahr.
```

# 4. Felder (Arrays)

Felder sind Ansammlungen fester Größe von Werten desselben Datentyps und das Äquivalent zu Arrays in anderen Sprachen.

Sie werden deklariert als `<Typ>-Feld`. Der Zugriff auf einzelne Elemente eines Feldes erfolgt über Indizes in der Form `Element <Index> aus <Feld>`. Dieser Ausdruck gibt einen Wert des Feld-Typen zurück oder verursacht einen Fehler, wenn der Index außerhalb der Grenzen des Feldes liegt.

Felder fangen bei 1 an, nicht bei 0 wie in anderen Sprachen.

Ein neues Feld wird so erzeugt: `ein leeres Feld der Größe <Größe>`. Der Typ des Feldes wird inferiert. Die Größe gibt an, wie viele Elemente das Feld beinhaltet. Ein leeres Feld beinhaltet an jedem Index `nichts`.

So wird ein Feld erzeugt:

```
Sei das Array ein Ganzzahl-Feld.
Setze das Array auf ein leeres Feld der Größe 5.
```

So werden Werte eingetragen:

```
Setze Element 1 aus dem Array auf -10.
Setze Element 2 aus dem Array auf 42.
```

So werden Werte ausgelesen:

```
Sei die Antwort eine Ganzzahl.
Setze die Antwort auf Element 2 aus dem Array.
```

Mit dem Ausdruck `die Größe von <Feld>` lässt sich die ganzzahlige Anzahl der Elemente eines Feldes holen.

# 5. Blöcke

Blöcke werden genutzt, um mehrere Anweisungen zu einer zusammenzufassen. Dies ist besonders für Kontrollstrukturen wichtig.

Das Ausführen von Blöcken hat keinen Rückgabewert.

```
Führe den Block {
    # Anweisungen
} aus.
```

# 6. Nichts

Das Schlüsselwort `nichts` beschreibt einen fehlenden Wert und ist äquivalent zu `null` aus Java. Jedoch ist `nichts`  in Kartoffelskript ein gültiger Wert für jeden Datentypen und der Standardwert für jede neu deklarierte Variable.

Wird eine Operation wie Umwandlung oder eine arithmetische Operation oder eine Funktion auf einen `nichts`-Wert angewendet, so kommt es zu einem Fehler.

Beispiel:

```
Sei das Wort eine Zeichenkette.
Sei der Inhalt ein Zeichen-Feld.
Setze den Inhalt auf die Zeichen in dem Wort. # Fehler
```

# 7. Operationen

## 7.1. Vergleiche

Vergleiche sind Operationen, die immer auf zwei Operanden mithilfe eines Operators angewendet werden und einen `Aussage` zurückgeben. Sie sind also Ausdrücke.

Um einen Vergleich als Wert für den Typ `Aussage` zu nutzen, muss er das Präfix `<Artikel entsprechend des Falls> Aussage:` erhalten.

### 7.1.1. (Un)gleichheit

Auf Gleich- und Ungleichheit wird mit den Operatoren `gleich` und `ungleich` geprüft.

```
Sei die Wahrheit eine Aussage.
Setze die Wahrheit auf die Aussage 5 ist gleich 5.
Setze die Wahrheit auf die Aussage 3 ist ungleich 5.
```

Vorsicht: wenn es sich beim zweiten Operanden um eine Variable mit Artikel handelt, muss der Name der Variablen im Dativ stehen.

```
Sei der Name eine Zeichenkette mit dem Wert "Lena".
Sei die Bedingung eine Aussage mit dem Wert der Aussage "Lena" ist gleich dem Namen.
```

### 7.1.2. Größer als, kleiner als

Größer als hat in Kartoffelskript den Operator `größer als`, kleiner als den Operator `kleiner als`. Für inklusives < und > gibt es die Operatoren `kleiner gleich` und `größer gleich`.

```
Sei w eine Aussage.
Setze w auf die Aussage 4 ist kleiner gleich 5.
Setze w auf die Aussage 5 ist größer als 10.
```

### 7.1.3. Logische Operationen

Logische Operationen in Kartoffelskript beschränken sich auf die Operatoren `und` (AND), `oder` (OR) und `nicht` (NOT).  `oder` und `und` werden genutzt, um Aussagen miteinander zu verknüpfen:

```
Sei w eine Aussage.
Setze w auf die Aussage wahr oder falsch. # w = wahr
Setze w auf die Aussage wahr und falsch.  # w = falsch
```

`nicht` negiert das Ergebnis einer Operation und kann für jeden Vergleichsoperator nach dem `ist` eingefügt werden:

```
Sei w eine Aussage.
Setze w auf die Aussage 5 ist größer als 4.       # w = wahr
Setze w auf die Aussage 5 ist nicht größer als 4. # w = falsch
```

## 7.2. Arithmetische Operationen

Zu den arithmetischen Operationen gehören die 4 Grundoperationen plus, minus, mal und geteilt. Die Rechenregeln für diese werden beachtet (Punkt vor Strich) und Klammersetzung wird unterstützt.

### 7.2.1. Addition

Um die Summe zweier Zahlenwerte zu erhalten, wird der Additionsoperator `+` genutzt.

```
Setze die Summe auf 2 + 3.
```

### 7.2.2. Subtraktion

Um die Differenz zweier Zahlenwerte zu erhalten, wird der Subtraktionsoperator `-` genutzt.

```
Setze die Differenz auf 3 - 2.
```

### 7.2.3. Multiplikation

Um das Produkt zweier Zahlenwerte zu erhalten, wird der Multiplikationsoperator `*`  genutzt.

```
Setze das Produkt auf 2 * 3.
```

### 7.2.4. Division

Um den Quotienten zweier Zahlenwerte zu erhalten, wird der Divisionsoperator `/` genutzt.

Ist der Divisor des Ausdrucks = 0, so gibt es einen Fehler.

```
Setze den Quotienten auf 6 / 3.
```

### 7.2.5. Divisionsrest

Um den ganzzahligen Rest einer Division mit zwei Ganzzahlen zu erhalten, wird der Modulo-Operator `mod` genutzt.

```
Setze den Rest auf 10 mod 3.
```

## 7.3. Umwandlung

Wie bereits erwähnt, können die Datentypen `Ganzzahl`, `Fließkommazahl`, `Zeichen`, `Zeichenkette` und `Wahrheitswert` ineinander umgewandelt werden.

Umwandlungen irgendeines Typen in eine Zeichenkette umschließen den Wert als des Typen in einer Zeichenkette. Umgekehrt, um eine Zeichenkette in einen anderen Typen umzuwandeln, muss die Zeichenkette einem direkten, zu dem Typ passenden, Wert entsprechen.

Eine Umwandlung von `Ganzzahl` zu `Zeichen` oder `Fließkommazahl` ist immer möglich, umgekehrt gibt es bei `Fließkommazahl` zu `Ganzzahl` die Einschränkung, dass Nachkommastellen wegfallen.

Zum Umwandeln dient das Schlüsselwort `als`.

```
Sei der Text eine Zeichenkette mit dem Wert "42".
Sei der Zahlenwert eine Ganzzahl mit dem Wert des Textes als Ganzzahl.
```

Ob ein Wert in einen anderen umgewandelt werden kann, kann mit dem Operator `ist` überprüft werden.

```
Sei w eine Aussage.
Setze w auf die Aussage: "3" ist eine Ganzzahl.
```

# 8. Kontrollstrukturen

Kontrollstrukturen verändern den Programmfluss in Abhängigkeit von Bedingungen. 

## 8.2. if

Die Schlüsselphrase für if-Statements ist `wenn <Aussage> <wahr/falsch> ist, <Anweisung>.` Zuerst wird die Aussage evaluiert und dann mit dem darauffolgenden, direkten Wert verglichen. Ergibt dies wiederum `wahr`, so wird die folgende Anweisung ausgeführt.

```
Sei die eine Bedingung eine Aussage mit dem Wert wahr.
Sei die andere Bedingung eine Aussage mit dem Wert falsch.

Sei x eine Ganzzahl.

Wenn die eine Bedingung wahr ist, setze x auf 0.
Wenn die andere Bedingung wahr ist, führe den Block {
    Setze x auf y.
    Erhöhe x um 3.
} aus.
```

## 8.3 while

Die Schlüsselphrase für `while`-Schleifen ist `solange <Aussage> <wahr/falsch> ist, <Anweisung>`.  Für `do-while`-Schleifen werden Haupt- und Nebensatz einfach vertauscht. Die Überprüfung der Bedingung findet genau so statt wie bei if-Statements.

```
Sei w eine Aussage mit dem Wert falsch.

Solange w wahr ist, führe den Block {} aus. # Wird kein Mal ausgeführt (While)
Führe den Block {} aus, solange w wahr ist. # Wird ein Mal ausgeführt (Do-While)
```
