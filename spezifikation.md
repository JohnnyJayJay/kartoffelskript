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
      1. Addition
      2. Subtraktion
      3. Multiplikation
      4. Division
      5. Divisionsrest
   3. Umwandlung

7. Kontrollstrukturen

   1. if / if-else / if-elseif

   2. while

   3. for-each

8. Funktionen

   1. Native Funktionen
      1. Ausgabe

      2. Eingabe
   2. Sonstige

9. Fehler

# 1. Allgemein

Kartoffelskript ist eine interpretierte, imperative Sprache, welche eine, vollständig der deutschen Sprache angepasste, Syntax besitzt. Sie ist stark und statisch typisiert, allerdings nicht objektorientiert.

Quelltext besteht aus einer Reihe von Anweisungen und Definitionen. Zu Anweisungen gehören Deklarationen, Zuweisungen, Kontrollstrukturen sowie Ausdrücke. Die Anweisungen sind syntaktisch alle dem deutschen Imperativ angepasst.

Anweisungen werden mit einem Punkt `.` beendet **oder** mit einer anderen Anweisung durch ein `und` verknüpft. Satzanfänge  (nach einem Punkt) sollten immer großgeschrieben sein, das gilt auch für sämtliche, normalerweise klein geschriebene, Schlüsselwörter. Zeilenumbrüche können und sollten an den Stellen genutzt werden, an denen sie Sinn ergeben. 

In Kartoffelskript ist besonders eine Sache wichtig: **Der Quelltext sollte sich nach Möglichkeit wie ein deutscher, grammatikalisch korrekter Text lesen.**

# 2. Variablen

Variablen müssen mit expliziter Typangabe deklariert werden. Sie können zwar nicht im gleichen Zuge initialisiert werden, also einen Wert erhalten, die Anweisungen können jedoch über ein `und` verknüpft werden. Der Typ einer Variablen ist nicht mehr veränderbar, der Wert einer Variable schon. Eine Variable kann nicht denselben Namen wie eine bereits existierende haben. Ein Variablenname darf keine Leerzeichen beeinhalten. Zu den Benennungskonventionen, siehe Style Guide.

Grundsätzlich wird die Schlüsselwortkombination `setze <Variable> auf <Wert>` benutzt, um Variablen einen Wert zuzuweisen. Die Deklaration findet nur einmal am Anfang statt und hat die Form `deklariere <Typ> <Variable>`. 

Nach einer Deklaration bekommt jede Variable den Standardwert `nichts` (s.u.).

Beispiele:

```
Deklariere Ganzzahl Nummer und setze Nummer auf 5.

Deklariere Zeichenkette Begrüßung.
Setze Begrüßung auf "Hallo, Welt".
```

Für Zahlentypen (`Ganzzahl`, `Fließkommazahl`) gibt es noch zwei zusätzliche Zuweisungsmöglichkeiten:

```
Deklariere Ganzzahl x und setze x auf 1.
Erhöhe x um 1.
Verringere x um 1.
```

Dies ist äquivalent zu:

```
Deklariere die Ganzzahl x und setze x auf 1.
Setze x auf x + 1.
Setze x auf x - 1.
```

**Variablen können zu jedem Zeitpunkt einen bestimmten Artikel als Präfix und eine Angleichung zu einem bestimmten Fall erhalten, um grammatikalisch korrekte Sätze zu ermöglichen.**

Sollte ein Artikel bei der Deklaration genutzt werden, zählt dieser effektiv nicht mit zum Namen der Variable. Stattdessen wird der Nominativ aus den, dem Artikel folgenden, Wörtern gebildet und als Variablenname genutzt. Wird kein Artikel verwendet, so findet dies nicht statt. Auch in späteren Referenzen kann auf den Artikel verzichtet werden. Nur, wenn einer benutzt wird, wird der eigentliche Name aus der auf den Artikel folgenden Form rekonstruiert. Wird eine falsche Form oder ein falscher Artikel genutzt, gibt es einen Grammatikfehler.

**Potentielle Lösungen hierfür: OpenThesaurus Wörterbuch-Resource (bei Variablen mit mehreren Wörtern alle Wörter nutzen - Backticks ignorieren) // TODO**

Erstes Beispiel (mit Artikeln):

```
Deklariere die Ganzzahl Nummer und setze die Nummer auf 5.
Deklariere die Zeichenkette Begrüßung.

Setze die Begrüßung auf "Hallo, Welt".
```

Damit auch bei Angleichung immer noch die richtigen Variablen referenziert werden, wird über ein Wörterbuch nach dem passenden Wort für eine angeglichene Form gesucht. Sollte die Form trotz Artikel falsch sein, wird ein Grammatikfehler geworfen. Bei Variablen mit mehreren Wörtern werden die Formen aller Wörter überprüft. Dies kann umgangen werden, indem die ignorierten Teile in Backticks \` gesetzt werden.

Beispiel dafür:

```
Deklariere die Variable `ist_geeignet` als Wahrheitswert.
```

Nur das Wort "Variable" wird hier auf die entsprechende Grammatik überprüft. Dies ist besonders dann wichtig, wenn es ein Wort im deutschen gar nicht gibt.

# 3. Datentypen

In Kartoffelskript gibt es ein paar grundlegende Datentypen, die für Variablen genutzt werden können. Jede Variable und jeder Ausdruck hat einen dieser Datentypen. Alle Datentypen können per Umwandlung in einen anderen umgewandelt werden (s.u.).

Überall, wo Datentypen benutzt werden (beim Deklarieren oder Umwandeln) werden sie mit einem unbestimmten Artikel davor verwendet (ein, eine, einen).

## 3.1. Ganzzahl

Der Typ `Ganzzahl` (`eine Ganzzahl`) beschreibt einen signed Integer mit einer Größe von 32 Bit. Die Reichweite ist also -2^31 - 2^31 - 1. Er ist das Äquivalent zu `int` aus anderen Sprachen.

Auf Ausdrücke dieses Typens können die 5 arithmetischen Grundoperationen angewendet werden.

Direkte Ausdrücke (literal expressions) werden als einfache Zahl dargestellt. Für negative Zahlen muss davor ein `-` stehen. Da es sich um eine Ganzzahl handelt, sind Kommata nicht erlaubt.

Beispiel:

```
Deklariere x als eine Ganzzahl und setze x auf -12.
Setze x auf 765443.
```

## 3.2. Fließkommazahl

Der Typ `Fließkommazahl` beschreibt wie `Ganzzahl` eine 32-Bit große Zahl, nur, dass diese auch Kommazahlen ermöglicht. Er ist das Äquivalent zu `float` aus anderen Sprachen.

Auf Ausdrücke dieses Typens können die 5 arithmetischen Grundoperationen angewendet werden.

Direkte Ausdrücke werden entweder wie als Ganzzahl dargestellt oder im Falle einer Kommazahl mit einem Komma `,`. 

Beispiel:

```
Deklariere Pi als eine Fließkommazahl und setze Pi auf 3,14159.
```

## 3.3. Zeichen

Der Typ `Zeichen` beschreibt ein 16-Bit großes Zeichen. Er ist das Äquivalent zu `char` aus anderen Sprachen.

Direkte Ausdrücke werden in Hochkommata `'` eingeschlossen. Sie dürfen maximal ein Zeichen enthalten. Unicode wird unterstützt.

Beispiel:

```
Deklariere den Buchstaben als ein Zeichen und setze den Buchstaben auf 'X'.
```

## 3.4. Zeichenkette

Der Typ `Zeichenkette` ist das Äquivalent zu `string` aus anderen Sprachen.

Direkte Ausdrücke werden in Anführungszeichen `"` eingeschlossen. Zeichenketten können mit dem Operator `+` konkateniert werden.

Beispiel:

```
Deklariere das Grußwort als eine Zeichenkette und setze das Grußwort auf "Hallo".
Deklariere den Namen als eine Zeichenkette und setze den Namen auf "Johnny".

Deklariere die Begrüßung als eine Zeichenkette.
Setze die Begrüßung auf das Grußwort + ", " + den Namen.
```

Außerdem bieten Zeichenketten eine native Funktion. Die Zeichen einer Zeichenkette können mit dem Ausdruck `Zeichen in <Zeichenkette>`  erhalten werden. Die Rückgabe dieses Ausdrucks ist ein `Feld mit Zeichen-Werten`.

## 3.5 Wahrheitswert

Der Typ `Wahrheitswert` beschreibt einen simplen, binären Wert. Er ist das Äquivalent zu `boolean` oder `bool` aus anderen Sprachen.

Er kann nur einen von genau zwei Werten besitzen: `wahr` oder `falsch`. Außerdem können Werte dieses Typs direkt in Bedingungen für Kontrollstrukturen verwendet werden (dazu später mehr).

Beispiel:

```
Deklariere die Bedingung als einen Wahrheitswert und setze die Bedingung auf wahr.
```

# 4. Felder (Arrays)

Felder sind Ansammlungen fester Größe von Werten desselben Datentyps und das Äquivalent zu Arrays in anderen Sprachen.

Sie werden deklariert als `<Typ>-Feld`. Der Zugriff auf einzelne Elemente eines Feldes erfolgt über Indizes in der Form `Element <Index> aus <Feld>`. Dieser Ausdruck gibt einen Wert des Feld-Typen zurück oder verursacht einen Fehler, wenn der Index außerhalb der Grenzen des Feldes liegt.

Felder fangen bei 1 an, nicht bei 0 wie in anderen Sprachen.

Ein neues Feld wird so erzeugt: `ein neues Feld der Größe <Größe>`. Der Typ des Feldes wird inferiert. Die Größe gibt an, wie viele Elemente das Feld beinhaltet. Ein leeres Feld beinhaltet an jeder Position `nichts`.

So wird ein Feld erzeugt:

```
Deklariere das Array als ein Ganzzahl-Feld und setze das Array auf ein neues Feld der Größe 5.
```

So werden Werte eingetragen:

```
Setze das Element 1 aus dem Array auf -10.
Setze das Element 2 aus dem Array auf 42.
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

Alle Vergleiche nutzen das Wort `ist` in Kombination mit dem eigentlichen Operator. Dies wird später bei den Kontrollstrukturen wichtig.

### 6.1.1. (Un)gleichheit

Auf Gleich- und Ungleichheit wird mit den Operatoren `gleich` und `ungleich` geprüft.

```
Deklariere die Wahrheit als einen Wahrheitswert.
Setze die Wahrheit auf 5 ist gleich 5.
Setze die Wahrheit auf 3 ist ungleich 5.
```

Vorsicht: wenn es sich beim zweiten Operanden um eine Variable mit Artikel handelt, muss der Name der Variablen im Dativ stehen.

```
Deklariere den Namen als eine Zeichenkette und setze den Namen auf "Lena".
Deklariere die Variable `heißt_Lena` als einen Wahrheitswert und setze die Variable `heißt_Lena` auf "Lena" ist gleich dem Namen.
```

### 6.1.2. Größer als, kleiner als

Größer als hat in Kartoffelskript den Operator `größer als`, kleiner als den Operator `kleiner als`. Für inklusives < und > gibt es die Operatoren `kleiner oder gleich` und `größer oder gleich`.

```
Deklariere w als einen Wahrheitswert.
Setze w auf 4 ist kleiner oder gleich 5.
Setze w auf 5 ist größer als 10.
```

### 6.1.3. Boolesche Operationen

Boolesche Operationen in Kartoffelskript beschränken sich auf die Operatoren `oder` und `und`. Sie sind das Äquivalent zu `||` bzw. `&&` aus Java und werden auch genau so eingesetzt.

```
Deklariere w als einen Wahrheitswert.
Setze w auf wahr oder falsch. <-- w = wahr
Setze w auf wahr und falsch. <-- w = falsch
```

## 6.2. Arithmetische Operationen

### 6.2.1. Addition

Um die Summe zweier Zahlenwerte zu erhalten, wird der Additionsoperator `+` genutzt.

```
Setze die Summe auf 2 + 3.
```

### 6.2.2. Subtraktion

Um die Differenz zweier Zahlenwerte zu erhalten, wird der Subtraktionsoperator `-` genutzt.

```
Setze die Differenz auf 3 - 2.
```

### 6.2.3. Multiplikation

Um das Produkt zweier Zahlenwerte zu erhalten, wird der Multiplikationsoperator `⋅` (U+22C5) genutzt.

```
Setze das Produkt auf 2 ⋅ 3.
```

### 6.2.4. Division

Um den Quotienten zweier Zahlenwerte zu erhalten, wird der Divisionsoperator `:` genutzt.

Ist der Divisor des Ausdrucks = 0, so gibt es einen Fehler.

```
Setze den Quotienten auf 6 : 3.
```

### 6.2.5. Divisionsrest

Um den ganzzahligen Rest einer Division mit zwei Ganzzahlen zu erhalten, wird der Modulo-Operator `mod` genutzt.

```
Setze den Rest auf 10 mod 3.
```

## 6.3. Umwandlung

Wie bereits erwähnt, können die Datentypen `Ganzzahl`, `Fließkommazahl`, `Zeichen`, `Zeichenkette` und `Wahrheitswert` ineinander umgewandelt werden.

Umwandlungen irgendeines Typen in eine Zeichenkette umschließen den Wert als des Typen in einer Zeichenkette. Umgekehrt, um eine Zeichenkette in einen anderen Typen umzuwandeln, muss die Zeichenkette einem direkten, zu dem Typ passenden, Wert entsprechen.

Eine Umwandlung von `Ganzzahl` zu `Zeichen` oder `Fließkommazahl` ist immer möglich, umgekehrt gibt es bei `Fließkommazahl` zu `Ganzzahl` die Einschränkung, dass Nachkommastellen wegfallen.

Zum Umwandeln dient das Schlüsselwort `als`.

```
Deklariere die Zeichenkette Text und setze den Text auf "42".
Deklariere die Ganzzahl Zahl und setze die Zahl auf den Text als Ganzzahl.
```

Ob ein Wert in einen anderen umgewandelt werden kann, kann mit dem Operator `ist vom Typ` überprüft werden.

```
Deklariere den Wahrheitswert w, dann setze w auf "3" ist vom Typ Ganzzahl.
```


