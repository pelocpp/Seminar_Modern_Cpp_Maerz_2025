Modern C++

Peter Loos

Dev. // Schulung

C/C++ Java  C#  JavaScript Android (Java) ( Python )

Back-to-the-Roots: C/C++

Guten Morgen

== Visual Studio 2022

== Github

Vorstellungsrunde:

= Was sind meine Erwartungen

= Was muss DRIN sein

= Benötige einen Überblick über alles "Moderne"

= Mein Background: Welche Sprachen

=============================================

9  => 17 Uhr

Kantine:  12.30

caaaaaa. 10.30 // 15.00

=============================================

Lambdas , Templates , MT, alles Neue

gut strukturierter Kurs  

C => C++:   OO  Klasse ....

DRY  Don't repeat yourself 

emplace

=============================================

C# versus C++:

A) C#:   Referenz-Semantik

B) C++:  Value-Semantik
         Referenz-Semantik

class Time{}

void tueWas ()
{
    Time now;                // C++ // Stack

    Time now =  new Time();  // C# // now: Referenz

    Time* now = new Time();  // C++ // Heap
    delete now;
}

===========================

Begriff der Referenz:

Oberflächlich:  Adresse

C#:   ==> new // Halde // Exakt: Doppel-Zeiger: Stub => Heap

C++:  ==> Ist ein Aliasname eines vorhandenen Objekts (Variable)

          Intern: Durch die Adresse des Originalobjekts //
                                    des referenzierten Objekts

C-Level:

a = 123;
a = b;

lvalue:  left value   // Adresse
rvalue:  right value  // Wert


=============================================================

:--: ... BE0   // Original  // anonym. Objekt am Stack // tmp. Objekt  // wird freigegeben
:--: ... 120   // Kopie im Vektor

:--: ... A50

=============================================================

Why auto vor Funktionen ???

Welches Paradigma ist in C++ gegeben ???

OO: Objektorientierung
GP: Great Performanz

GP: Generische Programmierung (Templates)

    Alexander Alexandrowitsch Stepanow // Stroustrup ==> Bibliothek: STL

"Mit Typen rechnen"  ==> Metaprogramming

=============================================================

explicit

=============================================================

Lambda

Historisch:

a) Mit free function

b) Aufrufbares Objekt // Callable Object // Funktor

=============================================================

Cpp Insights:

https://cppinsights.io/