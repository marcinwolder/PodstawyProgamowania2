# Podstawy programowania 2 (C++)

### klasy:

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
}

```
