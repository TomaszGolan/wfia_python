% Języki skryptowe Python
% Wykład 11

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

# 

## Programowanie strukturalne

---

* sekwencje (ciąg instrukcji)
* wybór (*if*)
* iteracja (pętle *for* i *while*)
* funkcje

## Słownik

---

* OOP - *Object-Oriented Programming*
* klasa - definicja obiektu
* instanacja (klasy) - obiekt utworzony na podstawie klasy

## Klasy

---

<div class="tree">
<ul>
<li><p>Klasa</p>
<ul>
<li><p>Atrybuty</p>
<ul>
<li><p>Dane</p>
<li><p>Metody</p>
</ul> 
</ul>
</ul>
</div>

## Przykład - klasa *complex*

---

<div class="tree">
<ul>
<li><p>complex</p>
<ul>
<li><p>Dane:</p>
<ul>
<li><p>real</p>
<li><p>imag</p>
</ul>
<li><p>Metody:</p>
<ul>
<li><p>conjugate</p>
</ul>
</ul> 
</ul>
</div>

## Klasa *complex*

---

```python
c = 10 + 5j    # utwórz obiekt klasy complex
```

```python
c.real         # dane: real
```

```bash
10.0
```

```python
c.imag         # dane: imag
```

```bash
5.0
```

```python
c.conjugate()  # metody: conjugate
```

```bash
(10-5j)
```

#

## Programowanie obiektowe

---

* tworzenie obiektów
    * mogą przechowywać dane
    * mogą wykonywać opearacje
    * przykład: klasa samochód
        * dane: moc, masa, moment obrotowy ...
        * metody: jedź, skręć, ...
* komunikacja między obiektami
    * przykład: klasa łyżka i klasa zupa
        * łyżka.pobierz(zupa)

## Klasa w Pythonie

---

```py
class Nazwa:
    instrukcje
    ...
```

* zbudujemy krok po kroku klasę trójkąt:
    * dane: boki a, b, c
    * metody: pole, obwód, typ...

## "Pusta" klasa

---

```python
class Triangle:
    pass
```


```python
# na razie klasa Triangle
# nie zawiera ani danych ani metod
# ale już możemy stworzyć obiekt typu Triangle

t = Triangle()
```

```python
type(t)
```

```bash
__main__.Triangle
```


## Uwaga

---

* w Pythonie można dodawać atrybuty do istniejących obiektów (choć nie jest to zalecane!)


```python
t.a = 3.0  # atrybut a obiektu t
t.b = 4.0  # atrybut b obiektu t
t.c = 5.0  # atrybut c obiektu t

print(t.a, t.b, t.c)  # drukuj atrybuty a, b, c
```

```bash
3.0 4.0 5.0
```

```python
def drukuj(triangle):  # każdy obiekt może być argumentem funkcji
    print(triangle.a, triangle.b, triangle.c)
    
drukuj(t)
```

```bash
3.0 4.0 5.0
```

## Inicjalizacja

---

* `__init__` - prawie jak konstruktor, ale wywoływana **po** utworzeniu instancji
* *self* - odpowiednik *this* z c++


```python
class Triangle:
    """Dokumentacja jak w przypadku funkcji"""
    
    def __init__(self, a, b, c):
        """Prawie jak konstruktor"""
        self.a = a  # zmiennej obiekt.a
        self.b = b  # przypisz wartość a
        self.c = c  # itd
```

```python
t = Triangle(3, 4, 5)  # wywołuje funkcję __init__(3, 4, 5)
```

```python
print(t.a, t.b, t.c)
```

```bash
3 4 5
```

## *self*

---

* pierwszy argument każdej metody = *self*
* przyjęto konwencję *self*, ale może to być dowolna nazwa


```python
class Triangle:
    """Dokumentacja jak w przypadku funkcji"""
    
    def __init__(this, a, b, c):
        """Prawie jak konstruktor"""
        this.a = a
        this.b = b
        this.c = c
```

```python
# wywołuje funkcję __init__(3, 4, 5)
t = Triangle(3, 4, 5)
```


```python
print(t.a, t.b, t.c)
```

```bash
3 4 5
```

## Dokumentacja

---

```python
help(t)
```

```bash
Help on Triangle in module __main__ object:

class Triangle(builtins.object)
    |  Dokumentacja jak w przypadku funkcji
    |  
    |  Methods defined here:
    |  
    |  __init__(this, a, b, c)
    |      Prawie jak konstruktor
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

#

## Metody specjalne

---

* `__init__` jest jedną z metod specjalnych klasy
* [tutaj](https://docs.python.org/3/reference/datamodel.html#special-method-names) znajduje się pełna lista dostępnych metod specjalnych
* w trakcie wykładu pojawią się kolejne (wszystkie `__nazwa__`)

## *str* i *repr*

---

* `__repr__` - "oficjalna" reprezentacja obiektu, powinna być jednoznaczna; wywołana przez `repr(obiekt)` lub w interpreterze po wpisaniu nazwy zmiennej
* `__str__` - "nieformalna" reprezentacja obiektu, powinna być czytelna; wywołana przez `str(obiekt)` lub `print`

## *Triangle* : *str* i *repr*

---


```python
class Triangle:
    # pomijamy dokumentację: oszczędność slajdu
    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c
        
    def __str__(self):  # zwraca string
        return "Trójkąt o bokach: {}, {}, {}"\
                .format(self.a, self.b, self.c)
    
    def __repr__(self):  # zwraca string
        return "Triangle({}, {}, {})"\
                .format(self.a, self.b, self.c)
```

## *Triangle* : *str* i *repr*

---


```python
t = Triangle(3, 4, 5)

print(t)  # wywołuje __str__
```

```bash
Trójkąt o bokach: 3, 4, 5
```

```python
t  # (w interpreterze) wywołuje __repr__
```


```bash
Triangle(3, 4, 5)
```

#

## Własne metody - obwód

---

```python
class Triangle:

    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c
        
    def obwod(self):
        # do zmiennych obiektu odwołujemy się przez self.zmienna
        return self.a + self.b + self.c
```

```python
t = Triangle(3, 4, 5)
```

```python
t.obwod()
```

```bash
12
```

## Własne metody - pole

---


```python
from math import sqrt

class Triangle:

    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c
        
    def obwod(self):
        return self.a + self.b + self.c
    
    def pole(self):
        # do metod odwołujemy się przez self.metoda
        p = self.obwod()/2
        return sqrt(p*(p - self.a)*(p - self.b)*(p - self.c))
```

## Test

---

```python
t = Triangle(3, 4, 5)

print("Obwód =", t.obwod())
print("Pole =", t.pole())
```

```bash
Obwód = 12
Pole = 6.0
```

#

## Klasa wektor

---

* współrzędne *x*, *y*, *z*
* długość wektora
* dodawanie wektorów
* mnożenie wektora przez liczbę
* iloczyn skalarny
* ...

## Wektor: długość

---

```python
from math import sqrt

class Wektor:
    """Trójwymiarowy wektor"""
    
    def __init__(self, x=0.0, y=0.0, z=0.0):
        self.x = x
        self.y = y
        self.z = z
        
    def norm(self):
        """Długość wektora"""
        return sqrt(self.x**2 + self.y**2 + self.z**2)
```

## Długość: test

---

```python
w = Wektor(1)  # utwórz wektor (1, 0, 0)

w.norm()
```

```bash
1.0
```

```python
w.x = 2  # zmień składową x

w.norm()
```

```bash
2.0
```

## Zmienne prywatne

---


```python
class Wektor:
    """Trójwymiarowy wektor"""
    
    def __init__(self, x=0.0, y=0.0, z=0.0):
        self._x = x  # zmienne "prywatne"
        self._y = y  # sygnalizuje się _
        self._z = z
        
    def __str__(self):
        return "[{}, {}, {}]".format(self._x, self._y, self._z)
```

## Wektor prywatny

---


```python
from wektor import Wektor

w = Wektor(1)  # utwórz wektor (1, 0, 0)

print(w)
```

```bash
[1, 0.0, 0.0]
```


```python
# dostęp do _zmienna nie jest ograniczony
# jest to tylko wskazówka, żeby nie ruszać
w._x = 2.0

print(w)
```

```bash
[2.0, 0.0, 0.0]
```

## Zmienne bardziej prywatne

---


```python
class Wektor:
    """Trójwymiarowy wektor"""
    
    def __init__(self, x=0.0, y=0.0, z=0.0):
        self.__x = x  # zmienne zaczynające się __
        self.__y = y  # zamieniane są na
        self.__z = z  # _nazwa_klasy__zmienna
        
    def __str__(self):
        return "[{}, {}, {}]".format(self.__x, self.__y, self.__z)
```

## Wektor bardziej prywatny

---


```python
w = Wektor(1)  # [1, 0, 0]

print(w)
```

```bash
[1, 0.0, 0.0]
```


```python
w.__x = 2  # nie zmienia skladowej __x

print(w)
```

```bash
[1, 0.0, 0.0]
```


```python
w._Wektor__x = 2  # zmienia składową __x

print(w)
```

```bash
[2, 0.0, 0.0]
```

#

## Dodawanie wektorów

---


```python
class Wektor:
    """Trójwymiarowy wektor"""
    
    def __init__(self, x=0.0, y=0.0, z=0.0):
        self.x = x
        self.y = y
        self.z = z
        
    def __str__(self):
        return "[{}, {}, {}]".format(self.x, self.y, self.z)
        
    def __add__(self, w):  # operator dodawania
        return Wektor(self.x + w.x, self.y + w.y, self.z + w.z)
```

## Dodawanie: test

---


```python
x = Wektor(1, 2, 3)
y = Wektor(2, 4, 6)

print(x + y)  # wywołuje x.__add__(y)
```

```bash
[3, 6, 9]
```

## Wektor: iloczyn skalarny

---

```python
class Wektor:
    """Trójwymiarowy wektor"""
    
    def __init__(self, x=0.0, y=0.0, z=0.0):
        self.x = x
        self.y = y
        self.z = z
        
    def __str__(self):
        return "[{}, {}, {}]".format(self.x, self.y, self.z)
        
    def __mul__(self, w):  # operator mnożenia
        return self.x*w.x + self.y*w.y + self.z*w.z
```

## Iloczyn skalarny: test

---

```python
x = Wektor(1, 2, 3)
y = Wektor(2, 4, 6)

print(x*y)  # wywołuje x.__mul__(y)
```

```bash
28
```

## Mnożenie przez liczbę

---


```python
class Wektor:
    """Trójwymiarowy wektor"""
    
    def __init__(self, x=0.0, y=0.0, z=0.0):
        self.x = x
        self.y = y
        self.z = z
        
    def __str__(self):
        return "[{}, {}, {}]".format(self.x, self.y, self.z)
        
    def __mul__(self, w):          # operator mnożenia
        if type(w) == type(self):  # dla wektora - iloczyn skalarny
            return self.x*w.x + self.y*w.y + self.z*w.z
        else:                      # dla liczby - mnożenie składowych
            return Wektor(w*self.x, w*self.y, w*self.z)
```

## Mnożenie: test

---

```python
x = Wektor(1, 2, 3)
y = Wektor(2, 4, 6)

print(x*y)  # wywołuje x.__mul__(y)
```

```bash
28
```


```python
print(x*10)  # mnoży wektor z przez 10
```

```bash
[10, 20, 30]
```


```python
print(10*x)  # nie działa...
```

```bash
TypeError: unsupported operand type(s) for *: 'int' and 'Wektor'
```

## Mnożenie z prawej

---


```python
class Wektor:
    """Trójwymiarowy wektor"""
    
    def __init__(self, x=0.0, y=0.0, z=0.0):
        self.x = x
        self.y = y
        self.z = z
        
    def __str__(self):
        return "[{}, {}, {}]".format(self.x, self.y, self.z)
        
    def __mul__(self, w):          # operator mnożenia
        if type(w) == type(self):  # dla wektora - iloczyn skalarny
            return self.x*w.x + self.y*w.y + self.z*w.z
        else:                      # dla liczby - mnożenie składowych
            return Wektor(w*self.x, w*self.y, w*self.z)
        
    def __rmul__(self, w):  # mnożenie z prawej
        return self.__mul__(w)
```

## Mnożenie z prawej: test

---


```python
x = Wektor(1, 2, 3)

print(x*10)
```

```bash
[10, 20, 30]
```


```python
print(10*x)
```

```bash
[10, 20, 30]
```