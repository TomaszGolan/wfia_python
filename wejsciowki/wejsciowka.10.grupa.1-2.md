# Imię i nazwisko:  \vspace{20pt}

Uzupełnij definicję klasy `Student` o dwie brakujące metody (po 1 pkt każda):

```py
class Student:

    def __init__(self, imie, indeks):
        self.imie = imie
        self.id = indeks
```

\vspace{200pt}

tak, aby poniższy kod

```py
s = Student("Jan", 123)
print(s)
s.setname("Marek")
print(s)
```

wydrukował na ekranie:

```bash
Student Jan -> 123
Student Marek -> 123
```