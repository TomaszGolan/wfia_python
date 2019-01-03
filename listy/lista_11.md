# Lista 11

## Zadanie 1 (5 pkt)

W pliku `prostokat.py` stwórz klasę `Prostokat`, która:

* przyjmuje długości boków przez funkcję `__init__`, np. `p = Prostokat(3, 4)`
* przyjmuje, że prostokat jest kwadratem, jeśli podany zostanie jeden argument, np. `p = Prostokat(2)`
* posiada metodę, która liczy i zwraca pole prostokąta
* posiada metodę, która liczy i zwraca obwód prostokąta
* posiada metodę, która liczy i zwraca długość przekątnych prostokąta
* posiada zdefiniowanę metodę specjalną `__str__` taką, że

```py
from prostokat import Prostokat

p = Prostokat(3, 4)
print(p)
```

wydrukuje na ekranie:

```
Prostokąt o bokach 3 i 4:

-> obwód = 14
-> pole = 12
-> przekątna = 5.0
```

## Zadanie 2 (5 pkt)

Stwórz klasę `CiagGeometryczny`, która

* wymaga podanie trzech danych przy inicjalizacji (*a1* - pierszy wyraz ciągu, *q* - iloraz, i *n* - początkowo liczba wyrazów ciągu)
* początkowo przechowuje *n* pierwszych wyrazów ciągu
* posiada metodę *add*, która dodaje kolejny wyraz ciągu
* ma zdefiniowane odpowiednie metody specjalne tak, aby:
    * *print* wywołane na obiekcie klasy drukowało wyrazy ciągu
    * *sum* wywołane na obiekcie klasy zwracało sumę wyrazów ciągu
    * *len* wywołane na obiekcie klasy zwracało liczbę wyrazów ciągu

## Zadanie 3 (5 pkt)

Napisz klasę do konwersji liczb na system rzymski. Klasa powinna zawierać:

* *konstruktor* inicjowany liczbą całkowitą z domyślna wartością 0
* metodę, która konwertuje liczbę całkowitą na system rzymski
* wywołanie funkcji `print` na obiekcie powinno drukować na ekranie informacje o liczbie, np.

```
Liczba 10 w systemie rzymskim to X.
```

* metodę, która umożliwia zmianę liczby.