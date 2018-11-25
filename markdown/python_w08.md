% Języki skryptowe Python
% Wykład 8

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

# 

## Moduł *os*

---

* przenośne używanie funkcjonalności zależnych od systemu operacyjnego
    * operacje na plikach (o tym za tydzień)
    * operacje na ścieżkach
    * uruchamianie poleceń systemowych
    * zarządzanie zmiennymi środowiskowymi
    * ...

## System operacyjny

---


```python
import os

# POSIX = Portable Operating System Interface for Unix
print(os.name)  # posix, nt, ce, java
```

```bash
'posix'
```

```python
if os.name == "posix":  # jeśli unix
    cmd = "ls"          # użyj ls
elif os.name == "nt":   # jeśli windows
    cmd = "dir"         # użyj dir
    
print(cmd)
```

```bash
ls
```

## Katalog roboczy

---

```python
current_path = os.getcwd()  # pwd

print("Katalog roboczy:", current_path)

new_path = "/home/goran"

os.chdir(new_path)          # zmień katalog roboczy

print("Nowy katalog roboczy:", os.getcwd())

os.chdir(current_path)      # wracamy
```

```bash
Katalog roboczy: /doc/insync/scratch/zajęcia/2016/języki skryptowe - python/js-python
Nowy katalog roboczy: /home/goran
```

## Zawartość katalogu

---


```python
print(os.listdir("/usr/"))  # lista plików i katalogów
```

```bash
['src', 'local', 'bin', 'include', 'sbin', 'lib', 'games', 'share', 'locale']
```

```python
print(os.listdir())         # lista plików i katalogów w pwd
```

```bash
['my_script.py',
'usos.py',
'.ipynb_checkpoints',
'js-python_w05.html',
'js-python_w01.html',
'js-python_l02.md',
'test.2016_11_11_175921.log',
'js-python_w04.ipynb',
'js-python_w06.html',
'README.md',
'js-python_w03.html',
'test.2016_11_11_175922.log',
'js-python_l00.md',
'iloczyn.py',
'js-python_w04.html',
'temp.py',
'js-python_w03.ipynb',
'js-python_l01.pdf',
'js-python_w05.ipynb',
'print_args.py',
'src',
'js-python_l01.md',
'middle2.py',
'js-python_w01.ipynb',
'listy_zadan',
'__pycache__',
'dodaj_studentow.py',
'js-python_w07.ipynb',
'test.2016_11_11_175942.log',
'js-python_w02.ipynb',
'js-python_w02.html',
'temp',
'my_module.py',
'js-python_w06.ipynb',
'private.py']
```

## Tworzenie / usuwanie katalogów

---

```python
def check(ls, folder):
    """Sprawdza czy folder znajduje się na liście."""
    if folder in ls:
        print("{} is found.".format(folder))
    else:
        print("{} not found.".format(folder))

my_folder = "test"

check(os.listdir(), my_folder)

os.mkdir(my_folder)  # stwórz katalog test

check(os.listdir(), my_folder)

os.rmdir(my_folder)  # usuń katalog test

check(os.listdir(), my_folder)
```

```bash
test not found.
test is found.
test not found.
```

## Tworzenie / usuwanie plików

---

```python
os.mkdir("my_dir")  # stwórz katalog "my_dir"

# otwórz plik w trybie zapisu (więcej za tydzień)
file = open("my_dir/my_file", 'w')
file.close()

print(os.listdir("my_dir"))
```

```bash
['my_file']
```

```python
# nie można usunąć niepustego katalogu
os.rmdir("my_dir")
```

```bash
OSError: [Errno 39] Directory not empty: 'my_dir'
```

```python
os.remove("my_dir/my_file")  # usuń plik
os.rmdir("my_dir")           # usuń katalog
```

## Drzewo katalogów

---

```python
# os.makedirs(..., exist_ok=True) -> działa jak mkdir -p
os.makedirs("level0/level1/level2")  # utwórz "ciąg" katalogów

print(os.listdir("level0"))
```

```bash
['level1']
```

```python
print(os.listdir("level0/level1"))
```

```bash
['level2']
```

```python
# os.rmdir("level0/level1/level2")     # usunie tylko level2
os.removedirs("level0/level1/level2")  # usunie wszystko
```

## Moduł *os.path*

---


```python
import os

path = "/my/path"  # katalog
file = "file.py"   # plik

print(os.path.join(path, file))              # tworzy pełną ścieżkę do pliku
```

```bash
'/my/path/file.py'
```


```python
print(os.path.split("/my/path/file.py"))     # zwraca (head, tail)
```

```bash
('/my/path', 'file.py')
```

```python
print(os.path.dirname("/my/path/file.py"))   # zwraca split()[0]
```

```bash
'/my/path'
```

```python
print(os.path.basename("/my/path/file.py"))  # zwraca split()[1]
```

```bash
'file.py'
```

## Więcej o *os.path*

---


```python
import os.path as path

print(path.splitext("/my/path/file.py"))  # wydziela rozszerzenie pliku
```

```bash
('/my/path/file', '.py')
```

```python
my_path, my_file = path.split("/my/path/file.py")
my_base, my_extn = path.splitext(my_file)

print("my_path =", my_path)
print("my_file =", my_file)
print("my_base =", my_base)
print("my_extn =", my_extn)
```

```bash
my_path = /my/path
my_file = file.py
my_base = file
my_extn = .py
```

## Zmienne środowiskowe

---


```python
print(os.getenv("HOME"))   # pobierz wartość zmiennej środowiskowej
```

```bash
'/home/goran'
```

```python
print(os.environ["HOME"])  # environ -> słownik zmiennych środowiskowych
```

```bash
'/home/goran'
```

```python
# tworzenie zmiennej środowiskowej z poziomu pythona
os.environ["MOJA_ZMIENNA"] = "To musi być string"
```

```bash
echo $MOJA_ZMIENNA
```

```bash
To musi być string
```

#

## USOS 

---

`usos.py`

```python
"""Uniwersytecki System Obsługi Studiów

Dane przechowywane w postaci: kierunek/rok/imie.nazwisko
a w pliku zapisany jest numer indeksu
"""

import os

# top-level katalog na podstawie zmiennej środowiskowej $USOS
# jeśli nie jest zdefiniowana -> bieżący katalog
_BASE_PATH = os.getenv("USOS") or os.getcwd()
```

## Zmienna środowiskowa USOS

---

```bash
python -c "import usos; print(usos._BASE_PATH)"
```

```bash
/doc/insync/scratch/zajęcia/2016/języki skryptowe - python/js-python
```

```bash
export USOS="/moja/sciezka/do/bazy/danych"
python -c "import usos; print(usos._BASE_PATH)"
```

```bash
/moja/sciezka/do/bazy/danych
```

## USOS - dodawanie studenta

---

`usos.py`

```python
def add_student(imie, nazwisko, indeks, kierunek, rok):
    """Dodaje studenta.
    
    Tworzy plik imie.nazwisko w katalogu kierunek/rok/
    i umieszcza w nim numer indeksu
    """
    # pełna ścieżka do katalogu danego kierunku/rocznika
    path = os.path.join(_BASE_PATH, kierunek, str(rok))
    # imie.nazwisko
    file = ".".join([imie, nazwisko])
    # stwórz kierunek lub pomiń jeśli istnieje
    os.makedirs(path, exist_ok=True)
    # o plikach więcej za tydzień
    with open(os.path.join(path, file), 'w') as f:
        f.write(str(indeks))
```

## USOS - przykład

---

`dodaj_studentow.py`

```python
import usos
import random

imiona = ["Kasia", "Basia", "Marek", "Darek"]
nazwiska = ["Nowak", "Marian", "Python"]
kierunki = ["ISSP", "Fizyka Komputerowa"]

for i in range(10):
    imie = random.choice(imiona)          # losowe imie
    nazwisko = random.choice(nazwiska)    # losowe nazwisko
    indeks = random.randint(1000, 9999)   # losowy indeks
    rocznik = random.randint(2015, 2017)  # losowy rocznik
    kierunek = random.choice(kierunki)    # losowy kierunek
    
    usos.add_student(imie, nazwisko, indeks, kierunek, rocznik)
```

## USOS - wynik

---


```bash
export USOS=/home/goran/usos
python dodaj_studentow.py
tree $USOS
```

```bash
/home/goran/usos
├── Fizyka Komputerowa
│   ├── 2015
│   │   └── Marek.Python
│   ├── 2016
│   │   ├── Basia.Marian
│   │   ├── Kasia.Nowak
│   │   └── Marek.Python
│   └── 2017
│       └── Basia.Marian
└── ISSP
    ├── 2015
    │   └── Marek.Marian
    ├── 2016
    │   ├── Basia.Marian
    │   ├── Kasia.Nowak
    │   └── Kasia.Python
    └── 2017
        └── Basia.Nowak

8 directories, 10 files
```

## *os.walk*

---

```python
# os.walk "podróżuje po drzewie katalogów"
# na każdym kroku zwracając krotkę
# (obecny katalog, lista podkatalogów, lista plików)
for root, dirs, files in os.walk("/home/goran/usos"):
    print(root, dirs, files, sep="\n", end="\n\n")
```

```bash
/home/goran/usos
['Fizyka Komputerowa', 'ISSP']
[]

/home/goran/usos/Fizyka Komputerowa
['2016', '2015', '2017']
[]

/home/goran/usos/Fizyka Komputerowa/2016
[]
['Kasia.Nowak', 'Basia.Marian', 'Marek.Python']

/home/goran/usos/Fizyka Komputerowa/2015
[]
['Marek.Python']

/home/goran/usos/Fizyka Komputerowa/2017
[]
['Basia.Marian']

/home/goran/usos/ISSP
['2016', '2015', '2017']
[]

/home/goran/usos/ISSP/2016
[]
['Kasia.Python', 'Kasia.Nowak', 'Basia.Marian']

/home/goran/usos/ISSP/2015
[]
['Marek.Marian']

/home/goran/usos/ISSP/2017
[]
['Basia.Nowak']
```    


## *os.walk*

---


```python
for root, dirs, files in os.walk("/home/goran/usos"):
    for file in files: # pętla po plikach w danym katalogu root
        print(os.path.join(root, file))
```

```bash
/home/goran/usos/Fizyka Komputerowa/2016/Kasia.Nowak
/home/goran/usos/Fizyka Komputerowa/2016/Basia.Marian
/home/goran/usos/Fizyka Komputerowa/2016/Marek.Python
/home/goran/usos/Fizyka Komputerowa/2015/Marek.Python
/home/goran/usos/Fizyka Komputerowa/2017/Basia.Marian
/home/goran/usos/ISSP/2016/Kasia.Python
/home/goran/usos/ISSP/2016/Kasia.Nowak
/home/goran/usos/ISSP/2016/Basia.Marian
/home/goran/usos/ISSP/2015/Marek.Marian
/home/goran/usos/ISSP/2017/Basia.Nowak
```

## Moduł *glob*

---

* umożliwia wykorzystanie uniksowych *dzikich kart*: `?`, `*`, `[]`


```python
import glob

print(glob.glob("*.ipynb"))  # lista plików z rozszerzeniem ipynb
```

```bash
['js-python_w04.ipynb',
'js-python_w03.ipynb',
'js-python_w05.ipynb',
'js-python_w01.ipynb',
'js-python_w07.ipynb',
'js-python_w02.ipynb',
'js-python_w06.ipynb']
```

## Więcej o *glob*

---

```python
# pliki z roszerzeniem html oraz
# pasujące do wzorca (coś)(cyfra od 0 do 3)
print(glob.glob("*[0-3].html"))
```

```bash
['js-python_w01.html', 'js-python_w03.html', 'js-python_w02.html']
```

```python
print(glob.glob("js-python_?02.*"))  # js-python_[znak]02.[cokolwiek]
```

```bash
['js-python_l02.md', 'js-python_w02.ipynb', 'js-python_w02.html']
```

```python
print(glob.glob("js-python_?02.[mi]*"))  # js-python_[znak]02.[m lub i]cokolwiek
```

```bash
['js-python_l02.md', 'js-python_w02.ipynb']
```

#

## Moduł *sys*

---

* funkcje i parametry specyficzne dla systemu operacyjnego
* ostatnio: ścieżka dostępu do modułów *sys.path*
* referencje do obiektów
* argumenty wywołania skryptu

## Referencje do obiektu

---

```python
import sys

x = 1234
y = 1234
z = "Mój tekst"

print(sys.getrefcount(x))  # x, y i ?
```

```bash
3
```

```python
print(sys.getrefcount(z))  # getrefcount pracuje na kopii z 
```

```bash
2
```

## Referencje do obiektów *mutowalnych*

---

```python
x = [1, 2, 3]
y = x
z = x.copy()

print(sys.getrefcount(x))  # x, y i getrefcount
```

```bash
3
```

```python
print(x is y)  # x i y wskazują to samo
```

```bash
True
```

```python
print(x is z)  # x i z wskazują na inne listy
```

```bash
False
```


## Argumenty 

---

`print_args.py`

```python
"""Drukuje argumenty podane w linii komend."""

import sys

# sys.argv - lista argumentów linii komend
for i, arg in enumerate(sys.argv):
    print("{}. {}".format(i, arg))
```

```bash
python print_args.py arg1 arg2 33 "hello world"
```

```
1. print_args.py
2. arg1
3. arg2
4. 33
5. hello world
```

## Przykład

---

`iloczyn.py`

```python
"""Liczy iloczyn podanych argumentów."""

import sys

if len(sys.argv) < 2:  # sys.argv[0] = iloczyn.py
    print("Musisz podać co najmniej jedną liczbę .")
else:
    wyrazenie = "*".join(sys.argv[1:])
    print(wyrazenie, "=", eval(wyrazenie))
```

```bash
python iloczyn.py
```

```bash
Musisz podać co najmniej jedną liczbę .
```

```bash
python iloczyn.py 1 2 5 4 10 0.5
```

```bash
1*2*5*4*10*0.5 = 200.0
```

#

## Moduł *time*

---

* operacje na czasie
* nie wszystkie funkcjonalności są dostępne na wszystkich platformach
* najczęściej wywoływane są funkcje biblioteki C o tej samej nazwie

## Czas uniksowy

---


```python
import time

print(time.gmtime())   # Greenwhich Mean Time / czas uniwersalny
```

```bash
time.struct_time(tm_year=2016, tm_mon=11, tm_mday=14, tm_hour=17, tm_min=43, tm_sec=9, tm_wday=0, tm_yday=319, tm_isdst=0)
```

```python
print(time.time())     # ile minęło sekund od epoki uniksa
```

```bash
1479145391.2862186
```

```python
print(time.gmtime(0))  # eoki Uniksa
```

```bash
time.struct_time(tm_year=1970, tm_mon=1, tm_mday=1, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=3, tm_yday=1, tm_isdst=0)
```

## Przybliżony test

---


```python
time.time() / 60 / 60 / 24 / 365  # lat
```

```bash
48.933277998481934
```

```python
print(time.gmtime()[0] - time.gmtime(0)[0])  # rok teraz - rok epoki linuksa
```

```bash
48
```

## Uniksowe chwile godne uwagi

---

```python
print(time.gmtime(1000000000)[:6])  # Unix billenium
```

```bash
(2001, 9, 9, 1, 46, 40)
```

```python
print(time.gmtime(1234567890)[:6])  # piątek 13-tego
```

```
(2009, 2, 13, 23, 31, 30)
```

![](../img/unix1234567890.gif)


```python
print(time.gmtime(0x7FFFFFFF)[:6])  # max ze znakiem (32-bit)
```

```bash
(2038, 1, 19, 3, 14, 7)
```

## Czas lokalny

---

```python
print(time.localtime())  # czas lokalny
```

```bash
time.struct_time(tm_year=2016, tm_mon=11, tm_mday=14, tm_hour=18, tm_min=43, tm_sec=19, tm_wday=0, tm_yday=319, tm_isdst=0)
```

```python
print(time.localtime()[3] - time.gmtime()[3])  # różnica Polska - GMT
```

```bash
1
```

## Czas w formie czytelnej

---

```python
teraz = time.localtime()

print(time.strftime("%c", teraz))  # lub time.asctime(teraz)
```

```bash
'Mon Nov 14 18:43:22 2016'
```

```python
dzien_tygodnia = time.strftime("%A", teraz)  # %a - skrót

print("Dzisiaj jest", dzien_tygodnia)
```

```bash
Dzisiaj jest Monday
```

```python
print(time.strftime("%Y-%m-%d %H:%M", teraz)) # ROK-MIESIĄC-DZIEŃ GODZINA:MINUTA
```

```bash
'2016-11-14 18:43'
```

* pełna lista dyrektyw [tutaj](https://docs.python.org/3.6/library/time.html#time.strftime)

## Pomiar czasu (*wall time*)

---

```python
import time

def poczekalnia(n):
    """Czeka n sekund."""
    time.sleep(n)
    
przed = time.time()  # czas przed wywołaniem funkcji

poczekalnia(2)

po = time.time()     # czas po wywołaniu funkcji

print("Czekałem {} sekund.".format(po - przed))
```

```bash
Czekałem 2.002260446548462 sekund.
```

## Pomiar czasu procesora (*process time*)

---


```python
import time

def poczekalnia(n):
    """Czeka n sekund."""
    time.sleep(n)
    
przed = time.clock()  # czas przed wywołaniem funkcji

poczekalnia(2)

po = time.clock()     # czas po wywołaniu funkcji

print("Czekałem {} sekund.".format(po - przed))
```

```bash
Czekałem 0.0015890000000000626 sekund.
```

#

## Moduł *datetime*

---

* wygodniejszy w użyciu do zarządzania czasem i datą
* arytmetyka czasu i daty, np.


```python
import datetime

t0 = datetime.datetime.now()
t1 = datetime.datetime(2017, 2, 4)  # początek sesji

print(t1 - t0)
```

```bash
81 days, 5:16:24.258938
```

## Przykład

---

```python
teraz = datetime.datetime.now()
uniks_end = datetime.datetime(2038, 1, 19, 3, 14, 7)

print("teraz =", teraz)
print("rok =", teraz.year)
print("miesiąc =", teraz.month)
print("dzień =", teraz.day)
print("Do końca uniksa zostało", uniks_end - teraz)
```

```bash
teraz = 2016-11-14 18:43:37.185897
rok = 2016
miesiąc = 11
dzień = 14
Do końca uniksa zostało 7735 days, 8:30:29.814103
```

## Przykład - logi

---

```python
import os
from datetime import datetime

def create_log(log_path, process):
    """Tworzy unikatowy log."""
    timestamp = datetime.now().strftime('%Y_%m_%d_%H%M%S')
    filename = ".".join([process, timestamp, "log"])
    with open(os.path.join(log_path, filename), 'w+') as f:
        f.write("Uruchomiono proces.")

create_log(os.getcwd(), "test")
```

```bash
ls -l *.log
```

```bash
-rw-rw-r-- 1 goran goran 19 lis 11 17:59 test.2016_11_11_175921.log
-rw-rw-r-- 1 goran goran 19 lis 11 17:59 test.2016_11_11_175922.log
-rw-rw-r-- 1 goran goran 19 lis 11 17:59 test.2016_11_11_175942.log
-rw-rw-r-- 1 goran goran 19 lis 14 18:43 test.2016_11_14_184342.log
```