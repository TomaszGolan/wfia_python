# Imię i nazwisko:  \vspace{20pt}

1. Wyjaśnij różnicę między trybami `r` i `r+` otwierania plików.

\vspace{50pt}

2. Jaka będzie zawartość pliku `dane.txt` po wykonaniu poniższego skryptu: 

```py
for i in range(10):
    file = open("dane.txt", "w")
    file.write(str(i))
    file.close()
```