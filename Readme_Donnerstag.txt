================================================

Modern C++

Donnerstag

================================================

std::array
vs.
C-Style Array:

Funktionalität: FIXED-Size Array     (std::vector)

Was sollten wir verwenden ???

Go for std::array

a) size()

b) Index out of Range:

   Kann geprüft werden:

   i)   array[n] = 123;       // KEIN INDEX CHECK
   ii)  array.at(n) = 123;    // MIT INDEX CHECK


=====================================

std::string

std::string_view


Frage:

const char* langeZeichenkette = "11111111111111111111111111111111111111111111111111111";

// std::string langeZeichenkette = "11111111111111111111111111111111111111111111111111111";

a) Möglich: .text == Code Segment

   Möglich: .data == Datensegment (initialisiert)

==> Will ich alle Zeichenkette auf dem Heap haben ????????????????

    Nein.

3. Option:

std::string_view langeZeichenkette = "11111111111111111111111111111111111111111111111111111";

Wo liegt diese Zeichenkette im Speicher ???

Antwort: Siehe a) 

Was ist ein std::string_view  ?? Ein Span für Zeichenketten:

i)  Die Anfangsadresse
ii) Die Länge

==============================================================================

String Pool: C++

Verhindern von Duplikaten

Java // C#:   Konstante Zeichenkette wiederverwenden.

Java: Class String immutable

==============================================================================

All-In von mehreren Konzepten:

std::variant

std::vector<T>:  Homogener Container  /// Alle Elemente sind vom selben Typ

std::vector mit std::variant:  Heterogener Container :)

Templates

virtual, override ...

Vergleich (Performanzbetrachtung) von statischem Polymorphismus (Templates) mit dynamischem Polymorphismus (virtueller Methodenaufrufmechanismus)

Beispiel „Buchhandlung”

==> Type Erasure

=============================================================

Virtueller Basisklassendestruktor

=============================================================

1. Ansatz:

virtueller Methodenaufruf  // klassische Umsetzung mit Vererbung

Bashing: der virtueller Methodenaufruf ist schlecht.

Performanz  // Laufzeit

2. Ansatz:

kein virtueller Methodenaufruf  // keine Vererbung

Klasse Bookstore

class Bookstore

a) Vererbung:  std::vector von Interface-Zeigern

b) Ohne Vererbung: Beliebige Klassen (die ein Konzept akzeptieren)

   Wie kommen diese Klassen (Datentypen)
   mit der Klasse Bookstore in Kontakt / in Berührung ??

Statisches Konzept  // Übersetzungszeit

i) Klasse, deren Container mit Template - Parametern definiert werden.

ii) std::vector von std::variant

iii) Besucher // std::visit

KEINE Virtuellen Methoden (Vorteil)

ABER (Nachteil): Die Klasse std::variant kann den Heap verwenden.

Ist am Ende die Laufzeit besser: Depends.

iv) Die beteiligten Klassen stehen NICHT in einer Hierarchie von Klassen

v) ABER: Die beteiligten Klassen kann man mit Concept // Requires auch bzgl.
   bestimmter Regeln beschreiben (Vorhandensein von Methoden)

INTERESSANT: KEIN HIERARCHIE.  // Starre Kopplung

"not implemented"  smell // wrong design

Lose Kopplung

========================================================================

Ein weiterer Ansatz: Polymorphismus, aber zur Übersetzungszeit

===> CRTP    C = Curious

===> Performanz

"Ein kurioses Pattern":  Gebrauchsanweisung.


=========================================================================

Folding  // Falten 

Wozu gibt es Folding:

Um die wiederholte Anwendung eines Operators EFFIZIENT auf MC abbilden zu können:

int n = 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8;

Matrizen: 

Syntax: Grausam.




================================================

"printf is back"

Ist mehr println von C#
