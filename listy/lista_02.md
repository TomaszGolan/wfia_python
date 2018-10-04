# Lista 2

> Każde zadanie należy umieścić w osobnym pliku `imie.nazwisko.XX.YY.py` gdzie `XX` to numer listy a `YY` numer zadania. 

---

## Zadanie 1 (1 pkt)

Napisz skrypt, który wykona następujące czynności:

* zmiennej `a` przypisze wartość `5`
* zmiennej `b` przypisze wartość `3`
* zmiennej `P` przypisze wartość `a*b`
* wypisze na ekranie "Pole prostokąta o bokach `a` i `b` wynosi `P`." (gdzie w miejsce zmiennych zostaną wstawione odpowiednie wartości).

Wskazówka:

```py
x = 2
print(f"Zmienna = {x}")         # Python >= 3.6 lub
print("Zmienna = {}".format(x))
```

---

## Zadanie 2 (2 pkt)

* Stwórz krotkę (*tuple*) zawierającą pięć cyfr: `0, 1, 2, 3, 4` oraz pięć literałów słownych: `"pięć", "sześć", "siedem", "osiem", "dziewięć"`.

* Wydrukuj na ekranie trzy pierwsze elementy.

* Wydrukuj na ekranie 2 ostatnie elementy.

* Wydrukuj co drugi element (zaczynając od drugiego).

* Korzystając z funkcji `len` sprawdź ilość elementów w krotce oraz długość przedostatniego elementu.

* Niech `x` oznacza nazwę krotki. Wykonaj:

    * `x[:5] + (5, 6) + x[-3:]`
    * `x[:5], (5, 6), x[-3:]`
    * porównaj (i wyjaśnij) otrzymane wyniki

* Dodaj pusty literał słowny na koniec krotki. Czy możesz skorzystać z funkcji `append` (wyjaśnij)?

---

## Zadanie 3 (1 pkt)

* Stwórz listę studentów: Kasia, Basia, Marek, Darek.

* Korzystając z funkcji `append` dodaj do listy Józka.

* Korzystając z funkcji `extend` dodaj do listy Anię i Basię.

* Posortuj alfabetycznie studentów.

* Wypisz na ekranie:

    * czwartego studenta na liście
    * dwóch pierwszych studentów na liście
    * dwóch ostatnich studentów na liście

* Korzystając z funkcji `remove` usuń wszystkie Basie.

* Korzystając z funkcji `len` sprawdź ilość studentów.

* Z ostatecznej listy studentów utwórz krotkę.

---

## Zadanie 4 (1 pkt)

* Stwórz krotkę: `('a', 'b', 'c', 'd')`.

* Zapoznaj się z dokumentacją funkcji `str.join`.

* Wykonaj następujące polecenia (gdzie `x` to zmienna wskazująca na krotkę):

```py
"".join(x)
" ".join(x)
", ".join(x)
```

* Korzystając z funkcji `join` wydrukuj (jednolinijkową komendą) na ekranie 100 zer oddzielonych tabulacjami.

---

## Zadanie 5 (2 pkt)

* Stwórz obiekt typu `str`, który przechowuje tekst ślubowania studenta:

```py
slubowanie = """
wstępując do wspólnoty akademickiej Uniwersytetu Wrocławskiego, ślubuję uroczyście:
- zdobywać wiedzę i umiejętności,
- postępować zgodnie z prawem, tradycją i dobrymi obyczajami akademickimi,
- dbać o dobre imię Uniwersytetu Wrocławskiego i godność studenta.
"""
```

* W interpreterze sprawdź wynik:

```
>>> print(slubowanie)
>>> slubowanie
>>> slubowanie[0]
```

* Popraw zmienną `slubowanie`, aby tekst zaczynał się wielką literą.

* Korzystając z funkcji `count` sprawdź, ile razy występuje spójnik "i".

* Korzystając z funkcji `count` sprawdź, ile razy występuje litera "i".

* Korzystając z `in` sprawdź, czy słowo "Uniwersytet" występuje w tekście.

* Korzystając z funkcji `str.split`:

    * stwórz listę wyrazów występujących w tekście (30 słów => 30 elementów)
    * stwórz listę, której każdy element odpowiada jednej linijce tekstu (4 linie => 4 elementy)

---

## Zadanie 6 (1 pkt)

* Korzystając z `range` utwórz listę zawierającą wszystkie wielokrotności liczby 3 mniejsze od 100.

* Korzystając z `del` usuń co trzeci element (zaczynając od piątego).

* Sprawdź definicję funkcji wbudowanej `sum`. Wykorzystaj ją, aby wyliczyć średnią arytmetyczną otrzymanej listy.

---

## Zadanie 7 (3 pkt)

Warunki zostaną omówione na kolejnym wykładzie. Na potrzeby tego zadania wykorzystaj podstawową składnię:

```py
if [warunek]:
    [polecenie]  # wykonane jeśli warunek jest spełniony
else:
    [polecenie]  # wykonane jeśli warunek nie jest spełniony
```

Niech 

```py
lista_studentow = ("Kasia", "Basia", "Marek", "Darek")
```

Napisz program, który pobierze od użytkownika imię studenta, a następnie wydrukuje na ekranie informację, czy student znajduje się na liście. Program powinien ignorować wielkości liter.

---

## Zadanie 8 (1 pkt)

Napisz skrypt, który pobiera od użytkownika ciąg znaków, a następnie drukuje na ekranie informację, czy podano liczbę naturalną (wsk. `help(str)`).

---

## Zadanie 9 (3 pkt)

Napisz program, który:

* pobiera od użytkownika sekwencję liczb całkowitych oddzielonych przecinkiem (np. "4, 19, 2, 57")
* konwertuje pobrany literał na listę (`["4", "19", "2", "57"]`)
* konwertuje listę literałów na listę liczba całkowitych (np. `[4, 19, 2, 57]`), *wsk. lista składana*
* drukuje na ekranie pełne działanie dodawania i wynik: `4 + 19 + 2 + 57 = 82`