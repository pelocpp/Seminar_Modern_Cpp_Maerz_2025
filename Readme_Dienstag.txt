================================================

Modern C++

Dienstag

================================================


std::initializer_list<int>   ===> Stack

std::vector<int>             ===> Heap  (new, delete)

Wozu: Übergabe auf dem Stack: ist schneller

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

Fazit: Würde elem. Variablen immer als Kopie übergeben.

Ausnahme: Möchte eine Variable durch deren Referenz verändern.

=================================================

Achtung:

std::vector<int> vec1{ 5 };   // Size: 1, Value: 5 
std::vector<int> vec2(5);     // Size: 5, Value: 0

=================================================

Frage: STL - Algorithmen


Was liefert begin() zurück ???

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

Wir nur von sequentiellen Containern unterstützt !!!!

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

   Geht das länger als die Lebensdaur des Blocks: Ja.
   
   
d) Was ist mit new und delete ???
   1. new:  Konstruktor
   2. delete: Destruktor

e) Welche Klasse ist das dann? ?? 

   Das sind Hüllenklassen oder Wrapperklassen.

   std::unique_ptr<int> ptr = std::make_unique<int>(5);
   std::shared_ptr<int> ptr = std::make_shared<int>(5);


f) Die verschiedenen Hüllenklassen haben verschiedene Strategien:

g) std::unique_ptr: 1 Besitzer

h) std::shared_ptr:  Mehrere Besitzer       

Zu g) Ein std::unique_ptr hat zu einem Zeitpunkt nur einen Besitzer.

Zu h) Ein std::shared_ptr hat zu einem Zeitpunkt einen oder mehrere Besitzer.

=========================================

Details: