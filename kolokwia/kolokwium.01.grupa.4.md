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


Napisz program, który dla zadanego przez użytkownika *n* (jako argument wywołania) rysuje trójkąt wg poniższego wzoru (dla *n = 5*):

\mbox{}

```
* 
* * 
* * * 
* * * * 
* * * * * 
* * * * 
* * * 
* * 
*
```

*Uwaga: program powinien stosownie reagować, gdy podane przez użytkownika dane są niepoprawne.*

---

# Zadanie 2 (2 pkt)

Robot porusza się po płaszczyźnie rozpoczynając w punkcie *(0,0)*. W każdym kroku może przesunąć się o jedno pole w dół, górę, lewo, prawo.

Napisz program, który pobiera od użytkownika (ze standardowego wejścia) sekwencję ruchów robota, np: `G G P P D D L L`, a następnie drukuje na ekranie informację o przebytej przez robota drodze oraz przemieszczeniu.

*Uwaga: program powinien stosownie reagować, gdy podane przez użytkownika dane są niepoprawne.*

---

# Zadanie 3 (2 pkt)

Napisz program, który wczytuje zawartość podanego pliku i drukuje statystykę występowania wszystkich występujących w nich słów (w kolejności alfabetycznej, pomijając wielkość liter).

Przykład: Niech `tekst.txt`:

```
Ala ma kota a Józek ma psa. Ani Ala, ani Józek nie ma Ani.
```

Program powienien wydrukować:

```
a: 1
ala: 2
ani: 3
józek: 2
kota: 1
ma: 3
nie: 1
psa: 1
```

*Uwaga: można przyjąć, że jedynymi znakami interpunkcyjnymi występującymi w tekście są: , . ? !*