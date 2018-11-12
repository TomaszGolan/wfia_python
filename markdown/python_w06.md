% Języki skryptowe Python
% Wykład 6

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

# 

## Nazwy zmiennych

---


```python
zmienna = 10              # zmienna wskazuje na int

print(zmienna)

zmienna = "Hello World!"  # zmienna wskazuje na str

print(zmienna)

def funkcja():
    print("Jestem funkcją.")
    
zmienna = funkcja         # zmienna wskazuje na funkcje

zmienna()
```

```bash
10
Hello World!
Jestem funkcją.
```

## Niebezpieczne nadpisania

---


```python
def moja_nazwa():  # moja_nazwa wskazuje na funkcję
    print("Jestem funkcją.")
    
def moja_nazwa():  # moja_nazwa wskazuje inną funkcję
    print("Jestem nową funkcją.")
    
moja_nazwa()
```

```bash
Jestem nową funkcją.
```

```python
moja_nazwa = 10  # moja_nazwa wskazuje na int 

moja_nazwa()     # TypeError: 'int' object is not callable
```

```bash
...
TypeError: 'int' object is not callable
```

## Moduły - *import* ...

---

```python
import math

def sin(x):
    """Zwraca x."""
    return x
```

```python
math.sin(math.pi / 2)  # wywołanie [moduł].[funkcja]
```

```bash
1.0
```

```python
sin(math.pi / 2)  # wywołanie [funkcja]
```

```bash
1.5707963267948966
```

## Moduły - *from ... import ...*

---


```python
from math import sin

def sin(x):       # nadpisuje sin z math
    """Zwraca x."""
    return x

sin(math.pi / 2)  # wywołanie funkcji sin
```

```bash
1.5707963267948966
```

```python
def sin(x):
    """Zwraca x."""
    return x

from math import sin  # nadpisuje sin

sin(math.pi / 2)      # wywołanie math.sin
```

```bash
1.0
```

#

## Przestrzenie nazw

---

* abstrakcyjna przestrzeń przechowująca nazwy
* np. przestrzeń nazw wbudowanych


```python
print(dir(__builtin__)[-72:])
```

```bash
['abs', 'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable', 'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits', 'delattr', 'dict', 'dir', 'divmod', 'dreload', 'enumerate', 'eval', 'exec', 'filter', 'float', 'format', 'frozenset', 'get_ipython', 'getattr', 'globals', 'hasattr', 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass', 'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview', 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice', 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars', 'zip']
```

## Uwaga: nadpisać można wszystko

---

```python
slownik = dict(x=1, y=2)

print(slownik)
```

```bash
{'y': 2, 'x': 1}
```

```python
def dict(x, y):  # nazwy wbudowane też można nadpisać
    return x, y

slownik = dict(x=1, y=2)

print(slownik)
```

```bash
(1, 2)
```

## Przestrzeń nazw lokalnych

---

* zmienne zdefiniowane wewnątrz funkcji (niedostępne poza nią)


```python
def funkcja():              # zmienne lokalne dostępne
    zmienna_lokalna = 1     # są tylko wewnątrz funkcji
    return zmienna_lokalna  # w której zostały zdefiniowane

print("zmienna_lokalna =", zmienna_lokalna)
```

```bash
...
NameError: name 'zmienna_lokalna' is not defined
```

## Przestrzeń nazw globalnych

---

* dostępne w całym module (pliku)

```python
zmienna_globalna = "Python"

def funkcja():
    return zmienna_globalna

# wewnątrz funkcji zmienne globalne są dostępne
funkcja()
```

```bash
'Python'
```

## Zmienne lokalne nadpisują globalne

---


```python
zmienna_globalna = "Python"

def funkcja():
    zmienna_globalna = "Nowy Python"         # lokalna zmienna_globalna
    print("in funkcja:", zmienna_globalna)

funkcja()

print("outside funkcja:", zmienna_globalna)  # globalna bez zmian
```

```bash
in funkcja: Nowy Python
outside funkcja: Python
```

## Albo *global* albo *local*

---


```python
zmienna_globalna = "Python"

def funkcja():
    print("in funkcja:", zmienna_globalna)  # globalna?
    zmienna_globalna = "Nowy Python"
    print("in funkcja:", zmienna_globalna)  # lokalna?

funkcja()
```

```bash
...
UnboundLocalError: local variable 'zmienna_globalna' referenced before assignment
```

#

## Kolejność przestrzeni

---

```python
#nazwy lokalne, potem globalne, na końcu wbudowane
list = tuple  # zmienna globalna nadpisuje wbudowane list
dict = float  # zmienna globalna nadpisuje wbudowane dict

print("type(list()) =", type(list()))
print("type(dict()) =", type(dict()))

def funkcja():
    dict = int  # zmienna lokalna nadpisuje globalne dict
    print("In funkcja:")
    print("\ttype(dict()) =", type(dict()))  # lokalna
    print("\ttype(list()) =", type(list()))  # globalna
    print("\ttype(int()) =", type(int()))    # wbudowana

funkcja()
```

```bash
type(list()) = <class 'tuple'>
type(dict()) = <class 'float'>
In funkcja:
    type(dict()) = <class 'int'>
    type(list()) = <class 'tuple'>
    type(int()) = <class 'int'>
```

## Wielokrotne zagnieżdżenie

---


```python
a = "global a"  # zasięg zmiennych a, b, c
b = "global b"  # jest globalny
c = "global c"

def funkcja():
    a = "local a"  # lokalne a, b dostępne w funkcji
    b = "local b"  # i w każdym kolejnym zagnieżdzeniu
    
    def funkcja_w_funkcji():
        a = "local local a"  # dostępna tylko w funkcja_w_funkcji
        print(a, b, c, sep='\n')
    
    funkcja_w_funkcji()
    
funkcja()  # od "najlokalniejszej" do "najglobalniejszej"
```

```bash
local local a
local b
global c
```

## Uwaga na globalne mutowalne

---


```python
x = [1, 2, 3]
y = ['a', 'b', 'c']

def funkcja():
    x = [1, 2, 3, 4]  # przypisanie -> zmienna lokalna
    y.append('d')     # modyfikacja -> ciągle globalna
    
funkcja()

print(x, y, sep='\n')
```

```bash
[1, 2, 3]
['a', 'b', 'c', 'd']
```

## Wymuszanie zmiennej globalnej

---


```python
zmienna = "globalna"

def f():
    global zmienna             # przypisanie nie tworzy zmiennej lokalnej
    zmienna = "nowa globalna"  # ale modyfikuje globalną
    
f()

print(zmienna)
```

```bash
nowa globalna
```

## Wymuszanie zmiennej "nielokalnej"

---


```python
a = "global a"  # globalna

def f():
    a = "local a"  # lokalna w f
    
    def g():
        a = "local local a"  # lokalna w g
        print("in g():", a)
        
    g()
        
    print("in f():", a)

f()

print("outside:", a)
```

```bash
in g(): local local a
in f(): local a
outside: global a
```

## Wymuszanie zmiennej "nielokalnej"

---


```python
a = "global a"  # globalna

def f():
    a = "local a"  # lokalna w f
    
    def g():
        global a             # używaj globalnej
        a = "local local a"  # modyfikuje globalną
        print("in g():", a)
        
    g()
        
    print("in f():", a)

f()

print("outside:", a)
```

```bash
in g(): local local a
in f(): local a
outside: local local a
```

## Wymuszanie zmiennej "nielokalnej"

---

```python
a = "global a"  # globalna

def f():
    a = "local a"  # lokalna w f
    
    def g():
        nonlocal a           # użyj a z poprzedniego zagnieżdżenia
        a = "local local a"  # modyfikuje a z f
        print("in g():", a)
        
    g()
        
    print("in f():", a)

f()

print("outside:", a)
```

```bash
in g(): local local a
in f(): local local a
outside: global a
```

## Uwaga dla programistów C/C++

---


```python
def funkcja(flag=True):
    if flag:    # zmienna zdefiniowana w bloku
        x = 10  # jest dostępna poza tym blokiem
    else:
        x = 20
        
    print(x)
```

```python
funkcja() 
```

```bash
10
```


```python
funkcja(False)
```

```bash
20
```

## Zasięg

---

* obszar dostępności danej przestrzeni nazw

```python
import math
from math import cos

a = 1  # zasięg -> cały plik

def f():
    # uwaga: zaleca się wszystkie importy robić na początku
    from math import log  # zasięg log(...) -> funkcja
    b = 2                 # zasięg -> funkcja
    c = log(3) 
    
d = math.sin(4)  # sin(...) poza zasięgiem [moduł].[funkcja]
e = cos(5)       # zasięg cos(...) -> cały plik
# f = log(6)     # NameError: name 'log' is not defined
```

#

## Dokumentacja

---

```python
help(help)
```

```bash
Help on _Helper in module _sitebuiltins object:

class _Helper(builtins.object)
    |  Define the builtin 'help'.
    |  
    |  This is a wrapper around pydoc.help that provides a helpful message
    |  when 'help' is typed at the Python interactive prompt.
    |  
    |  Calling help() at the Python prompt starts an interactive help session.
    |  Calling help(thing) prints help for the python object 'thing'.
    |  
    |  Methods defined here:
    |  
    |  __call__(self, *args, **kwds)
    |      Call self as a function.
    |  
    |  __repr__(self)
    |      Return repr(self).
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

## Dokumentowanie własnych funkcji

---

```python
def funkcja():
    pass
```

```python
help(funkcja)
```

```bash
Help on function funkcja in module __main__:

funkcja()
```    

```python
def funkcja():
    """To jest moja funkcja, która nic nie robi"""
    pass
```

```python
help(funkcja)
```

```
Help on function funkcja in module __main__:

funkcja()
    To jest moja funkcja, która nic nie robi
```    

## Dokumentacja (PEP 257)

---

* dokumentacja (czyli tzw. *docstring*) wg standardów PEP 257:

    * jednolinjkowy opis

    ```py
    """Mój opis"""
    ```

    * wielolinijkowy opis

    ```py
    """Mój opis
    
    więcej opisu
    """
    ```

## Opis

---

* opis powinien krótki i jasny (i mieć sens), np:

```py

# taki opis nie ma sensu
def moja_funkcja(a, b):
    """moja_funkcja(a, b) -> a + b"""
    return a + b

# taki jest lepszy
def moja_funkcja(a, b):
    """Zwraca sumę podanych liczb"""
    return a + b
```

## Dokumentowanie zmiennych

---


```python
def reszta(a = 0, b = 0):
    """Zwraca resztę z dzielenia
    
    Keyword arguments:
    a -- licznik
    b -- mianownik
    """
    if not b:
        return 0
    return a%b
```

```python
help(reszta)
```

```bash
Help on function reszta in module __main__:

reszta(a=0, b=0)
    Zwraca resztę z dzielenia
    
    Keyword arguments:
    a -- licznik
    b -- mianownik
```    

## Wyrażenie *lambda*

---

```python
def suma(a, b):  # "klasyczna" funkcja
    return a + b
```


```python
lsuma = lambda a, b: a + b  # "anonimowa" funkcja
```


```python
suma(1, 2)  # wywołujemy funkcję suma
```

```bash
3
```

```python
lsuma(1, 2) # wywołujemy wyrażenia lambda
```

```bash
3
```

## Wyrażenie *lambda*

---

```python
def wrapper(funkcja):
    print("Wywołuję funkcję:", funkcja)
    funkcja()

def f():
    print("Hello World!")
    
wrapper(f)
```

```bash
Wywołuję funkcję: <function f at 0x7f92543518c8>
Hello World!
```

```python
wrapper(lambda: print("Hello World!"))
```

```bash0
Wywołuję funkcję: <function <lambda> at 0x7f92543517b8>
Hello World!
```

## Wyrażenie *lambda*

---

```python
def increase(n):
    print("Teraz tworzę lambdę")
    return lambda x: x + n

inc2 = increase(2)  # powiększ o 2
inc4 = increase(4)  # inc4 = lambda x: x + 4
```

```bash
Teraz tworzę lambdę
Teraz tworzę lambdę
```

```python
inc2(10)
```

```bash
12
```

```python
inc4(10)
```

```bash
14
```

#

## Rekurencja

---

```python
i = 0

def funkcja():
    global i  # używaj zmiennej globalnej i
    i += 1
    print(i, end=' ')
    if i < 10:
        return funkcja()  # wywołuje sama siebie
```

```python
funkcja()
```

```bash
1 2 3 4 5 6 7 8 9 10 
```

## Rekurencja - silnia

---

```python
def silnia(n):
    result = 1
    while n > 1:
        result *= n
        n -= 1
    return result
```


```python
print("Klasycznie silnia(5) =", silnia(5))
```

```bash
Klasycznie silnia(5) = 120
```

```python
def silnia(n):
    if n < 2:
        return 1  # 0! = 1, 1! = 1
    return n*silnia(n - 1)
```

```python
print("Rekurencyjnie silnia(5) =", silnia(5))
```

```bash
Rekurencyjnie silnia(5) = 120
```