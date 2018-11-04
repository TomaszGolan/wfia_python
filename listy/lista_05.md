# Lista 5

> Każde zadanie należy umieścić w osobnym pliku `imie.nazwisko.XX.YY.py` gdzie `XX` to numer listy a `YY` numer zadania.

---

## Zadanie 1 (1 pkt)

Napisz funkcję `generate_password(n)`, która zwraca losowo wygenerowane hasło o długości `n`. Hasło powinno składać się z liter i cyfr.

*wskazówka:*

```
import random
import string
print(string.ascii_letters)
print(string.digits)
help(random.choice)
```

## Zadanie 2 (2 pkt)

Napisz funkcję, która liczy i zwraca wyróżnik trójmianu kwadratowego.

Następnie wykorzystaj ją w programie, który pobiera od użytkownika współczynniki trójmianu kwadratowego, a następnie podaje jego rozwiązania.

---

## Zdanie 3 (2 pkt)

Napisz funkcję, która liczy i zwraca wartość wielomianu w zadanym punkcie:

$$w(x) = a_0 + a_1\cdot x + a_2\cdot x^2... + a_n\cdot x^n$$

Współczynniki $a_0, a_1, ..., a_n$ (dowolna ilość) oraz $x$ powinny być przyjmowane jako argumenty funkcji.

*Wsk: `*args`*

---

## Zadanie 4 (3 pkt)

Napisz funkcję, która rozkłada podaną liczbę na czynniki pierwsze. Następnie wykorzystaj tę funkcję do wyznaczenia największego wspólnego dzielnika oraz najmniejszej wspólnej wielokrotności dwóch liczb podanych przez użytkownika.

---

## Zadanie 5 (3 pkt)

Dany jest szyfr, który zamienia samogłoski wg klucza:

```
klucz = {"a": "y", "e": "i", "i": "o", "o": "a", "y": "e"}
```

Czyli wszystkie `a` zamienia na `y` itd. Np. tekst:

```
to jest moj tekst
```

po przepuszczeniu przez szyfr wyglądać będzie następująco:

```
ta jist maj tikst
```

Napisz funkcję do szyfrowania i deszyfrowania tekstu. Dla uproszczenia przyjmij, że szyfrowane są tylko małe litery.

Przetestuj szyfrowanie i deszyfrowanie na kilku przykładach.

*wskazówka: do deszyfrowania można użyć:* 

`deklucz = {v: k for k, v in klucz.items()}`

---

## Zadanie 6 (4 pkt)

Napisz program do analizy ruchu ciała w rzucie ukośnym. Program powinien:

* pobierać od użytkownika wartość prędkości początkowej i kąt
* drukować na ekranie poniższe informacje:
    * czas lotu
    * maksymalną wysokość
    * zasięg

Za powyższe do zdobycia 2 punkty. Dalej do wyboru:

Wersja za 1 dodatkowy punkt:

* następnie w pętli pytać użytkownika o podanie czasu $t$ i wyświetlać położenie punktu $(x(t), y(t))$
* pętla powinna się kończyć, gdy użytkownika poda $t = 0$

Wersja za 2 dodatkowe punkty:

* zapoznaj się z bilioteką `matplotlib`
* wykorzystaj ją, aby narysować wykres wykres $y(x)$