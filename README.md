# Podstawy programowania 2 (C++)

### `class` :

```cpp
class Example: public Example_Parent { //dziedziczenie
    int var1; //zmienna prywatna
    int &arr; //referencja

    public:
    int var2; //zmienna publiczna
    inline static int var3 = 0; //zmienna statycznna
    const int var4; //zmienna stała

    Example(int var, int &arr): arr(arr), var4(var) { //lista inicjacyjna - definicja zmiennych statycznych, stałych, referencji i konstruktorów
        //konstruktor
    }
    Example(int var1, int var2, int &arr): Example(var1+var2, arr) {
        //konstruktor z przekazaniem do konstruktora wyżej
    } 
    ~Example(){
        //destruktor
    }
    int getVar1() const { //zmienne które nie powinny zostać zmieniane powinny być zwracane jako const
        return var1;
    }
}

int Example::var3 = 0; //inny sposób inicjalizacji zmiennej statycznej

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