# Imię i nazwisko:  \vspace{20pt}

1. Wyjaśnij różnicę między trybami `r+` i `w+` otwierania plików.

\vspace{50pt}

2. Niech `dane.txt` zawiera:

```
Ala
Ma
Kota
```

Jaki będzie wynik działania poniższego kodu:

```py
for a, b in enumerate(open("dane.txt", 'r').readlines()):
    print(f"{a} -> {b}")
```