* Rozwiązane zadania należy wysłać mailem do prowadzącego nie później niż w ciągu 90 minut licząc od ropoczęcia kolokwium.

* Każde zadanie należy umieścić w osobnym pliku `imie.nazwisko.kolokwium.XX.py` gdzie `XX` to numer zadania.

* Punktacja:
  
    * bdb: >= 5.0 pkt
    * db+: >= 4.5 pkt
    * db: >= 4.0 pkt
    * dst+: >= 3.5 pkt
    * dst: >= 3.0 pkt

---

# Zadanie 1 (2 pkt)

Napisz program, który dla zadanego przez użytkownika *n* (jako argument wywołania) generuje tablicę dwuwymiarową *n x n*, której elementy są iloczynem indeksów kolumny i rzędu. Np. dla *n = 4*, program powinien drukować:


```
0 0 0 0 
0 1 2 3
0 2 4 6
0 3 6 9
```

*Uwaga: program powinien stosownie reagować, gdy podane przez użytkownika dane są niepoprawne.*

---

# Zadanie 2 (2 pkt)

Niech słowo zawierające parzystą liczbę samogłosek = 2 pkt, a słowo z nieparzystą liczbą samogłosek = 1 pkt. Ocena zdania jest sumą punktów za wszystkie słowa, np.

```
Ala ma kota. = 2 + 1 + 2 = 5 pkt
```

Napisz program, który:

* zawiera funkcję, która przyjmuje pojedyncze słowo i zwraca liczbę punktów wg opisanej reguły, np:

```
f("Ala") -> 2
f("ma") -> 1
```

* zawiera funkcję, która przyjmuje tekst i zwraca sumę punktów (wykorzystując funkcję z pierwszego punktu), np.:

```
f("Ala ma kota.") -> 5
```

* pobiera od użytkownika (ze standardowego wejśćia) tekst i zwraca liczbę zdobytych punktów.

---

# Zadanie 3 (2 pkt)

Napisz program, który:

* tworzy plik zawierający 100 linii, w każdej 3 losowe liczby całkowite z przedziału `[1, 10]` oddzielone spacjami, np.

```
3 2 7
6 3 5
3 4 5
1 2 4
...
```

* następnie wczytuje stworzony plik i sprawdza, które linie zawierają długości boków, z których można zbudować trójkąt.

W podanym przykładzie program powinien wydrukować:

```
Trójkąt można zbudować z boków podanych w liniach: 2, 3.
```