# Lista 4

> Każde zadanie należy umieścić w osobnym pliku `imie.nazwisko.XX.YY.py` gdzie `XX` to numer listy a `YY` numer zadania.

---

## Zadanie 1 (3 pkt)

Napisz program, który dla podanej liczby *n* (z konsoli) generuje słownik, którego kluczami są liczby całkowite od *1* do *n*, a wartościami listy ze wszystkimi dzielnikami danej liczby.

Następnie drukuje na ekranie (dla n = 6):

```bash
Dzielnikami liczby 1 są: 1
Dzielnikami liczby 2 są: 1, 2
Dzielnikami liczby 3 są: 1, 3
Dzielnikami liczby 4 są: 1, 2, 4
Dzielnikami liczby 5 są: 1, 5
Dzielnikami liczby 6 są: 1, 2, 3, 6
```

---

## Zadanie 2 (2 pkt)

Napisz program, który dla podanego $c_0$ drukuje ciąg Collatza (aż do wystąpienia liczby 1).

---

## Zadanie 3 (2 pkt)

Napisz program, który drukuje wszystkie *podlisty* podanej listy, np.

```bash
[1, 2, 3] -> [[], [1], [1, 2], [1, 2, 3], [2], [2, 3], [3]]
```

---

## Zadanie 4 (4 pkt)

Napisz program, który pobiera od użytkownika klucz produktu (16 cyfr), następnie:

* sprawdza poprawność wprowadzonych danych (długość 16, tylko cyfry)
* konwertuje klucz do stringa w formacie *AAAA-BBBB-CCCC-DDDD*
* sprawdza, czy podany klucz jest prawidłowy (każda z otrzymanych liczb 4-cyfrowych AAAA itd. jest podzielna przez 3)

---

## Zadanie 5 (4 pkt)

Napisz program do tworzenia listy zakupów. Program w pętli powinien pytać użytkownika o nazwę produktu oraz jego cenę i zapisywać podane wartości w słowniku (koniec pętli po podaniu pustej nazwy produktu), np.

```bash
Podaj produkt: maslo
Podaj cenę: 5
Podaj produkt: mleko
Podaj cenę: 3
Podaj produkt: [enter]
```

tworzy słownik `lista_zakupow = {"maslo": 5, "mleko": 3}`. Podanie produktu, który już występuje na liście, aktualizuje cenę. Na koniec program drukuję pełną listę zakupów oraz całkowity koszt produktów:

```bash
Lista zakupów:
--------------

1. maslo, cena 5 zł
2. mleko, cena 3 zł

Do zapłaty: 8 zł
```

---

