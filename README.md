# Podstawy programowania 2 (C++)

### modyfikatory:

#### zmiennych:

```cpp
const Type var;        // brak możliwości zmiany wartości  
mutable Type var;      // możliwość zmiany w funkcjach *const*  
static Type var;       // zmienna wspólna dla całej klasy  
inline Type var = 10;  // inicjalizacja w miejscu  
```

#### motod:
```cpp
[[nodiscard]] Type func() const {}; // funkcja, nie zmieniająca wartości klasy
virtual Type func()=0;              // funkcja, która musi zostać przedefiniowana w klasach pochodnych
virtual Type func(){};              // funkcja, która może zostać przedefiniowana w klasach pochodnych
Type func() override {};            // funkcja, która musi zostać zdefiniowana w klasie bazowej
explicit Type func(){};             // funkcja, bez niejawnej tranformacji argumentów (np. string -> char*)
Type(Type&& var) noexcept {};       // przy konstruktorze przenoszącym
friend T func(){};                  // zaprzyjaźniona metoda (globalnie lub zakresowo) ma dostęp do składowych private i protected
```
#### klas:
```cpp
class B: public A {};       // dziedziczenie publiczne
class B: protected A {};    // dziedziczenie chronione
class B: private A {};      // dziedziczenie prywatne
class B: virtual A {};      // dziedziczenie wirtualne - wartości A są wspólne dla wszystkich dziedziczących
class A final {};           // klasa finalna - brak możliwości dziedziczenia tej klasy
```

### `class` :

```cpp
class Example: public Example_Parent { //dziedziczenie
    int var1; //zmienna prywatna
    int &arr; //referencja

    public:
    int var2; //zmienna publiczna
    inline static int var3 = 0; //zmienna statycznna
    const int var4; //zmienna stała
    mutable int var5; //zmienna modyfikowalna

    Example(int var, int &arr): arr(arr), var4(var) { //lista inicjacyjna - definicja zmiennych statycznych, stałych, referencji i konstruktorów
        //konstruktor
    }
    Example(int var1, int var2, int &arr): Example(var1+var2, arr) {
        //konstruktor z przekazaniem do konstruktora wyżej
    }
    ~Example(){
        //destruktor
    }
    int getVar1() const { //funkcja const - nie zmieniająca wartości w klasie
        this->var5 = 7; //jedyna dozwolona zmiana w funkcji const to zmiana na wartości `mutable`
        return var1;
    }
}

int Example::var3 = 0; //inny sposób inicjalizacji zmiennej statycznej

```

#### konstruktory:
```cpp
Class(){};                          // konstruktor bezargumentowy
Class Class(const Class& c){};      // konstruktor kopiujący
Class Class(Class&& c) noexcept {}; // konstruktor przenoszący
~Class(){}                          // destruktor
virtual ~Class(){}                  // destruktor wirtualny - pozwala na wykonanie się poprawnego destrukotra klas dziedziczących
```

##### kolejność wywołania konstruktorów:
1. konstruktor klasy bazowej
1. konstruktor klasy pochodnej
##### kolejność wywołania destruktorów:
1. konstruktor klasy pochodnej
1. konstruktor klasy bazowej

#### operatory:
```cpp
T& T::operator=(const T&){}; // przypisania
T operator()(args){}         // operator wywołania funkcyjnego
T operator[](int){}          // operator dostępu indeksowego
T& operator++(){}            // operator pre-inkrementacji
T operator++(int){}          // operator post-inkrementacji

friend ostream& operator<<(ostream& os, const T&){}; // operator wyjścia na stumień
friend istream& operator>>(istream& is, T&){};       // operator wejścia ze stumienia
```

### biblioteka `std::` :

#### `std::vector<T>` :

```cpp
#include <vector>

std::vector<T> v;

v.assign()  // Usuwa wszystkie istniejące elementy z kontenera, a następnie kopiuje wskazane elementy do kontenera.
v.swap()	// Kontenery vector zamieniają się posiadanymi danymi.
v.insert()	// Wstawia jeden element lub wiele elementów do kontenera vector na określonej pozycji.
v.push_back()	// Dodaje nowy element na końcu kontenera vector.
v.emplace_back()    // Przekazuje argumenty do konstuktura klasy T i dodaje nowy element na końcu kontenera vector.

v.clear()	// Usuwa wszystkie elementy z kontenera vector.
v.erase()	// Usuwa jeden element lub wiele elementów z kontenera vector występujących na podanej pozycji lub w podanym zakresie.
v.pop_back()	// Usuwa jeden element z kontenera vector, znajdujący się na jego końcu.

v.at()  // Zwraca referencję na element, który znajduje się na podanej pozycji w kontenerze » standard C++ ♦ vector.
v.front()	// Zwraca referencję na pierwszy element w kontenerze.
v.back()	// Zwraca referencję na ostatni element w kontenerze.

v.begin()	// Zwraca iterator wskazujący na pierwszy element.
v.end()	// Zwraca iterator wskazujący na element będący za ostatnim elementem.
v.rbegin()	// Zwraca iterator odwrotny wskazujący na ostatni element.
v.rend()	// Zwraca iterator odwrotny wskazujący na element występujący bezpośrednio przed pierwszym elementem.

v.reserve()	// Rezerwuje tyle miejsca w kontenerze, żeby pomieściła się wskazana liczba elementów bez konieczności wykonywania dodatkowej realokacji pamięci przy ich dodawaniu.
v.resize()	// Ustawia nowy rozmiar kontenera vector.

v.capacity()	// Zwraca maksymalną liczbę elementów jaką może pomieścić kontener bez wykonywania realokacji pamięci.
v.empty()	// Sprawdza czy kontener jest pusty.
v.max_size()	// Maksymalna możliwa długość tablicy kontenera » standard C++ ♦ vector, wyrażona w liczbie elementów.
v.size()	// Zwraca liczbę elementów znajdujących się aktualnie w kontenerze.
```

#### `std::string` :

```cpp
#include <string>

std::string s;

s.length()  // Zwraca długość tekstu.
s.reserve() // Zmienia rozmiary bufora.
s.resize()  // Zmienia rozmiar tablicy - w razie potrzeby wypełnia nowe miejsca podanym znakiem.
s.c_str()	// Zwraca łańcuch znaków tylko do odczytu w standardzie języka C.
s.find()	// Wyszukuje pierwszego wystąpienia danego łańcucha znaków.
s.substr()	// Zwraca podciąg łańcucha znaków.
s.erase()	// Usuwa część stringa.
s.insert()	// Wstawia znaki do aktualnego łańcucha znaków.
s.replace()	// Zamienia część znaków na inne.
```

#### `std::list` :

```cpp
#include <list>

std::list<T> l;

l.insert()  //
l.emplace() //
l.push_back()   //
l.emplace_back()    //
l.push_front()  //
l.emplace_front()   //

l.clear()   //
l.erase()   //
l.pop_back()     //
l.pop_front()   //

l.resize()  //
l.swap()    //

l.merge()   //
l.splice()  //
l.reverse() //
l.unique()  //
l.sort()    //
```

#### `std::map` :

```cpp
#include <map>

std::map<T,G> m;

m.insert(std::map<T,G>::value_type(val1,val2));
m.insert(std::pair<T,G>(val1,val2));
m.emplace(val1,val2);
```

#### `std::set` :

```cpp
#include <set>

std::set<T> s;

s.insert()  // Dodaje element.
s.empty()   // Testuje czy zbiór jest pusty.
s.find()    // Znajduje element w zbiorze.
```

#### `std::stringstream`

#### `std::lower_bound`

#### `std::upper_bound`
