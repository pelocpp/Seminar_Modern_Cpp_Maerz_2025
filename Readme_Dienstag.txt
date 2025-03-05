================================================

Modern C++

Dienstag

================================================


std::initializer_list<int>   ===> Stack

std::vector<int>             ===> Heap  (new, delete)

Wozu: �bergabe auf dem Stack: ist schneller

Beobachtung: Eine std::initializer_list<int> ist kein STL-Container.

Lightweight-Container: std::initializer_list<int>

begin(), end(), size().




Frage:

std::array      Daten auf dem Stack

C-Style Array:  Daten auf dem Stack

Genauer:

a) Globales Feld:            Daten in einem globalen Datensegment.

b) Lokales Feld:             Daten auf dem Stack.

c) Dynamisches Feld:         Daten auf dem Heap.

=================================================

int sum = adder ( { 1, 2, 3, 4, 5, 6, 7, 8 } );

2 Arten umsetzen oder realisieren:

a) static int adder ( std::vector<int> list )

   i) Stack: Vector-Objekt (klein) abgelegt // Nutzdaten auf dem Heap

b) static int adder ( std::initializer_list<int> list )

   ii) ALLES AUF DEM STACK: 8 * 4 = 32 Byte plus Verwaltungsdaten der initialisierungsliste

   Stack : Pro: Performanz gut
   Contra: Maximale Stacksize

Frage: ginge die Schnittstelle von Adder auch mit einem C-Style Array ???

Ja: Ginge, ist aber konzeptionell schlecht.

// Frage:

Elementare Variablen:

void tueWas (int n)

oder

void tueWas (int& n)


a)

Direkter Zugriff // Via Kopie

    m = n;
00007FF607CB18E6  mov         eax,dword ptr [n]  
00007FF607CB18EC  mov         dword ptr [m],eax  

b)

Indirekter Zugriff // Via Referenz

    m = n;
00007FF679F918E7  mov         rax,qword ptr [n]  
00007FF679F918EE  mov         eax,dword ptr [rax]  
00007FF679F918F0  mov         dword ptr [m],eax  

Fazit: W�rde elem. Variablen immer als Kopie �bergeben.

Ausnahme: M�chte eine Variable durch deren Referenz ver�ndern.

=================================================

Achtung:

std::vector<int> vec1{ 5 };   // Size: 1, Value: 5 
std::vector<int> vec2(5);     // Size: 5, Value: 0

=================================================

Frage: STL - Algorithmen


Was liefert begin() zur�ck ???

a) Iterator // Position

b) Ein Objekt (meistens), dass die Operatoren implementiert,
die ein Iterator implementieren muss.

operator*() // Dereferenzierung
operator++() // Inkrementierung
operator==() // Vergleich


=================================================

using: Die moderne Variante von typedef


=================================================

Container und INdex-Oparator []:

Wir nur von sequentiellen Containern unterst�tzt !!!!

Das sind wenige .............


=================================================

STL: Konzeption: klassisch

        std::for_each(
            values.begin(),
            values.end(),
            [](auto& elem) { elem = 123.0; }
        );

STL::Container (std::vector) 

II
II
II

STL::Iterator (begin(), end())

II
II
II

STL::Algorithmus (std::for_each)

Neu -- ab C++11:

range_based_for_loop

Das ist in anderen Sprachen ein for_each.

for (auto& elem : values)
{
    elem = 123.0;
}

Frage:

std::memcpy : Geht das ??????????????????????????????

vector  ==> 123.0 

=========================================

Smart Pointer:

Was ist das Problem mit new ???

Zu jedem new muss ein delete stehen.

a) Speicherleck

=========================================

Idee:

a) OO, Klassen und Objekte

b) Objekte: Konstruktor und Destruktor

c) Wann wird ein Destruktor aufgerufen ???

   1. Ende des Blocks  // deterministisch

   Geht das l�nger als die Lebensdaur des Blocks: Ja.
   
   
d) Was ist mit new und delete ???
   1. new:  Konstruktor
   2. delete: Destruktor

e) Welche Klasse ist das dann? ?? 

   Das sind H�llenklassen oder Wrapperklassen.

   std::unique_ptr<int> ptr = std::make_unique<int>(5);
   std::shared_ptr<int> ptr = std::make_shared<int>(5);


f) Die verschiedenen H�llenklassen haben verschiedene Strategien:

g) std::unique_ptr: 1 Besitzer

h) std::shared_ptr:  Mehrere Besitzer       

Zu g) Ein std::unique_ptr hat zu einem Zeitpunkt nur einen Besitzer.

Zu h) Ein std::shared_ptr hat zu einem Zeitpunkt einen oder mehrere Besitzer.

=========================================

Details:

=========================================

std::move bei return;

Antwort: NIEMALS !!!!!!!

Lass den Compiler entscheiden. // seine Arbeit machen.

=========================================

Z�sur:

Shared oder Unique: ???

a) Go-for-Unique: 1 Besitzer, wenn es geht.

  Kommt dem raw-Pointer am N�chsten.

b) Sonst Shared: Mehrere Besitzer.

Problem:  Geht nicht immer. !!!

L�sung:  std::weak_ptr.

Wann ben�tige ich den std::weak_ptr ????

=========================================


Frage: Observer-Pattern ????

Skizze:

a) Subject: Hier kann ein Ereignis eintreten.

b) Observer: Hier wird das Ereignis verarbeitet.

             Ein Observer interessiert sich f�r ein Ereignis.

c) Observer melden sich am Subject an.

d) Observer melden sich am Subject ab.

e) Ein Subject kennt seine Observer.

i) Das Subject: std::shared_ptr:   

ii) Observer: std::shared_ptr

iii) Im Subject gibt es eine Liste von Observern:

     Legen wir hier shared_ptr ab oder weak_ptr ab ???

     =======> weak_ptr !!!!!!!

Fazit:  std::shared_ptr oder std::weak_ptr ???

Antwort: So viel es geht weak_ptr !!!

Observer konkret:

https://github.com/pelocpp/cpp_design_patterns/tree/master/Patterns/Observer/Resources

=========================================

        constexpr Complex c3 = c1 + c2;
00007FF74FF09310  movss       xmm0,dword ptr [__real@40800000 (07FF75012E760h)]  
00007FF74FF09318  movss       dword ptr [c3],xmm0  
00007FF74FF09320  movss       xmm0,dword ptr [__real@40a00000 (07FF75012E764h)]  
00007FF74FF09328  movss       dword ptr [rbp+8Ch],xmm0  

float: IEEE 754

===

class X {};


X x;

X y = x;   // copy-c'tor  // KEINE WERTZUWEISUNG
// IDENTISCH ZU
X y (x);   // copy-c'tor
// IDENTISCH ZU
X y {x};   // copy-c'tor // Brace-Init.

C#:

class X
{
    void print();
}

X x();  // Valid C++ // Was ist x ???
        // x ist eine FUNKTION, die keine PArameter hat und ein Objekt X zur�ckliefert

Most vexing Parse

X x{};  // x ist ein Objekt, durch den Def. C'tor vorbelegt.

// besser:  X x = new X();   // C#

x.print();   // x ist kein Objekt
