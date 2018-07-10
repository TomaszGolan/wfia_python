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

