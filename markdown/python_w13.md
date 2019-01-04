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

