# Imię i nazwisko:  \vspace{20pt}

1. Uzupełnij metodę `__init__`:

```py
class Prostokat:

    def __init__(self, a, b):





        
    def __str__(self):
        return f"Pole prostokąta = {self.pole}, a obwód = {self.obwod}"
        
        
print(Prostokat(2, 3))
```

tak, aby skrypt wyświetlał na ekranie:

```bash
Pole prostokąta = 6, a obwód = 5
```

2. Uzupełnij klasę `Ciag` o odpowiednią metodę:

```py
class Ciag:

    def __init__(self, *x):
        self.wyrazy = x
```

\vspace{100pt}

tak, aby poniższy kod

```py
c = Ciag(1, 2, 3, 4, 5)
print(sum(c))
```

drukowałem na ekranie `15`.