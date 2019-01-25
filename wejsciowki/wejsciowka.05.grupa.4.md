# Imię i nazwisko:  \vspace{20pt}


1. Jaki będzie wynik działania poniższego kodu:

```py
import string
print(len(string.ascii_letters))
```

\vspace{50pt}

2. Jaki będzie wynik działania poniższego kodu:

```py
i = 0

def create_empty_and_fill(lista = []):
    global i
    i += 1

    lista.append(i)

    while i < 5:
        return create_empty_and_fill()
    else:
        return lista

print(create_empty_and_fill())

```