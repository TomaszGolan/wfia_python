# Imię i nazwisko:  \vspace{20pt}

Niech 

```py
def funkcja(a, b, *c):
    return a + b - sum(c)
```

Jaki będzie wynik działania poniższego kodu:

```py
x = funkcja(1, 2)
y = funkcja(3, 4, 5)
z = funkcja(*range(5))

print("x = ", x)  # 0.5 pkt
print("y = ", y)  # 0.5 pkt
print("z = ", z)  # 1 pkt
```