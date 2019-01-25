# Imię i nazwisko:  \vspace{20pt}

1. Co wydrukuje na ekranie poniższy kod:

```py
ukryta_liczba = 5.5

if ukryta_liczba > 5:
    print("Twoja liczba jest większa od 5.")
elif ukryta_liczba < 6:
    print("Twoja liczba jest mniejsze od 6.")
else:
    print("Twoja liczba jest mniejsza od 5 lub większa od 6.")
```

\vspace{50pt}

2. Jaka będzie wartość zmiennej `licznik` po zakończeniu działania pętli `while`?

```py
licznik = 0
komenda = ''

while licznik < 10 or komenda != 'stop':
    licznik += 1

    if not licznik % 3 and not licznik % 5:
        komenda = 'stop'
```