% Języki skryptowe Python
% Wykład 4

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

# 

## Typy mutowalne (*mutable*) i niemutowalne (*immutable*)

---

* typy liczbowe ("niemutowalne"): `int`, `float`, `complex`
* typy sekwencyjne ("mutowalne"): `list`
* typy sekwencyjne ("niemutowalne"): `tuple`, `range`, `str`


## `id` zmiennych

---


```py
x = 2  # tworzymy niemutowalną zmienną
id(x)  # i sprawdzamy jej id
```

```bash
140685772794432
```

```py
x = 3  # przypisanie nowej wartości 
id(x)  # tworzy nowy obiekt (z nowym id)
```

```bash
140685772794464
```


```py
x = [2]  # tworzymy mutowalną zmienną 
id(x)    # i sprawdzamy jej id
```

```bash
140685552461384
```

```py
x[0] = 3  # wartość wskazywana przez zmienną jest modyfikowana
id(x)     # ale jej id pozostaje stałe (uwaga: id(x[0]) będzie inne!)
```

```bash
140685552461384
```

## Konsekwencje

---

```py
x = 2  # uwtórz obiekt typu int
y = x  # y wskazuje na to samo co x
y = 5  # zmieniam y - nowe miejsce w pamięci

print(x)  # x dalej wskazuje na 2
```

```bash
2
```

```py
x = [1, 2, 3]  # utwórz obiekt typu list
y = x          # y wskazuje na to samo co x

print(id(x), id(y))
```

```bash
140684962055816 140684962055816
```

```py
y[0] = 4  # modyfikuję y

print(x)  # a zmienia się x...
```

```bash
[4, 2, 3]
```

## Funkcja `copy`

---

```py
x = [1, 2, 3]  # utwórz obiekt typu list
y = x.copy()   # stwórz kopię tego obiektu

print(id(x), id(y))  # teraz są to dwa różne obiekty
```

```bash
140685552556616 140685552460232
```

#


## "Odpakowywanie" (*unzip*)

---

```py
lista = [1, 2]

a, b = lista  # a = lista[0], b = lista[1]

print(a, b)
```

```bash
1 2
```

przykład: zamiana zmiennych


```py
a, b = b, a  # a, b = tuple(b, a)

print(a, b)
```

```bash
2 1
```

dla porównania przykład zamiany zmiennych w C++

```cpp
a = a + b - (b = a);
```

## *splat*, czyli tzw. *asterisk*

---

```py
x = [1, 2, 3]

# print(arg1, arg2, arg3, ..., +opcje)

print(x)                 # drukuje listę (1 argument)
print(*x)                # drukuje "rozpakowaną" listę (3 argumenty)
print(x[0], x[1], x[2])  # równoważny zapis
```

```bash
[1, 2, 3]
1 2 3
1 2 3
```

## *unzip* i *splat*

---

```py
lista = [1, 2, 3, 4, 5]

# a, b = lista  # ValueError: too many values to unpack (expected 2)

a, *b = lista  # a = lista[0], b = reszta

print(a, b)
```

```bash
1 [2, 3, 4, 5]
```

```py
lista = [1, 2, 3, 4, 5]

a, *b, c = lista  # a, b[0], b[1], b[2], c

print(a, b, c)
```

```bash
1 [2, 3, 4] 5
```

## "Pakowanie" (*zip*)

---


```py
x = [1, 2, 3]
y = ['a', 'b', 'c']

zipped = zip(x, y)  # pary (x[i], y[i])

print(*zipped)
```

```bash
(1, 'a') (2, 'b') (3, 'c')
```

```py
x = [1, 2, 3]
y = ['a', 'b', 'c', 'd']  # długość nie ma znaczenia

zipped = zip(x, y)  # pary (x[i], y[i])

print(*zipped)
```

```bash
(1, 'a') (2, 'b') (3, 'c')
```

## *zip* / *unzip* - test

---

```py
x = [1, 2, 3]
y = [4, 5, 6]

# pakujemy rozpakowaną paczkę
x_copy, y_copy = zip(*zip(x, y))

# i otrzymujemy znowu te same listy
x == list(x_copy) and y == list(y_copy)
```

```bash
True
```

```py
# jak to działa krok po kroku
print(list(zip(x,y)))         # lista par i-tych elementów
print(*zip(x,y))              # rozpakowana lista
print(list(zip(*zip(x, y))))  # parujemy i-te elementy
```

```bash
[(1, 4), (2, 5), (3, 6)]
(1, 4) (2, 5) (3, 6)
[(1, 2, 3), (4, 5, 6)]
```

## Pętla *for* z indeksami

---

```py
lista = ['a', 'b', 'c']
```

```py
# pętla po indeksach od 0 do N-1
for i in range(len(lista)):
    print(str(i+1) + '.', lista[i])
```

```py
# pętla po spakowanych indeksach i elementach listy
for i, element in zip(range(len(lista)), lista):
    print(str(i+1) + '.', element)
```

```py
# pętla po spakowanych indeksach i elementach listy z użyciem enumerate
for i, element in enumerate(lista):
    print(str(i+1) + '.', element)
```

```
1. a
2. b
3. c
```

#

## Formatowanie tekstu

---

```py
help(print)
```

```bash
Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.
```    


## *sep* i *end*

---


```py
a, b, c = 1, 2, 3

print(a, b, c)           # domyślnym separatorem jest spacja
```

```bash
1 2 3
```

```py
print(a, b, c, sep='_')  # ale można go zmiennić
```

```bash
1_2_3
```

```py
# domyślnie print kończy sekwencję nową linią, ale można to zmienić
print(a, b, c, sep="...", end=" koniec")
```

```
1...2...3 koniec
```

## *format* - podstawy

---

```py
x = 2

print("x jest równe " + str(x))  # skuteczne, ale mało wygodne
```

```bash
x jest równe 2
```

```py
x = 2

# klasa string ma metodę format
print("x jest równe {}".format(x))
```

```bash
x jest równe 2
```

```py
# która w miejsce {} wstawia kolejne argumenty
print("x jest równe {}, a x**2 = {}".format(x, x**2))
```

```bash
x jest równe 2, a x**2 = 4
```

## *format* - kolejność

---

```py
x = 2
y = 2.5
z = "trzy"

# domyślnie pod {} wstawiane są kolejne argument format
print("x, y, z = {}, {}, {}".format(x, y, z))
```

```bash
x, y, z = 2, 2.5, trzy
```

```py
# ale kolejność można zmienić
print("x, y, z = {2}, {0}, {1}".format(x, y, z))
```

```bash
x, y, z = trzy, 2, 2.5
```

## *format* - deklaracja typu

---


```py
x = 1234567890
y = 1234567890.1234567890
z = "Python"

# z reguły nie ma potrzeby jawnej deklaracji typu
print("x, y, z = {}, {}, {}".format(x, y, z))
```

```bash
x, y, z = 1234567890, 1234567890.1234567, Python
```


```py
# ale można to zrobić: d - int; f - float; s - str
print("x, y, z = {:d}, {:f}, {:s}".format(x, y, z))
```

```bash
x, y, z = 1234567890, 1234567890.123457, Python
```


```py
# e - wygodny format dla dużych liczb: XeY = X * 10^Y
print("x, y, z = {:f}, {:e}, {}".format(x, y, z))
```

```bash
x, y, z = 1234567890.000000, 1.234568e+09, Python
```

## *format* - dokładność

---


```py
from math import pi

print("pi = {}".format(pi))
```

```bash
pi = 3.141592653589793
```

```py
# ograniczamy się do dwóch liczb po przecinku
print("pi = {:.2f}".format(pi))
```

```bash
pi = 3.14
```

```python
# ograniczamy się do 50 liczb po przecinku
# zwróć uwagę na zera na końcu
print("pi = {:.50f}".format(pi))
```

```bash
pi = 3.14159265358979311599796346854418516159057617187500
```

## *format*  - keyword arguments

---


```py
# żeby się nie pogubić, warto "tagować" kolejne argumenty
print("{student} otrzymał {ocena}".format(student="Jan Nowak", ocena=5))
```

```bash
Jan Nowak otrzymał 5
```

```py
# wtedy kolejność nie ma znaczenia
print("{student} otrzymał {ocena}".format(ocena=5, student="Jan Nowak"))
```

```bash
Jan Nowak otrzymał 5
```

## 

```py
# lista studentów
studenci = ["Kasia", "Basia", "Marek", "Józek"]
# każdy element odpowiada liście ocen danego studenta
dziennik = [[3, 4, 5], [], [5, 3], [3, 2, 2, 2, 2]]

# [znak]^N -> centruj w szerokości N wypełniając [znakiem]
print("{:-^42}".format("OCENY"), end="\n\n")

# enumerate zwraca dwa obiekty: index i parę: (student, oceny)
for i, (student, oceny) in enumerate(zip(studenci, dziennik)):
    # policz średnią; chyba że brak ocen
    if len(oceny):
        srednia = sum(oceny) / len(oceny)
    else:
        srednia = 0

    # {oceny:<15} działa jak ljust; {oceny:>15} działa jak rjust
    print("{index}. {imie}: {oceny:<15} => srednia = {srednia:.1f}"
          .format(index=i+1,
                  imie=student,
                  oceny=str(oceny),
                  srednia=srednia))
```

```bash
------------------OCENY-------------------

1. Kasia: [3, 4, 5]       => srednia = 4.0
2. Basia: []              => srednia = 0.0
3. Marek: [5, 3]          => srednia = 4.0
4. Józek: [3, 2, 2, 2, 2] => srednia = 2.2
```

#

## Słownik (`dict`)

---

* mapuje obiekty hashowalne (*hashable*) w dowolne obiekty, czyli: *klucz: wartość*
    * *klucz* - stały hash
    * *wartość* - dowolny obiekt
* np. krotka może być kluczem, ale lista już nie
* słowniki tworzymy umieszczając oddzielone przecinkiem pary *key: value* w nawiasach klamrowych, np.


```py
# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

print(slownik)
```

```bash
{'Kasia': 7236, 'Basia': 5286, 'Darek': 7738, 'Marek': 9807}
```

## Słownik przez konstruktor

---

```py
# {key1: value1, key2: value2...}
a = {"jeden": 1, "dwa": 2, "trzy": 3}

# dict(key1=value1, key2=value2...)
b = dict(jeden=1, dwa=2, trzy=3) 

# dict([(key1, value1), (key2, value2)...])
c = dict(zip(["jeden", "dwa", "trzy"], [1, 2, 3]))

# dict(słownik)
d = dict(a)

a == b == c == d
```

```bash
True
```

## Słownik - dostęp do wartości

---

```py
# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

slownik["Kasia"]  # dostęp -> dict[key]
```

```
7236
```

```py
slownik[0]  # słownik nie jest uporządkowany
```

```bash
---------------------------------------------------------------------------

KeyError                                  Traceback (most recent call last)

<ipython-input-4-8f2cb9210d58> in <module>()
----> 1 slownik[0] # słownik nie jest uporządkowany


KeyError: 0
```

## Słowniki - *KeyError*

---

```py
# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

print(slownik["Kasia"])  # Kasia jest w słowniku -> OK
print(slownik["Ania"])   # Ani nie ma -> KeyError
```

```
7236
---------------------------------------------------------------------------

KeyError                                  Traceback (most recent call last)

<ipython-input-5-7f55cd27f397> in <module>()
        3 
        4 print(slownik["Kasia"]) # Kasia jest w słowniku -> OK
----> 5 print(slownik["Ania"])  # Ani nie ma -> KeyError


KeyError: 'Ania'
```

## Słowniki - `get`

---


```py
# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

print(slownik.get("Kasia"))       # Kasia jest w słowniku -> OK
print(slownik.get("Ania"))        # Ani nie ma -> default = None
print(slownik.get("Ania", 1234))  # Ani nie ma -> default = 1234
```

```bash
7236
None
1234
```

```py
# czemu domyślnie None?
if slownik.get("Ania"):
    print(slownik["Ania"])
else:
    print("Brak studenta.")

# lub prościej: `print(slownik.get("Ania") or "Brak studenta.")`
```

```bash
Brak studenta.
```

## Słownik - klucze i wartości

---


```py
# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}
```

```py
slownik.keys()    # lista kluczy
```

```bash
dict_keys(['Kasia', 'Basia', 'Darek', 'Marek'])
```

```py
slownik.values()  # lista wartości
```

```bash
dict_values([7236, 5286, 7738, 9807])
```

```py
slownik.items()   # lista par
```

```bash
dict_items([('Kasia', 7236), ('Basia', 5286), ('Darek', 7738), ('Marek', 9807)])
```


## Słownik - Python 2 vs 3

---

- w Pythonie 2: `dict.keys()`, `dict.values()` i `dict.items()` zwracają listy (czyli dopuszczalne jest np. `dict.keys()[0]`)
- w Pythonie 3:


```py
import collections # for Iterable

# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

# slownik.keys()[0] # TypeError: 'dict_keys' object does not support indexing

isinstance(slownik.keys(), list)
```

```bash
False
```

```py
isinstance(slownik, collections.Iterable)  # pętla po keys() -> OK
```

```bash
True
```

## Słownik - modyfikacja kluczy

---

```py
# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

slownik["Kasia"] = 1234  # dict[key] = value

print(slownik)
```

```
{'Kasia': 1234, 'Basia': 5286, 'Darek': 7738, 'Marek': 9807}
```

```py
slownik["Kasia"] += 1    # analogicznie do listy: list[index]

print(slownik)
```

```bash
{'Kasia': 1235, 'Basia': 5286, 'Darek': 7738, 'Marek': 9807}
```

## Słownik - usuwanie kluczy

---

```python
# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

del slownik["Marek"]  # del dict[key] -> usuń klucz

print(slownik)
```

```bash
{'Kasia': 7236, 'Basia': 5286, 'Darek': 7738}
```


```py
slownik.clear()  # wyczyść słownik
 
print(slownik)
```

```bash
{}
```

## Słownik - dodawanie kluczy

---


```py
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

slownik["Ania"] = 3384  # jeśli jest to zmień, jeśli nie ma to dodaj
print(slownik)
```

```bash
{'Kasia': 7236, 'Ania': 3384, 'Basia': 5286, 'Darek': 7738, 'Marek': 9807}
```

```py
nowi_studenci = {"Romek": 3343, "Basia": 8573}

slownik.update(nowi_studenci)  # "dodaj/scal" słowniki
print(slownik)                 # zwróć uwagę na Basię
```

```bash
{'Basia': 8573, 'Romek': 3343, 'Darek': 7738, 'Kasia': 7236, 'Ania': 3384, 'Marek': 9807}
```

```py
slownik.update(Józek=2276)
print(slownik)
```

```bash
{'Basia': 8573, 'Romek': 3343, 'Darek': 7738, 'Józek': 2276, 'Kasia': 7236, 'Ania': 3384, 'Marek': 9807}
```

## Pętla po słowniku

---

```py
# student: numer indeksu
slownik = {"Kasia": 7236, "Basia": 5286, "Marek": 9807, "Darek": 7738}

for student in slownik.keys():          # pętla po kluczach
    print(student, end=' ')
```

```bash
Kasia Basia Darek Marek 
```

```py
for index in slownik.values():          # pętla po wartościach
    print(index, end=' ')
```

```bash
7236 5286 7738 9807 
```

```py
for student, index in slownik.items():  # pętla po (klucz, wartość)
    print(student, index)
```

```bash
Kasia 7236
Basia 5286
Darek 7738
Marek 9807
```

## Przykład - tworzenie słownika

---


```py
studenci = {}  # stwórz pusty słownik

while True:
    # pobierz imię studenta
    student = input("Imię: ")
    # przerwij jeśli puste
    if not student: break  # niezalecane, ale możliwe w jednej linii
    # pobierz numer indeksu
    index = input("Nr indeksu: ")
    # aktualizuj słownik
    studenci.update({student: index})
    
print(studenci)
```

```bash
Imię: Kasia
Nr indeksu: 1234
Imię: Jasiu
Nr indeksu: 0987
Imię: 
{'Kasia': '1234', 'Jasiu': '0987'}
```

## Słownik w słowniku

---

```python
Kasia = {"Wiek": 20, "Wzrost": 190, "Waga": 70}
Marek = {"Wiek": 22, "Wzrost": 180, "Waga": 80}

# klucz musi być hashowalny
# wartością może być dowolny obieky, np. słownik
studenci = {"Kasia": Kasia, "Marek": Marek}

# wydrukuj w pętli wszystkich studentów i ich atrybuty
for imie, wlasnosci in studenci.items():
    print("{student} ma {wiek} lat, "
          "{wzrost} cm wzrostu "
          "i waży {waga} kg.".format(
            student=imie,
            wiek=studenci[imie]["Wiek"],
            wzrost=studenci[imie]["Wzrost"],
            waga=studenci[imie]["Waga"])
          )
```

```bash
Kasia ma 20 lat, 190 cm wzrostu i waży 70 kg.
Marek ma 22 lat, 180 cm wzrostu i waży 80 kg.
```