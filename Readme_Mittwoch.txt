================================================

Modern C++

Mittwoch

================================================

Literale // Konstanten

123

123l

123ll

123.456f

100_km

100_euro

0xFF00FF_color

Konstante:

a) WERT

b) ZEICHENKETTE

"05.03.2025"_date

Bauteil:

"hersteller:name:nummer"_bauteil

==> operator ""   (const char* literal)
  
Geht !!!

Programmiersprache:  Lexikon

C++ ist erweiterbar: Ben. def. Literal

Wie:   operator ""  :  Literal Operator

C ++ Syntax:   ... operator ""  _suffix  (params)

 _suffix = _euro, _km, _pfund, ....


0xFF00FF_rgb  ===>  Wert des Literals: Objekt 

class Color

Technologische Konstanten

Klasse: Member:

int m_age;

m_age = 18_age;

Bessere Lesbarkeit.

================================================

int result = func();

Gültiges Ergebnis ???

result : 0 

-1 

-MAX_INT

Perfekte Lösung:

int  result;
bool isValid;    ===> std::optional

C#:  int?  result;

// ====================================

Graphiksystem:

3-D Koordinaten

class 3DPoint
{
    int m_x;
    int m_y;
    int m_z;
    ....
}

3DPoint point;

if (point.m_x == ....)

Alternative:

std::tuple<int, int, int> point;

std::pair<int, int> 2d_point;


int x = std::get<0>(point);

// Structured Binding <====== Namen für die Elemente

Was ist der Unterschied von einem Tuple und einer Struktur ???

Ein Tuple ist eine Struktur für Schreibfaule :)

Wie kann ein Tuple realisiert werden:

https://eli.thegreenplace.net/2014/variadic-templates-in-c


=========================================================

std::variant

Was ist ein variant ???

Ein Variant kann mehrere Werte unterschiedlichen Typs aufnehmen :

Zu einem Zeitpunkt aber nur EINEN Wert !!!

Beispiel:

EXCEL // Google Sheets:    Zelle // Cell

Cell:  Zeichenkette, num. Wert (ganze Zahl, Kommawert), Datum, Currency

Wo legt ein Variant seine Daten ab ????????

Weird:

a) Kleinen Daten zu tun: Im Objekt selbst (häufig: Stack)

b) Großen Daten zu tun: Nicht im Objekt (häufig: Heap)

c) Wie geht ein Variant mit unterschiedlichen Daten unterschiedlichen Typs um ???

Type Erasure:

std::function   // Lambda, freie FUnktion, Member Methode , aufrufbares Objekt

std::variant

std::any

Man kann einen variant "besuchen"

            if ( std::is_same<ElemTypeWithOutRefAndConst, int>::value == true ) {
00007FF73E5AE146  xor         eax,eax  // eax auf Null !!
00007FF73E5AE148  cmp         eax,1    // Vergleicht eax mit 1
00007FF73E5AE14B  je          `VariantDemo::test_03'::`2'::<lambda_1>::operator()<int>+7Ah (07FF73E5AE19Ah)  

Ab C++ 17:

if Anweisung für den Übersetzer

Modern C++:

Generische Programmierung

Programmierung mit Datentypen

Type Traits: C++ 11

auto visitor = [] (const auto& elem) { }

a) Classic C++:

visit (const int& elem) { }   // KONKRETER TYP

b) Modern C++:

visit (const auto& elem) { }   // KANN ALLES SEIN

c) Kann  man "KANN ALLES SEIN" auf das einschränken, was ich brauche ???

i)   .... std::is_same ....    if constexpr  

ii)  concepts und requires ...

d) Templates ... hmmm

===> ABER: Mit generischen Funktionen ( Parameter vom Typ auto) siehst du das "Template" nicht mehr

===========

int, long, size_t  

float, double ...

Wahlfreiheit: template  ... generischen Funktionen   ... no Overhead

C++:   Bjarne Stroustrup

========================================================

C++ 11:

Variadische Templates

a) Kennen lernen

------------------------------------

b) Why ??????????????????

Zum Transport von Daten von A nach B

i) Von einem Methodenaufruf zu einem Konstruktoraufruf: zB make_unique

ii) Zur Anwendung der emplace-Technik

iii) Um einen Thread-Prozedur mit Parametern zu versorgen (std::thread)

------------------------------------

C) selber mal ein var. Template

Fragen: Was ist "m"

m ist ein "Pack": 

Verständnis:

i) Debugger

ii) Cpp Insights

=========================================

Wer könnte No-throw-Garantie (No-throw guarantee) versprechen:

Methoden, die nur aus Wertzuweisungen bestehen ;)

Beispiel: Ein Move-Konstruktor

Was kann ein new - Aufruf bedeuten:  bad_alloc Exception 

Was ist stack Unwinding:

Eine Ausnahme wird NICHT gefangen (try ... catch)
 ==> Es wird die Ausnahme an die rufende Methode durchgeschleust.