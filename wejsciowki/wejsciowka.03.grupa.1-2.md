# Imię i nazwisko:  \vspace{20pt}

1. Co wydrukuje na ekranie poniższy kod:

```py
slownik = {0: 'a', 1: 'b', 2: 'c'}

for k, v in slownik.items():
    if k > 0:
        print(v)
```

\vspace{50pt}

2. Co wydrukuje na ekranie poniższy kod:
 
```py
slownik = {0: 'a', 1: 'b', 2: 'c'}
kopia = slownik

kopia[0] = 'd'
slownik[1] = 'e'

print(slownik)
print(kopia)
```