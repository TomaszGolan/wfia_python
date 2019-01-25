# Imię i nazwisko:  \vspace{20pt}

1. Jaki będzie wynik działania poniższej pętli:

```py
for x in [a**2 for a in range(1, 5)]:
    print(x - 1)
```

\vspace{50pt}

2. Jaki będzie wynik działania poniższego programu:

```py
moje_liczby = list(range(5))

while moje_liczby:
    for liczba in moje_liczby:
        print(liczba)

    moje_liczby = moje_liczby[:-1]
```