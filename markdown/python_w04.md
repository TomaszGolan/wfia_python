% Języki skryptowe Python
% Wykład 4

<div class='footer'>
Sterowanie: spacja + shift-spacja || page down + page up || strzałki || esc 
</div>

# 

## Typy mutowalne (*mutable*) i niemutowalne (*immutable*)

---

* typy liczbowe ("niemutowalne"): `int`, `float`, `complex`
* typy sekwencyjne ("mutowalne"): `list`
* typy sekwencyjne ("niemutowalne"): `tuple`, `range`, `str`


## `id` zmiennych

---


```py
x = 2  # tworzymy niemutowalną zmienną
id(x)  # i sprawdzamy jej id
```

```bash
140685772794432
```

```py
x = 3  # przypisanie nowej wartości 
id(x)  # tworzy nowy obiekt (z nowym id)
```

```bash
140685772794464
```


```py
x = [2]  # tworzymy mutowalną zmienną 
id(x)    # i sprawdzamy jej id
```

```bash
140685552461384
```

```py
x[0] = 3  # wartość wskazywana przez zmienną jest modyfikowana
id(x)     # ale jej id pozostaje stałe (uwaga: id(x[0]) będzie inne!)
```

```bash
140685552461384
```

## Konsekwencje

---

```py
x = 2  # uwtórz obiekt typu int
y = x  # y wskazuje na to samo co x
y = 5  # zmieniam y - nowe miejsce w pamięci

print(x)  # x dalej wskazuje na 2
```

```bash
2
```

```py
x = [1, 2, 3]  # utwórz obiekt typu list
y = x          # y wskazuje na to samo co x

print(id(x), id(y))
```

```bash
140684962055816 140684962055816
```

```py
y[0] = 4  # modyfikuję y

print(x)  # a zmienia się x...
```

```bash
[4, 2, 3]
```

## Funkcja `copy`

---

```py
x = [1, 2, 3]  # utwórz obiekt typu list
y = x.copy()   # stwórz kopię tego obiektu

print(id(x), id(y))  # teraz są to dwa różne obiekty
```

```bash
140685552556616 140685552460232
```

#


## "Odpakowywanie" (*unzip*)

---

```py
lista = [1, 2]

a, b = lista  # a = lista[0], b = lista[1]

print(a, b)
```

```bash
1 2
```

przykład: zamiana zmiennych


```py
a, b = b, a  # a, b = tuple(b, a)

print(a, b)
```

```bash
2 1
```

dla porównania przykład zamiany zmiennych w C++

```cpp
a = a + b - (b = a);
```

## *splat*, czyli tzw. *asterisk*

---

```py
x = [1, 2, 3]

# print(arg1, arg2, arg3, ..., +opcje)

print(x)                 # drukuje listę (1 argument)
print(*x)                # drukuje "rozpakowaną" listę (3 argumenty)
print(x[0], x[1], x[2])  # równoważny zapis
```

```bash
[1, 2, 3]
1 2 3
1 2 3
```

## *unzip* i *splat*

---

```py
lista = [1, 2, 3, 4, 5]

# a, b = lista  # ValueError: too many values to unpack (expected 2)

a, *b = lista  # a = lista[0], b = reszta

print(a, b)
```

```bash
1 [2, 3, 4, 5]
```

```py
lista = [1, 2, 3, 4, 5]

a, *b, c = lista  # a, b[0], b[1], b[2], c

print(a, b, c)
```

```bash
1 [2, 3, 4] 5
```

## "Pakowanie" (*zip*)

---


```py
x = [1, 2, 3]
y = ['a', 'b', 'c']

zipped = zip(x, y)  # pary (x[i], y[i])

print(*zipped)
```

```bash
(1, 'a') (2, 'b') (3, 'c')
```

```py
x = [1, 2, 3]
y = ['a', 'b', 'c', 'd']  # długość nie ma znaczenia

zipped = zip(x, y)  # pary (x[i], y[i])

print(*zipped)
```

```bash
(1, 'a') (2, 'b') (3, 'c')
```

## *zip* / *unzip* - test

---

```py
x = [1, 2, 3]
y = [4, 5, 6]

x_copy, y_copy = zip(*zip(x, y))

x == list(x_copy) and y == list(y_copy)
```

```bash
True
```

```py
print(list(zip(x,y)))
print(*zip(x,y))
print(list(zip(*zip(x, y))))
```

```bash
[(1, 4), (2, 5), (3, 6)]
(1, 4) (2, 5) (3, 6)
[(1, 2, 3), (4, 5, 6)]
```