# Imię i nazwisko:  \vspace{20pt}

1. Jaki będzie wynik działania poniższego programu:

```py
moje_liczby = [1, 3, 5, 7, 11]

for x in moje_liczby:
    print(x)
    moje_liczby.append(x)
```

\vspace{50pt}

2. Jaka będzie zawartość listy po zakończeniu pętli `while`:

```py
lista = [1]
licznik = 1

while licznik < 10:
    if licznik%2:
        licznik += 1
    else:
        lista.append(licznik)
        break
```