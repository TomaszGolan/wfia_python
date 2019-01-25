# Imię i nazwisko:  \vspace{20pt}

Niech

```py
class Ciag:

    def __init__(self, *x):
        self.wyrazy = x
        
    def __iter__(self):
        for i in range(5):
            yield self.wyrazy[i]
            
    def __str__(self):
        return "Wyrazy ciągu: {}".format(self.wyrazy)
```

1. Jaki będzie rezultat poniższego kodu:

```py
c = Ciag(*range(10))
print(c)
```

\vspace{50pt}

2. Jaki będzie rezultat poniższego kodu:

```python
c = Ciag(*range(10))

for i, wyraz in enumerate(c):
    print("{} -> {}".format(i, wyraz))
```
