% Języki skryptowe Python
% Wykład 5

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

# 

## Funkcje

---

* funkcje (w programowaniu) to "wywoływalne bloki instrukcji"
* mogą (ale nie muszą) przyjmować argumenty
* mogą (ale nie muszą) zwracać obiekt
* raz napisana funkcja może być wykorzystywana wiele razy
* zwiększają czytelność kodu
* łatwiejsze debugowanie

## Definiowanie funkcji

---

```py
def nazwa_funkcji(argumenty):
    instrukcje
    ...
    return obiekt
```

1. słowo kluczowe *def*
2. nazwa funkcji
3. lista argumentów (opcjonalnie)
4. dwukropek
5. (wcięte) instrukcje
6. słowo kluczowe *return* (opcjonalnie)

## Funkcja "Hello World"

---


```python
def hello():  # brak argumentów
    print("Hello World!")
    # nic nie zwraca
    
hello()  # wywołanie funkcji
```

```bash
Hello World!
```

## Argumenty funkcji

---


```python
# funkcja dzialanie przyjmuje trzy argumenty a, b i c
# następnie zwraca wyrażenie a + b - c
def dzialanie(a, b, c):
    return a + b - c
```

```python
dzialanie(1, 2, 3)  # zwróci 1 + 2 - 3
```

```bash
0
```

```python
x = 1
y = 2

# c = 2*x + 3*y
dzialanie(x, y, 2*x + 3*y)  # zwróci 1 + 2 - 2*1 - 3*2 
```

```bash
-5
```

## Przykład

---

```python
def pobierz(komunikat):  # funkcja przyjmuje jeden argument
    user_input = input(komunikat.ljust(20))
    return user_input    # zwraca dane użytkownika

# raz zdefiniowaną funkcję możemy wykorzystać wielokrotnie
imie = pobierz("Jak masz na imię?")  # komunikat = "Jak masz na imię?"
wiek = pobierz("Ile masz lat?")      # komunikat = "Ile masz lat?"

print(imie, wiek)
```

```bash
Jak masz na imię?   Józek
Ile masz lat?       20
Józek 20
```

## Argumenty ze słowem kluczowym

---

```python
# funkcja dzialanie przyjmuje trzy argumenty a, b i c
# następnie zwraca wyrażenie a + b - c
def dzialanie(a, b, c):
    return a + b - c
```

```py
dzialanie(1, 2, 3)        # 3 argumenty pozycyjne
```

```bash
0
```

```python
dzialanie(a=1, b=2, c=3)  # 3 argumenty kluczowe
```

```bash
0
```

```python
dzialanie(b=2, c=3, a=1)  # kolejność nieważna dla argumentów kluczowych
```

```bash
0
```

## Mieszanie argumentów

---

```python
# funkcja dzialanie przyjmuje trzy argumenty a, b i c
# następnie zwraca wyrażenie a + b - c
def dzialanie(a, b, c):
    return a + b - c
```

```python
dzialanie(1, c = 3, b = 2)  # jeden pozycyjny, dwa kluczowe
```

```bash
0
```

```python
dzialanie(a = 1, b = 2, 3)  # najpierw pozycyjne, potem kluczowe!
```

```bash
File "<ipython-input-38-60286ad5b769>", line 1
 dzialanie(a = 1, b = 2, 3) # najpierw pozycyjne, potem kluczowe!
                               ^
SyntaxError: positional argument follows keyword argument
```

## Domyślne wartości argumentów

---

```python
def pobierz(komunikat):            # funkcja przyjmuje jeden argument
    user_input = input(komunikat)  # pobiera dane od użytkownika
    return user_input              # i je zwraca
```

```python
x = pobierz() # funkcja oczekuje argumentu "komunikat"
```

```bash
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)

<ipython-input-40-6184fdb92a47> in <module>()
----> 1 x = pobierz() # funkcja oczekuje argumentu "komunikat"
    
TypeError: pobierz() missing 1 required positional argument: 'komunikat'
```

## Domyślne wartości argumentów

---

```python
def pobierz(komunikat='> '):       # domyślna wartość = "> "
    user_input = input(komunikat)  # pobiera dane od użytkownika
    return user_input              # i je zwraca
```

```python
x = pobierz()  # brak argumentu -> domyślna wartość
```

```bash
> 
```

```python
x = pobierz("Napisz coś: ")  # nadpisanie wartości domyślne
```

```
Napisz coś: 
```

## Domyślne wartości argumentów

---

```python
# dwa ostatnie argumenty mają wartości domyślne
def dzialanie(a, b=2, c=3):
    return a + b - c
```

```python
dzialanie(1, 2, 3) == dzialanie(1)
```

```bash
True
```

```python
# argumenty bez wartości domyślnych nie mogą występować po tych
# które wartości domyśne posiadają
def dzialanie(a=1, b, c):
    return a + b - c
```

```bash
File "<ipython-input-46-21b67a48022e>", line 4
 def dzialanie(a=1, b, c):
                     ^
SyntaxError: non-default argument follows default argument
```

#

## Argumenty "niemutowalne"

---

```python
def zwieksz(x):
    print("wewnątrz funkcji (przed) id(x) =", id(x))
    x += 1
    print("wewnątrz funkcji (po) id(x)=", id(x))

x = 0  # zmienna x wskazuje na dany obszar pamięci

print("Przed zwiększeniem x =", x)
print("id(x) = ", id(x))

zwieksz(x)

print("id(x) = ", id(x))
print("Po zwiększeniu x =", x)
```

```bash
Przed zwiększeniem x = 0
id(x) =  140266666990080
wewnątrz funkcji (przed) id(x) = 140266666990080
wewnątrz funkcji (po) id(x)= 140266666990112
id(x) =  140266666990080
Po zwiększeniu x = 0
```

## Argumenty "mutowalne"

---

```python
def zwieksz(x):
    print("wewnątrz funkcji (przed) id(x) =", id(x))
    x[0] += 1
    print("wewnątrz funkcji (po) id(x) () =", id(x))

x = [0]  # zmienna x wskazuje na dany obszar pamięci

print("Przed zwiększeniem x =", x)
print("id(x) = ", id(x))

zwieksz(x)

print("id(x) = ", id(x))
print("Po zwiększeniu x =", x)
```

```bash
Przed zwiększeniem x = [0]
id(x) =  140266455152520
wewnątrz funkcji (przed) id(x) = 140266455152520
wewnątrz funkcji (po) id(x) () = 140266455152520
id(x) =  140266455152520
Po zwiększeniu x = [1]
```

## "Mutowalna" wartość domyślna

---

```python
# wartość domyślna jest inicjowana tylko raz
def update(N, L = []):
    L.append(N)
    return L

print(update(1))  # L wskazuje na obszar w pamięci
print(update(2))  # i tak już zostaje
print(update(3))  # dla każdego kolejnego wywołania
```

```bash
[1]
[1, 2]
[1, 2, 3]
```

## Obejście problemu

---

```python
# jeśli chcemy, aby wywołanie update bez argumentu L iniciowało nową listę
# musimy to zrobić "ręcznie"
def update(N, L = None):
    if not L:
        L = []
    L.append(N)
    return L

print(update(1))  # z każdym wywołaniem funkcji
print(update(2))  # tworzona jest nowa lista
print(update(3))
```

```bash
[1]
[2]
[3]
```

#

## Dowolna liczba argumentów (pozycyjnych)

---

```python
# funkcja przyjmuje dwa "normalne" argumenty; z pozostałych powstanie krotka
def funkcja(arg1, arg2, *args):
    print(arg1, arg2, args)

funkcja('a', 'b', 'c', 'd', 'e', 'f')
```

```bash
a b ('c', 'd', 'e', 'f')
```

## *args i key

---

```python
# po *args mogą występować tylko argumenty kluczowe
# mogą (ale nie muszą) mieć wartości domyślne
def funkcja(arg1, *args, kwarg1, kwarg2="key"):
    print("arg1 =", arg1)
    print("*args =", args)
    print("kwarg1 =", kwarg1)
    print("kwarg2 =", kwarg2)
    
funkcja('a', 'b', 'c', 'd', kwarg1="argument kluczowy")
```

```bash
arg1 = a
*args = ('b', 'c', 'd')
kwarg1 = argument kluczowy
kwarg2 = key
```

```python
funkcja('a', 'b', 'c', 'd')
```

```bash
...    
TypeError: funkcja() missing 1 required keyword-only argument: 'kwarg1'
```

## Przykład

---

```python
# średnia z dowolnej liczby argumentów
def srednia(*args):
    if not args:  # brak argumentów -> 0
        return 0
    return sum(args) / len(args)
```

```python
srednia()
```

```bash
0
```

```python
srednia(1, 2, 3, 4)
```

```bash
2.5
```

```python
srednia(*range(100))
```

```bash
49.5
```

#

## Dowolna liczba argumentów (kluczowych)

---

```python
# *args -> krotka argumentów pozycyjnych
# **kwargs -> słownik argumentów kluczowych
def funkcja(**kwargs):
    for key, value in kwargs.items():
        print(key, value, type(value))
```

```python
funkcja(imie="Jan", nazwisko="Kowalski", wiek=25)
```

```bash
imie Jan <class 'str'>
wiek 25 <class 'int'>
nazwisko Kowalski <class 'str'>
```

```python
funkcja("Jan", "Kowalski", 25)
```

```bash
...    
TypeError: funkcja() takes 0 positional arguments but 3 were given
```

## Forsowanie argumentów kluczowych

---

```python
# zwróć sumę a i b; jeśli flaga==True zwróć 0
def moja_suma(a, b, flaga=False):
    if flaga:
        return 0
    else:
        return a + b
```

```python
moja_suma(1, 2)     # dla dwóch argumentów działa OK
```

```bash
3
```

```python
moja_suma(1, 2, 3)  # flaga == 3
```

```bash
0
```


## Forsowanie argumentów kluczowych

---


```python
# zwróć sumę a i b; jeśli flaga==True zwróć 0
# *args wymusza, aby flaga byłą argumentem kluczowym
def moja_suma(a, b, *args, flaga=False):    
    if flaga:
        return 0
    else:
        return a + b
```

```python
moja_suma(1, 2)
```

```bash
3
```

```python
moja_suma(1, 2, 3)  # args=(3)
```

```bash
3
```

```python
moja_suma(1, 2, flaga=True)
```

```
0
```

## Forsowanie argumentów kluczowych

---

```python
# zwróć sumę a i b; jeśli flaga==True zwróć 0
def moja_suma(a, b, *, flaga=False):    
    if flaga:
        return 0
    else:
        return a + b
```

```python
moja_suma(1, 2)
```

```bash
3
```

```python
moja_suma(1, 2, 3)  # nadmiarowy argument wywołuje błąd
```

```bash
...
TypeError: moja_suma() takes 2 positional arguments but 3 were given
```

## Przykład

---

```python
def create_car(marka, model, **options):
    print(marka, model)
    for opcja, wartosc in options.items():
        print("  {}: {}".format(opcja, wartosc))
```

```python
create_car("Fiat", "126p", kolor="czarny", rocznik=1980)
create_car("Ford", "Mustang", kolor="różowy", moc="200KM", skrzynia="manualna")
```

```bash
Fiat 126p
    kolor: czarny
    rocznik: 1980
Ford Mustang
    moc: 200KM
    kolor: różowy
    skrzynia: manualna
```

## Argumenty ze słownika

---

```python
def create_car(marka, model, **options):
    print(marka, model)
    for opcja, wartosc in options.items():
        print("  {}: {}".format(opcja, wartosc))
        
ford_mustang = {"kolor": "różowy", "moc": "200KM", "skrzynia": "manualna"}

# **dict jako argument -> rozpakuj slownik
create_car("Ford", "Mustang", **ford_mustang)
```

```bash
Ford Mustang
    moc: 200KM
    kolor: różowy
    skrzynia: manualna
```
#

## Funkcja jako rezultat funkcji

---

```python
def kwadrat(x):
    print("kwadrat({})".format(x))
    return x*x

def kwadrat_sumy(a, b):
    print("kwadrat_sumy({}, {})".format(a, b))
    return kwadrat(a + b)  # return może zwrócić inną funkcję

wynik = kwadrat_sumy(2, 3)

print("wynik =", wynik)
```

```bash
kwadrat_sumy(2, 3)
kwadrat(5)
wynik = 25
```

## Wynik funkcji jako argument funkcji

---

```python
def kwadrat(x):
    print("kwadrat({})".format(x))
    return x*x

def suma(a, b):
    print("suma({}, {})".format(a, b))
    return a + b

def kwadrat_sumy(a, b):
    print("kwadrat_sumy({}, {})".format(a, b))
    return kwadrat(suma(a, b))  # wynik funkcji jest argumentem

wynik = kwadrat_sumy(2, 3)

print("wynik =", wynik)
```

```bash
kwadrat_sumy(2, 3)
suma(2, 3)
kwadrat(5)
wynik = 25
```

## Funkcja jako argument funkcji

---

```python
def kwadrat(x):
    print("kwadrat({})".format(x))
    return x*x

def suma(a, b):
    print("suma({}, {})".format(a, b))
    return a + b

def kwadrat_sumy(a, b, f1, f2):
    print("kwadrat_sumy({}, {}, {}, {})".format(a, b, f1, f2))
    return f2(f1(a, b))

wynik = kwadrat_sumy(2, 3, suma, kwadrat)  # funkcja jest argumentem

print("wynik =", wynik)
```

```bash
kwadrat_sumy(2, 3, <function suma at 0x7f9254388d08>, <function kwadrat at 0x7f925438ed90>)
suma(2, 3)
kwadrat(5)
wynik = 25
```