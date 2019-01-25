# Imię i nazwisko:  \vspace{20pt}

Niech

```py
def f(g, h, x):
    return g(h(x))

def g(x):
    return x**2

def h(x):
    return 2*x
```

Jaki będzie wynik działania poniższego kodu:

```py
x = f(g, h, 2)
y = f(h, g, 3)

print("x = ", x)  # 1 pkt
print("y = ", y)  # 1 pkt
```
