* Rozwiązane zadania należy wysłać mailem na adres tomasz.golan@uwr.edu.pl nie później niż w ciągu 90 minut licząc od ropoczęcia kolokwium.

* Każde zadanie należy umieścić w osobnym pliku `imie.nazwisko.kolokwium.XX.py` gdzie `XX` to numer zadania.

* Punktacja:
  
    * db: >= 5.0 pkt
    * dst+: >= 4.0 pkt
    * dst: >= 3.0 pkt

---

# Zadanie 1 (2 pkt)

Akceptowalne przez system hasło musi spełniać wszystkie poniższe wymogi:

* musi być nie krótsze niż 8 znaków oraz nie dłuższe niż 16 znaków;
* musi zawierać co najmniej jedną małą literę;
* musi zawierać co najmniej jedną wielką literę;
* musi zawierać co najmniej dwie cyfry.

Napisz program do walidacji haseł, który sprawdza poprawność hasła wprowadzonego przez użytkownika (ze standardowego wejścia).

*Uwaga: program powinien prosić o podanie hasła tak długo, aż zostanie podane poprawne.*

# Zadanie 2 (2 pkt)

W pliku `https://tomaszgolan.github.io/wfia_python/data/studenci.txt` znajduje się lista studentów w formacie:

```
[Imię] [Nazwisko], [Numer Indeksu]
```

W pliku `https://tomaszgolan.github.io/wfia_python/data/oceny.txt` znajduje się lista ocen studentów w formacie:

```
[Numer Indeksu]: [lista ocen oddzielonych przecinkiem]
```

Napisz program, który (na podstawie dwóch powyższych plików) liczy średnią ocen każdego student i zapisuje je w trzecim pliku w formacie:

```
[Imię] [Nazwisko]: [średnia ocen]
```

Przykład:

* `studenci.txt`

```
Jan Nowak, 1234
Anna Kowalska, 1111
```

* `oceny.txt`

```
1111: 3, 5
1234: 2, 3, 4, 5
```

* `oceny_studentow.txt` (kolejność dowolna)

```
Jan Nowak: 3.5
Anna Kowalska: 4
```

*Uwaga: w przypadku braku ocen należy przyjąć, że średnia = 0.*

# Zadanie 3 (2 pkt)

Niech *v1* oznacza prędkość samochodu wyruszającego z miasta *A* w kierunku miasta *B*, a *v2* prędkość samochodu wyruszającego z miasta *B* w kierunku miasta *A*. *Uwaga: należy założyć, że samochody poruszają się ruchem jednostajnym prostoliniowym.*

Napisz program, który dla zadanych *v1*, *v2* oraz *x* (odległość między miastami *A* i *B*) wyznacza czas (*t*), po którym samochody się spotkają oraz w jakiej odległości (*s*) od miasta *A* to nastąpi.

Program powinien przyjmować dane jako argumenty wywołania i działać w dwóch trybach:

* program wywołany z trzema argumentami (*v1*, *v2* i *x*) powinien drukować wyznaczone *t* oraz *s*;
* program wywołany z czterema argumentami (*v1*, *v2*, *x* oraz *dt*) powinien dodatkowo drukować odległość między samochodami co *dt*.

Program powinien przerywać działanie i drukować stosowny komunikat, jeśli podane dane są nieprawidłowe.




