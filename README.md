# PodstawyProgramowania2 (C++)

<img src="https://gitlab.com/marcinwolder/marcinwolder/-/raw/main/img/AGH-LOGO-ONLY.png" width="100px" align="left"></img>

<div>
  <br/>
  Repository for the subject "Podstawy Programowania 2" <br/>
  Lecturer: <b>Grzegorz Bazior</b>
</div>
<br/>
<br/>

---

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
Class(){};                      // konstruktor bezargumentowy
Class(const Class& c){};        // konstruktor kopiujący
Class(Class&& c) noexcept {};   // konstruktor przenoszący
~Class(){}                      // destruktor
virtual ~Class(){}              // destruktor wirtualny - pozwala na wykonanie się poprawnego destrukotra klas dziedziczących
```

##### kolejność wywołania konstruktorów:
1. konstruktor klasy bazowej
1. konstruktor klasy pochodnej
##### kolejność wywołania destruktorów:
1. konstruktor klasy pochodnej
1. konstruktor klasy bazowej
##### wywołanie metod z oraz bez `virtual`:
problem jedynie przy wskaźnikach `*`(też przy użyciu `dynamic_cast`), program zachowuje się normalnie gdy używamy typu `T`(też przy użyciu `static_cast`)
np.: `A* a = new B` oraz `void f()`, `virtual void f2()` w każdej z klas

1. (bez virtual): `a->f()` => `A::f()` (funkcja zależy od typu, działają cast'y)
2. (z virtual): `a->f2()` => `B::f2()` (funkcja zależy od skonstruowanego obiektu)

*tak samo działają destruktory - uruchamiają się albo od destruktora typu (bez virtual) albo od destruktora obiektu (z virtual)*

#### operatory:
```cpp
T& T::operator=(const T&){...; return this*}; // przypisania kopującego
T& T::operator=(T&&){...; return this*};      // przypisania przenoszącego
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

// Iterators:
begin() // Return iterator to beginning (public member function)
end()	// Return iterator to end (public member function)
rbegin()  // Return reverse iterator to reverse beginning (public member function)
rend()	// Return reverse iterator to reverse end (public member function)
cbegin()	// Return const_iterator to beginning (public member function)
cend()	// Return const_iterator to end (public member function)
crbegin()	// Return const_reverse_iterator to reverse beginning (public member function)
crend()	// Return const_reverse_iterator to reverse end (public member function)

// Capacity:
size()	// Return size (public member function)
max_size()	// Return maximum size (public member function)
resize(size_type n, value_type val)	// Change size (public member function)
capacity()	// Return size of allocated storage capacity (public member function)
empty()	// Test whether vector is empty (public member function)
reserve(size_type n)	// Request a change in capacity (public member function)
shrink_to_fit()	// Shrink to fit (public member function)

// Element access:
operator[](size_type n)	// Access element (public member function)
at(size_type n)	// Access element (public member function)
front()	// Access first element (public member function)
back()	// Access last element (public member function)
data()	// Access data (public member function)

// Modifiers:
assign(InputIterator first, InputIterator last) assign(size_type n, const value_type& val)	// Assign vector content (public member function)
push_back(const value_type& val)	// Add element at the end (public member function)
pop_back()	// Delete last element (public member function)
insert(iterator position, const value_type& val) insert(iterator position, size_type n, const value_type& val) insert(iterator position, InputIterator first, InputIterator last)	// Insert elements (public member function)
erase(iterator position) erase(iterator first, iterator last)	// Erase elements (public member function)
swap(vector& x)	// Swap content (public member function)
clear() // Clear content (public member function)
emplace(const_iterator position, Args&&... args)	// Construct and insert element (public member function)
emplace_back(Args&&... args)	// Construct and insert element at the end (public member function)
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
