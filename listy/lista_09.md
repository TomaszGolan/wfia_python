# Lista 9

## Zadanie 1 (3 pkt)

Napisz program `read.py`, który przyjmuje argumenty z linii komend:

```bash
read.py file [mode]
```

gdzie `file` (ścieżka do pliku) jest argumentem obowiązkowym, a `[mode]` opcjonalnym.

Program powinien drukować na ekranie podany plik w zadanym trybie:

* mode=0 (domyślnie) - drukuje cały plik
* mode=1 - pomija linie zaczynające się od # (komentarze)
* mode=2 - numeruje linie, czyli

```
1. pierwsza linia z pliku
2. druga linia z pliku
...
```

*Uwaga: program powinien zwracać stosowny komunikat, gdy argument obowiązkowy nie zostanie podany*

---

## Zadanie 2 (6 pkt)

* Stwórz moduł, który zawiera niżej wymienione funkcje:

    * konwersja Celsjusz -> Fahrenheit
    * konwersja Fahrenheit -> Celsjusz
    * generowanie N losowych temperatur w Celsjuszach

* Napisz skrypt, który wykorzystuje powyższy moduł, aby utworzyć plik `celsjusz.txt`, w którym zapisze *n* losowo wygenerowanych temperatur (w Celsjuszach).

*Uwaga: niech n będzie pobierane z linii komend; program powinien stosownie reagować, gdy podany przez użytkownika argument nie jest liczbą całkowitą;*

* Napisz skrypt, który wykorzystuje moduł z pierwszego punktu, aby wczytać plik `celsjusz.txt`, a następnie utworzyć odpowiadający mu plik `fahrenheit.txt`, w którym zapisze przekonwertowane temperatury.

* Napisz skrypt, który wykorzystuje moduł z pierwszego punktu, aby sprawdzić, czy pliki `celsjusz.txt` i `fahrenheit.txt` zawierają rzeczywiście te same temperatury, ale w innych skalach.

---

## Zadanie 3 (6 pkt)

Napisz program do zliczania, ile razy podany tekst mieści się na ekranie o zadanej szerokości i wysokości (bez dzielenie wyrazów na dwie linie).

Przykład:

```bash
liczba kolumn = 10
liczba rzędów = 3
tekst = "Ala ma kota."

Ala ma****
kota. Ala*
ma kota.**

wynik = 2
```

Program powinien:

* przyjmować 3 argumenty z linii komend: liczba kolumn, rzędów, ścieżka do pliku;

* wczytywać tekst z pliku;

* drukować tekst na ekranie wypełniając pozostałe spacje wybranym znakiem (jak * w przykładzie powyżej);

* podawać końcowy wynik.