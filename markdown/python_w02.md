% Języki skryptowe Python
% Wykład 2

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

#

## Sekwencyjne typy danych

---

* Na ostatnim wykładzie wprowadzone zostały liczbowe typy danych: `int`, `float` i `complex`

```
# [zmienna] [operator przypisania] [wartość]
# typowanie dynamiczne

n = 10  # liczba całkowita
x = 1.5 # liczba zmiennoprzecinkowa
c = 2j  # liczba zespolona
```

* Dzisiaj omówione zostaną podstawowe typy sekwencyjne: `str`, `list`, `tuple` i `range`

## Typ tekstowy

---

* Typ tekstowy (`str`, *string*) przechowuje ciąg znaków
```
s = "Python"
print(type(s))
```
```
<class 'str'>
```
* Python 3 używa domyślnie kodowania *unicode* dla typu *str*
* Dzięki czemu mamy polskie znaki od ręki

## Typ tekstowy z i bez *unicode*

---

<div class="left">
Python 3 (z *unicode*)

```
Python 3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  2 2016, 17:53:06) 
[GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> s = "zażółć gęślą jaźń"
>>> s
'zażółć gęślą jaźń'
>>> 
```
</div>
<div class="right">
Python 2 (bez *unicode*)

```
Python 2.7.12 (default, Jul  1 2016, 15:12:24) 
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> s = "zażółć gęślą jaźń"
>>> s
'za\xc5\xbc\xc3\xb3\xc5\x82\xc4\x87 g\xc4\x99\xc5\x9bl\xc4\x85 ja\xc5\xba\xc5\x84'
>>> 
```
</div>

## Typ tekstowy 

---

* Literał łańcuchowy można wprowadzić przez:

    * pojedynczy cudzysłów
    ```
    s = 'zażółć gęślą jaźń'
    ```
    * podwójny cudzysłów
    ```
    s = "zażółć gęślą jaźń"
    ```
    * potrójny cudzysłów
    ```
    s = '''zażółć gęślą jaźń'''
    s = """zażółć gęślą jaźń"""
    ```

## Cudzysłów w tekście

---

* Jeśli `str` otwieramy `"`, to ten sam znak kończy ciągn znaków, stąd np.
```
print("Ala powiedziała: "Mam kota." ...")  # cudzysłów kończy literał
```
* zwróci błąd:
```
  File "<stdin>", line 1
    print("Ala powiedziała: "Mam kota." ...") 
                               ^
SyntaxError: invalid syntax
```

## Cudzysłów w tekście

---

* Ale można wykorzystać kombinację `"` i `'`, np.
```
print('Ala powiedziała: "Mam kota." ...')
```
* wydrukuje na ekranie:
```
Ala powiedziała: "Mam kota." ...
```

## Znak ucieczki

---

* zmienia interpretację znaku
* w Pythonie (i prawie zawsze) jest to `\`
```
print("Ala powiedziała: \"Mam kota.\" ...")
```
* wydrukuje na ekranie:
```
Ala powiedziała: "Mam kota." ...
```

## Wybrane sekewncje specjalne

---

* `\n` - nowa linia
* `\t` - tabulacja
* `\r` - powrót kursora
* `\v` - pionowa tabulacja

## Przykład

---

```
print("\\n wstawia nową linię.\nNowa linia.\n\tNowa linia z tabulacją!")
```

wydrukuje na ekranie (zwróć uwagę na `\\n`)

```
\n wstawia nową linię.
Nowa linia.
	Nowa linia z tabulacją!
```

## Długie łańcuchy

---

* Długie ciągi znaków można przechowywać w jednej linii
* Jednak upośledza to czytelność kodu

```
tekst = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem. Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam. Quisque semper justo at risus. Donec venenatis, turpis vel hendrerit interdum, dui ligula ultricies purus, sed posuere libero dui id orci. Nam congue, pede vitae dapibus aliquet, elit magna vulputate arcu, vel tempus metus leo non est. Etiam sit amet lectus quis est congue mollis. Phasellus congue lacus eget neque. Phasellus ornare, ante vitae consectetuer consequat, purus sapien ultricies dolor, et mollis pede metus eget nisi. Praesent sodales velit quis augue. Cras suscipit, urna at aliquam rhoncus, urna quam viverra nisi, in interdum massa nibh nec erat."

print(tekst)
```

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem. Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam. Quisque semper justo at risus. Donec venenatis, turpis vel hendrerit interdum, dui ligula ultricies purus, sed posuere libero dui id orci. Nam congue, pede vitae dapibus aliquet, elit magna vulputate arcu, vel tempus metus leo non est. Etiam sit amet lectus quis est congue mollis. Phasellus congue lacus eget neque. Phasellus ornare, ante vitae consectetuer consequat, purus sapien ultricies dolor, et mollis pede metus eget nisi. Praesent sodales velit quis augue. Cras suscipit, urna at aliquam rhoncus, urna quam viverra nisi, in interdum massa nibh nec erat.
```

## Długie łańcuchy

---

* Tekst można dowolnie *łamać* korzystając z `\`
* Ale uwaga na dodatkowe spacje

```
tekst = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh \
         augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem. \
         Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam."

print(tekst)
```

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh          augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem.          Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam.
```

## Długie łańcuchy

---

* Problemu można uniknąć zamykając każdą linię w cudzysłowie

```
tekst = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh " \
        "augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem. " \
        "Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam."

print(tekst)
```

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem. Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam.
```

## Długie łańcuchy

---

* Jeśli chcemy, aby wydrukowany tekst też był *złamany*, to korzystamy z `\n`

```
tekst = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh\n" \
        "augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem.\n" \
        "Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam."

print(tekst)
```

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh
augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem.
Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam.
```

## Długie łańcuchy

---

* lub korzystamy z potrójnego cudzysłowu (uwaga na spacje w nowych liniach)

```
tekst = """Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh
augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem.
Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam."""

print(tekst)
```

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin nibh
augue, suscipit a, scelerisque sed, lacinia in, mi. Cras vel lorem.
Etiam pellentesque aliquet tellus. Phasellus pharetra nulla ac diam.
```

#

## Indeksowanie sekwencji

---

* Dostęp do elementów sekwencji odbywa się za pomocą operatora `[]`
* Indeksowanie zaczyna się od `0` a kończy na `n-1`, gdzie `n` - długość ciągu

```
s = "Python"

s[0]       # pierwszy znak      -> P
s[1]       # druki znak         -> y

n = len(s) # długość łańcucha s -> 6

s[n-1]     # ostatni znak       -> n
```

## IndexError

---

* Próba dostępu do elementu poza zakresem zakończy się błędem

```
>>> s = "Python"
>>> n = len(s)
>>> s[n]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
>>> 
```

## Wycinki

---

* Wycinki umożliwiają dostęp do fragmentu ciągu
* `zmienna[i:j]` zwróci elementy od `i` (włącznie) do `j`

```
s = "Python"

s[2:4]  # elementy od 2 do 3 -> th
```

## Domyślne granice przedziału

---

* Jeśli brzeg przedziału nie zostanie podany, intepreter przyjmie odpowiednio początek lub koniec ciągu

```
s = "Python"

s[2:]  # od 3-go do końca        -> thon
s[:2]  # od początku do drugiego -> Py
s[:]   # od początku do końca    -> Python
```

## Uwaga: brak IndexError dla wycinków

---

* W przypadku wycinków można wyjść z indeksem poza zakres

```
s = "Python"

s[0:1000]  # od początku do końca -> Python
```

## Wycinki z krokiem

---

* Możliwy jest również dostęp do co `k`-tego elementu podzbioru
* `zmienna[i:j:k]` zwróci co `k`-ty element z przedziału `[i, j)`

```
s = "0123456789"

s[2:8:2]  # od 3-go do 7-go, co drugi      -> 246

s[2::3]   # od 3-go do końca, co trzeci    -> 258

s[::2]    # od początku do końca, co drugi -> 02468
```

## Indeksy ujemne

---

* Indeks `−k` oznacza `n−k`, gdzie `n` - długość łańcucha

```
s = "Python"

s[-1]   # 6 - 1 = 5, ostatni znak -> n
s[-2]   # 6 - 2 = 4, przedostatni -> o
s[-2:]  # dwa ostanie             -> on
s[:-2]  # oprócz dwóch ostatnich  -> Pyth
```


