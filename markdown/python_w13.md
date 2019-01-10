% Języki skryptowe Python
% Wykład 13

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

# 

## Polimorfizm

---

* współdzielenie *interfejsu* przez różne typy


```python
class Kot:
    def glos(self):
        print("Miau")

class Pies:
    def glos(self):
        print("Hau")

class Krowa:
    def glos(self):
        print("Muu") 
```


```python
for zwierze in [Kot(), Pies(), Krowa()]:
    zwierze.glos()  # za każdym razem inny typ
```

```bash
Miau
Hau
Muu
```

## Ryby głosu nie mają

---


```python
class Ryba:
    pass  # brak definicji glos
```


```python
for zwierze in [Kot(), Pies(), Krowa(), Ryba()]:
    zwierze.glos()  # Ryba nie ma zdefiniowanej metody glos
```

```bash
Miau
Hau
Muu
...
AttributeError: 'Ryba' object has no attribute 'glos'
```

## Wymuszanie interfejsu

---


```python
class Zwierze:
    def glos(self):
        pass
    
class Kot(Zwierze):
    def glos(self):  # nadpisuje Zwierze.glos
        print("Miau")
        
class Ryba(Zwierze):
    pass
```

```python
for zwierze in [Kot(), Ryba()]:
    zwierze.glos()  # Ryba siedzi cicho
```

```bash
Miau
```

## Większe wymuszanie interfejsu

---


```python
class Zwierze:
    def glos(self):
        raise NotImplementedError("Każde zwiesze musi mieć głos.")
    
class Kot(Zwierze):
    def glos(self):  # nadpisuje Zwierze.glos
        print("Miau")
        
class Ryba(Zwierze):
    pass
```

```python
for zwierze in [Kot(), Ryba()]:
    zwierze.glos() # Ryba zwróci błąd
```

```bash
Miau
...
NotImplementedError: Każde zwiesze musi mieć głos.
```

#

## Przykład - Wielokąt

---

```python
class Wielokat:
    
    def __init__(self, *boki):
        self.boki = boki       # krotka
        
    def obwod(self):           # suma długości
        return sum(self.boki)  # boków
        
    def pole(self): raise NotImplementedError
```

```python
w = Wielokat(1, 2, 3, 4, 5)    # pięciokąt

w.obwod()
```

```bash
15
```

## Przykład - Trójkąt

---

```python
class Trojkat(Wielokat):
    
    def __init__(self, *boki):
        super().__init__(*boki)    # utwórz wielokąt
        
    def pole(self):
        pole = p = self.obwod()/2  # obwod zdefiniowane w Wielokat
        
        for bok in self.boki:      # wzór Herona
            pole *= (p - bok)      # p(p - a)(p - b)(p - c)
            
        return pole**0.5 # pierwiastek
```


```python
t = Trojkat(3, 4, 5)

t.obwod()  # z Wielokat
```

```bash
12
```

```python
t.pole()  # z Trójkat
```

```bash
6.0
```

## Przykład - Trójkąt Równoboczny

---


```python
class TrojkatR(Trojkat):
    
    def __init__(self, bok):
        super().__init__(bok, bok, bok)  # Trójkąt -> Wielokąt
        
    def pole(self):
        return (self.boki[0]**2)*(3**0.5)/4
```


```python
t = TrojkatR(3)  # (3, 3, 3)

t.pole()  # TrojkatR.pole()
```

```bash
3.8971143170299736
```

```python
t = Trojkat(3, 3, 3)

t.pole()  # Trojkat.pole() 
```

```bash
3.897114317029974
```

#

## Wielokrotne dziedziczenie

---

* klasa może posiadać kilka klas bazowych
* posiada wtedy wszystkie dane i metody
* a co jeśli się powtarzają?

## Przykład - amifibia

---

```python
class Samochod:
    
    def jedz(self):
        print("Jadę...")
        
class Lodz:
    
    def plyn(self):
        print("Płynę...")
        
class Amfibia(Samochod, Lodz): pass
```

```python
amfibia = Amfibia()

amfibia.jedz()  # Samochod
amfibia.plyn()  # Lodz
```

```bash
Jadę...
Płynę...
```

## Przykład - amifibia v2

---

```python
class Samochod:
    def run(self):
        print("Jadę...")
        
class Lodz:
    def run(self):
        print("Płynę...")
        
class Amfibia1(Samochod, Lodz): pass
class Amfibia2(Lodz, Samochod): pass
```

```python
amifibia1 = Amfibia1()
amifibia1.run()
```

```bash
Jadę...
```

```python
amifibia2 = Amfibia2()
amifibia2.run()
```

```bash
Płynę...
```

#

## Generatory

---

* funkcja, która zachowuje się jak iterator (czyli można np. wykorzystać ją w pętli)
* zamiast tworzyć całą listę obiektów, które będą przechowywane w pamięci
* oszczędza czas i pamięć

## Dygresja: *range*

---

```python
%timeit -n1 range(1000000)  # tworzy obiekt range
```

```bash
1 loop, best of 3: 1.68 µs per loop
```


```python
# kolejne elementy range
# muszą zostać zapisane w pamięci
%timeit -n1 list(range(1000000))
```

```bash
1 loop, best of 3: 53.3 ms per loop
```

## Ciąg geometryczny

---

```python
def geometryczny(a1, q, n):
    """Generuje n wyrazów ciągu geometrycznego."""
    
    ciag = [a1]
    
    for _ in range(n-1):         # n-1 bo pierwszy już jest
        ciag.append(ciag[-1]*q)  # następny = poprzedni * iloraz
        
    return ciag
```

```python
ciag = geometryczny(1, 3, 10)

print(ciag)
```

```bash
[1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683]
```

## Ciąg geometryczny - generator

---


```python
def gen_geometryczny(a1, q, n):
    """Generuje n wyrazów ciągu geometrycznego."""
    
    for _ in range(n):
        yield a1 # zwróć obecną wartość a1
        a1 *= q  # i czekaj na kolejną iterację
```

## Generator a lista

---


```python
ciag1 = geometryczny(1, 3, 10)      # zwraca listę 
ciag2 = gen_geometryczny(1, 3, 10)  # zwraca generator
```

```python
print(ciag1)
```

```bash
[1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683]
```

```python
print(ciag2)
```

```bash
<generator object gen_geometryczny at 0x7f9bac1ec678>
```

## Generator jak iterator

---

```python
next(ciag2)  # pierwszy element
```

```bash
1
```

```python
next(ciag2)  # kolejny element itd
```

```bash
3
```

```python
# a najczęściej w pętli
for i in gen_geometryczny(1, 3, 10):
    print(i, end=', ')
```

```bash
1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683, 
```

## Czas

---

```python
%timeit -n3 geometryczny(1, 3, 10000)
```

```bash
3 loops, best of 3: 12.8 ms per loop
```

```python
%timeit -n3 gen_geometryczny(1, 3, 10000)
```

```bash
3 loops, best of 3: 978 ns per loop
```

## Czas dokładniej

---

```python
def test_lista():
    """Pętla po liście"""
    for element in geometryczny(1, 3, 10000):
        pass
    
def test_generator():
    """Pętla po generatorze"""
    for element in gen_geometryczny(1, 3, 10000):
        pass
```

```python
%timeit -n3 test_lista()
```

```bash
3 loops, best of 3: 13.6 ms per loop
```

```python
%timeit -n3 test_generator()
```

```bash
3 loops, best of 3: 12.1 ms per loop
```

## Lista czy generator

---

* generator będzie z reguły szybszy
* generator może być nieskończony
* jednak nie można wykonywać operacji na "elementach", np. sortowania
* lista może być efektywniejsza, jeśli planujemy więcej pętli

## "Wyczerpanie" generatora

---


```python
ciag = gen_geometryczny(1, 3, 20)  # generuje 20 wyrazów
```


```python
for i in range(10):   # wydrukuj 10 pierwszych
    print(next(ciag), end=' ')
```

    1 3 9 27 81 243 729 2187 6561 19683 


```python
for element in ciag:  # nie zaczyna od pierwszego!
    print(element, end=' ')
```

```bash
59049 177147 531441 1594323 4782969 14348907 43046721 129140163 387420489 1162261467 
```

## Wielekrotne użycie

---

```python
def lista_loop(n=10):
    """Wykonuje n pętli po liście"""
    ciag = geometryczny(1, 3, 10000)
    
    for _ in range(n):
        for element in ciag:
            pass
    
def gen_loop(n=10):
    """Wykonuje n pętli po generatorze"""
    for _ in range(n):
        for element in gen_geometryczny(1, 3, 10000):
            pass
```

```python
%timeit -n3 lista_loop()
```

```bash
3 loops, best of 3: 14.2 ms per loop
```

```python
%timeit -n3 gen_loop()
```

```bash
3 loops, best of 3: 77.4 ms per loop
```

#

## Powtórka: listy składane (*list comprehensions*)

---


```python
# chcemy stworzyć listę zawierającą
# kwadraty wszystkich cyfr

kwadraty = []

for x in range(10):
    kwadraty.append(x**2)
    
print(kwadraty)
```

```bash
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

```python
# a korzystając z listy skladanej

kwadraty = [x**2 for x in range(10)]

print(kwadraty)
```

```bash
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

## Append vs lista składana

---


```python
def create_list(n=100000):
    """Tworzy listę kwadratów pierwszych n liczb naturalnych"""
    
    kwadraty = []
    
    for x in range(n):
        kwadraty.append(x**2)
        
    return kwadraty

def list_comprehension(n=100000):
    """Tworzy listę kwadratów pierwszych n liczb naturalnych"""
    
    return [x**2 for x in range(n)]
```

## Czas

---


```python
%timeit -n3 x = create_list()  # lista tworzona przez append
```

```bash
3 loops, best of 3: 48.3 ms per loop
```

```python
%timeit -n3 y = list_comprehension()  # lista składana
```

```bash
3 loops, best of 3: 42.5 ms per loop
```

```python
create_list() == list_comprehension()  # wynik ten sam
```

```bash
True
```

## Przykład

---


```python
def force(m, a):
    """Zwraca wartość siły [N].
    
    Liczy siłę jaką należy zadziałać na ciało
    o masie m [kg], aby nadać mu przyspieszenie a [m/s^2].
    """
    return m*a

wagi = [10, 20, 30, 40, 50]       # kg
przyspieszenia = [1, 2, 3, 4, 5]  # m/s^2
```

```python
# stwórz tablicę z wartościami sił 

sily = [force(m, a) for m, a in zip(wagi, przyspieszenia)]

print(sily)
```

```bash
[10, 40, 90, 160, 250]
```

## Generator "jak lista składana"

---


```python
# lista składana
list_comprehension = [x**2 for x in range(10)]

# generator expression
generator = (x**2 for x in range(10))
```

```python
for x in generator:
    print(x, end=' ')
```

```bash
0 1 4 9 16 25 36 49 64 81 
```

```python
# lub prościej

for x in (x**2 for x in range(10)):
    print(x, end=' ')
```

```bash
0 1 4 9 16 25 36 49 64 81 
```

## Uwagi na koniec

---

* unikaj tworzenia list przez *append*, jeśli można wykorzystać *list comprehension*
* unikaj tworzenia list jeśli jest to zbędne (użyj generatorów)
* unikaj *generator function* na rzecz *generator expression*
* jest też *tuple comprehension*:

```py
krotka = *(x**2 for x in range(10)),
print(krotka)
```

```bash
(0, 1, 4, 9, 16, 25, 36, 49, 64, 81)
```
