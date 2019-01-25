# Imię i nazwisko:  \vspace{20pt}

Zawartość pliku `zmienne.py`:

```py
a = 1
b = 2
c = 3

_x = 1.0
_y = 2.0
_z = 3.0
```

Jaki będzie wynik działania poniższego kodu:

```py
from zmienne import *

a = 10
_x = a

def f():
    b = 20
    return a + b + c

def g():
    _y = b
    return _x + _y + _z

print(f())  # 1 pkt
print(g())  # 1 pkt
```