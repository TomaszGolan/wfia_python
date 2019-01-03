% Języki skryptowe Python
% Wykład 12

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

# 

## Na ostatnim wykładzie

---

* klasy pozwalają na definiowanie własnych typów
* funkcje specjalne - definiowanie działania operatorów lub wywołań funkcji wbudowanych (*print*, *len*...)
* nie ma "pełnej prywatności"

## Konwencja *self*

---

* pierwszym argumentem każdej metody jest wskaźnik na obiekt
* przyjęto nazywać ten argument *self* (choć nic nie stoi na przeszkodzie, żeby używać innej nazwy)

## *self* test

---

```python
class Foo:
    
    def moja_metoda():  # błąd
        pass
```

```python
x = Foo()
x.moja_metoda()
# bo x jest pierwszym argumentem pozycyjnym!
```

```bash
TypeError: moja_metoda() takes 0 positional arguments but 1 was given
```

## Funkcja globalna

---

```python
class Foo:
    
    def __init__(self):  # "konstruktor"
        self.bar = False
        
    def __str__(self):   # print
        return "Foobar = {}".format(self.bar)
    
def funkcja(obiekt):     # funkcja globalna
    obiekt.bar = True    # ustaw flagę bar
```

```python
x = Foo()   # stwórz obiekt typu Foo

print(x)

funkcja(x)  # globalna na x

print(x)
```

```bash
Foobar = False
Foobar = True
```

## Metoda z funkcji globalnej

---


```python
class Foo:
    
    def __init__(self):    # "konstruktor"
        self.bar = False
        
    def __str__(self):     # print
        return "Foobar = {}".format(self.bar)
    
    def funkcja(obiekt):   # metoda
        obiekt.bar = True  # ustaw flagę bar
```

```python
x = Foo()    # stwórz obiekt typu Foo

print(x)

x.funkcja()  # metoda (x jest arg pozycyjnym)

print(x)
```

```bash
Foobar = False
Foobar = True
```

#

## Klasa student

---

* imię, nazwisko, nr indeksu
* zliczanie studentów (wspólna zmienna dla wszystkich obiektów danej klasy)

## Atrybuty klasy

---

* zmienne wprowadzane poza `__init__` są traktowane jako atrybuty klasy, a nie obiektu


```python
class Student:
    counter = 0  # licznik studentów
    
    def __init__(self, imie, nazwisko, indeks):
        self.__class__.counter += 1
        self.imie = imie
        self.naziwsko = nazwisko
        self.indeks = indeks
```

## Studenci

---


```python
student1 = Student("Jan", "Kowalski", 1234)
student2 = Student("Anna", "Nowak", 1234)

# każdy student ma swoje imię
print(student1.imie, student2.imie)
```

```bash
Jan Anna
```

```python
# ale licznik jest wspólny
# dla wszystkich obiektów klasy Student
print(student1.counter, student2.counter)
```

```bash
2 2
```

#

## Punkt

---

```python
class Punkt:
    
    def __init__(self, x=0.0, y=0.0):
        self.x = x  # odcięta 
        self.y = y  # rzędna
        
    def __str__(self):  # (x, y)
        return "({}, {})".format(self.x, self.y)
```


```python
x = Punkt(1.0, 2.0) 

print(x)
```

```bash
(1.0, 2.0)
```

## Odcinek

---

```python
from math import sqrt

class Odcinek:
    
    def __init__(self, start, end):
        self.poczatek = start  # Punkt
        self.koniec = end      # Punkt
        
    def dlugosc(self):
        # Odcinek.Punkt.Wspolrzedna
        x = self.koniec.x - self.poczatek.x
        y = self.koniec.y - self.poczatek.y
        return sqrt(x**2 + y**2)
```

```python
a = Punkt()   # (0, 0)
b = Punkt(2)  # (2, 0)
o = Odcinek(a, b)

o.dlugosc()
```

```bash
2.0
```

#

## Enkapsulacja

---

* enkapsulacja - ukrywanie implementacji
* brak bezpośredniego dostępu do danych
* tylko własne metody moga zmienić stan
* w Pythonie jest to umowne, bo nie ma zmiennych prywatnych

## Przykład - cząstka

---

```python
class Particle:
    
    def __init__(self, mass, velocity=0.0):
        self.m = mass      # masa
        self.v = velocity  # prędkość
        self.ped()         # ustala pęd

    def __str__(self):
        return "m = {m}, v = {v}, p = {p}"\
                .format(m=self.m, v=self.v, p=self.p)
        
    def ped(self):         # liczy pęd cząstki
        self.p = self.m*self.v
```

## Cząstka - test

---

```python
x = Particle(10, 10)  # masa = 10, prędkość = 10

print(x)              # pęd = masa * prędkość
```

```bash
m = 10, v = 10, p = 100
```

```python
x.v = 0   # zmień prędkość

print(x)  # pęd nie został uaktulaniony
```

```bash
m = 10, v = 0, p = 100
```

## *Gettery* i *settery*

---

```python
class Particle:
    
    def __init__(self, mass, velocity=0.0):
        self.__m = mass      # masa
        self.__v = velocity  # prędkość
        self.ped()           # ustala pęd
        
    def __str__(self):
        return "m = {m}, v = {v}, p = {p}"\
                .format(m=self.__m, v=self.__v, p=self.__p)
        
    def ped(self):       # liczy pęd cząstki
        self.__p = self.__m*self.__v
        
    def get_v(self):     # pobierz prędkośc
        return self.__v
    
    def set_v(self, v):  # ustaw prędkość
        self.__v = v
        self.ped()       # aktualizuj pęd
```

## *get*, *set* - test

---

```python
x = Particle(10, 10)  # masa = 10, prędkość = 10

print(x)
```

```bash
m = 10, v = 10, p = 100
```


```python
x.set_v(0)  # zmień prędkość

print(x)    # pęd został uaktulaniony
```

```bash
m = 10, v = 0, p = 0
```

```python
x.get_v()  # pobierz prędkość
```

```bash
0
```

#

## Ciąg arytmetyczny

---

* zadany przez pierwszy wyraz ciągu i różnicę
* przechowuje *n* pierwszych wyrazów ciągu
* *len(ciąg)* zwraca *n*
* *sum(ciąg)* zwraca sumę *n* wyrazów

## Ciąg arytmetyczny: *init*

---

```python
# arciag.py

class ArCiag:
    """Ciąg arytmetyczny"""
    
    def __init__(self, a1, r, n=1):
        """Inicjuje ciąg arytmetyczny
        
        a1 -- pierwszy wyraz ciągu
        r -- różnica
        n -- początkowa liczba wyrazów
        """
        
        self.__a1 = a1
        self.__r = r
        self.__wyrazy = [a1]
        
        if n > 1:
            self.generate(n - 1)
```

## Ciąg arytmetyczny: *str*

---

```python

    def __str__(self):
        s = "Ciąg arytmetyczny ({a1}, {r}):".format(a1=self.__a1, r=self.__r)
        
        for wyraz in self:  # skąd wie, jak po sobie iterować?
            s += " " + str(wyraz)
            
        return s
```

## Ciąg arytmetyczny: *iter*

---


```python

    def __iter__(self):  # iterator ciągu
        """Umożliwia iterację po ciągu"""
        
        for a in self.__wyrazy:
            yield a
```

## Ciąg arytmetyczny: *len*

---

```python

    def __len__(self):  # wywoływana przez len()
        """Zwraca ilość wyrazów ciągu"""
        
        return len(self.__wyrazy)
```

## Ciąg arytmetyczny: *generate*

---


```python

    def generate(self, n):
        """Generuje kolejne wyrazy ciągu"""
        
        for _ in range(n):
            self.__wyrazy.append(self.__wyrazy[-1] + self.__r)
```

## Ciąg arytmetyczny: *save*

---


```python

    def save(self, filename):
        """Zapisuje ciąg do pliku"""
        
        with open(filename, 'w') as f:
            f.write(self.__str__())
```

## Ciąg arytmeytczny: dokumentacja

---


```python
from arciag import ArCiag

help(ArCiag)
```

```bash
Help on class ArCiag in module arciag:

class ArCiag(builtins.object)
    |  Ciąg arytmetyczny
    |  
    |  Methods defined here:
    |  
    |  __init__(self, a1, r, n=1)
    |      Inicjuje ciąg arytmetyczny
    |      
    |      a1 -- pierwszy wyraz ciągu
    |      r -- różnica
    |      n -- początkowa liczba wyrazów
    |  
    |  __iter__(self)
    |      Umożliwia iterację po ciągu
    |  
    |  __len__(self)
    |      Zwraca ilość wyrazów ciągu
    |  
    |  __str__(self)
    |      Return str(self).
    |  
    |  generate(self, n)
    |      Generuje kolejne wyrazy ciągu
    |  
    |  save(self, filename)
    |      Zapisuje ciąg do pliku
    |  
    |  ----------------------------------------------------------------------
    |  Data descriptors defined here:
    |  
    |  __dict__
    |      dictionary for instance variables (if defined)
    |  
    |  __weakref__
    |      list of weak references to the object (if defined)
```    

## Ciąg arytmetyczny: test

---


```python
from arciag import ArCiag

x = ArCiag(1, 2)      # domyślnie jeden wyraz
y = ArCiag(2, 3, 10)  # zacznij od 10 wyrazów

print(x)
print(y)
```

```
Ciąg arytmetyczny (1, 2): 1
Ciąg arytmetyczny (2, 3): 2 5 8 11 14 17 20 23 26 29
```

## Ciąg arytmetyczny: *len* i *sum*

---


```python
from arciag import ArCiag

x = ArCiag(1, 2)  # domyślnie 1 wyraz

x.generate(10)    # generuj kolejne 10

print(x)
```

```bash
Ciąg arytmetyczny (1, 2): 1 3 5 7 9 11 13 15 17 19 21
```

```python
len(x)  # ilość wyrazów (dzięki __len__)
```

```bash
11
```

```python
sum(x)  # suma wyrazów (dzięki __iter__)
```

```bash
121
```

## Ciąg arytmetyczny: zapis

```python
from arciag import ArCiag

x = ArCiag(1, 2, 10)    # generuj 10 wyrazów

x.save('moj_ciag.txt')  # i zapisz do pliku
```

```bash
$ cat moj_ciag.txt
```

```bash
Ciąg arytmetyczny (1, 2): 1 3 5 7 9 11 13 15 17 19
```

## Ciąg geometryczny

---

* gdybyśmy chcieli stworzyć analogiczną klasę dla ciągu geometrycznego, to różnica pojawiłaby się tylko w funkcji `generate`
* istnieje mechanizm, który umożliwia klasom posiadanie wspólnych metod

#

## Dziedziczenie

---

* umożliwia ponowne wykorzystanie funkcjonalności *klas bazowych* w *klasach pochodnych*
* przykład:
    * klasa pojazd: jedz, hamuj...
    * klasa samochód: to co pojazd + otwórz bagażnik...
    * klasa motor: to co pojazd + jedz na jednym kole...

## Przykład

---

```python
class Baza:
    
    def whoami(self):
        print("Jestem obiektem klasy Baza.")
        
class Pochodna(Baza):  # dziedziczy z Baza
    
    def sayhi(self):
        print("Hello!")
```

```python
x = Pochodna()

x.sayhi()   # zdefiniowane w Pochodna
```

```bash
Hello!
```

```python
x.whoami()  # zdefiinowane w Baza
```

```bash
Jestem obiektem klasy Baza.
```

## Konstruktor klasy bazowej

---

```python
class Foo:
    
    def __init__(self):
        print("Tworzę Foo")
        
class Bar(Foo):
    
    def __init__(self):
        print("Tworzę Bar")
```


```python
x = Bar()  # __init__ z Foo nie jest wywołany
```

```bash
Tworzę Bar
```

## Wywołanie konstruktora bazy

---


```python
class Foo:
    
    def __init__(self):
        print("Tworzę Foo")
        
class Bar(Foo):
    
    def __init__(self):
        super().__init__()  # wywołaj konstruktor klasy nadrzędnej
        print("Tworzę Bar")
```


```python
x = Bar()
```

```bash
Tworzę Foo
Tworzę Bar
```

#

## Przykład - Student

---


```python
class Student:
    
    last_index = 1234  # atrybut klasy
    
    def __init__(self, name):
        # aktualizuj numer indeksu
        self.__class__.last_index += 1
        # przypisz studentowi imię i numer indeksu
        self.name = name
        self.index = self.__class__.last_index
        
    def __str__(self):  # Student [imię] (nr indeksu)
        return "Student {} (nr {})".format(self.name, self.index)
```


```python
student = Student("Anna")

print(student)
```

```bash
Student Anna (nr 1235)
```

## Przykład - StudentISSP

---

```python
class StudentISSP(Student):  # też Student
    
    def __init__(self, name, przedmioty):
        
        super().__init__(name)  # wywołaj Student.__init__
        
        self.przedmioty = przedmioty
        
    def __str__(self):
        return super().__str__() + \
                ": " + ", ".join(self.przedmioty)
```


```python
studentISSP = StudentISSP("Jan", ["programowanie", "fizyka"])

print(studentISSP)
```

```bash
Student Jan (nr 1236): programowanie, fizyka
```


