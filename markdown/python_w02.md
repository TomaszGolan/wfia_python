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

#

## Dygresja: klasy

---

* więcej o klasach będzie na dalszych wykładach
* klasa definuje obiekt
* przypisując wartość zmiennej tworzymy obiekt danej klasy

```
n = 10  # tworzymy obiekt klasy int
```

## Dygresja: metody

---

* klasa może posiadać zmienne i metody (czyli funkcje działające na obiekt)

```
x = 1.0  # tworzymy obiekt klasy float

# metody/zmienne klasy wywołujemy .
x.is_integer() # [obiekt].metoda
```

```
True
```

## Dygresja: dokumentacja

---

```
>>> help(str)
Help on class str in module builtins:

class str(object)
 |  str(object='') -> str
 |  str(bytes_or_buffer[, encoding[, errors]]) -> str
 |  
 |  Create a new string object from the given object. If encoding or
 |  errors is specified, then the object must expose a data buffer
 |  that will be decoded using the given encoding and error handler.
 |  Otherwise, returns the result of object.__str__() (if defined)
 |  or repr(object).
 |  encoding defaults to sys.getdefaultencoding().
 |  errors defaults to 'strict'.
 |  
 |  Methods defined here:
 |  
 |  __add__(self, value, /)
 |      Return self+value.
 |  
 |  __contains__(self, key, /)
 |      Return key in self.
 |  
 |  __eq__(self, value, /)
 |      Return self==value.
 |  
 |  __format__(...)
 |      S.__format__(format_spec) -> str
 |      
 |      Return a formatted version of S as described by format_spec.
 |  
 |  __ge__(self, value, /)
 |      Return self>=value.
 |  
 |  __getattribute__(self, name, /)
 |      Return getattr(self, name).
 |  
 |  __getitem__(self, key, /)
 |      Return self[key].
 |  
 |  __getnewargs__(...)
 |  
 |  __gt__(self, value, /)
 |      Return self>value.
 |  
 |  __hash__(self, /)
 |      Return hash(self).
 |  
 |  __iter__(self, /)
 |      Implement iter(self).
 |  
 |  __le__(self, value, /)
 |      Return self<=value.
 |  
 |  __len__(self, /)
 |      Return len(self).
 |  
 |  __lt__(self, value, /)
 |      Return self<value.
 |  
 |  __mod__(self, value, /)
 |      Return self%value.
 |  
 |  __mul__(self, value, /)
 |      Return self*value.n
 |  
 |  __ne__(self, value, /)
 |      Return self!=value.
 |  
 |  __new__(*args, **kwargs) from builtins.type
 |      Create and return a new object.  See help(type) for accurate signature.
 |  
 |  __repr__(self, /)
 |      Return repr(self).
 |  
 |  __rmod__(self, value, /)
 |      Return value%self.
 |  
 |  __rmul__(self, value, /)
 |      Return self*value.
 |  
 |  __sizeof__(...)
 |      S.__sizeof__() -> size of S in memory, in bytes
 |  
 |  __str__(self, /)
 |      Return str(self).
 |  
 |  capitalize(...)
 |      S.capitalize() -> str
 |      
 |      Return a capitalized version of S, i.e. make the first character
 |      have upper case and the rest lower case.
 |  
 |  casefold(...)
 |      S.casefold() -> str
 |      
 |      Return a version of S suitable for caseless comparisons.
 |  
 |  center(...)
 |      S.center(width[, fillchar]) -> str
 |      
 |      Return S centered in a string of length width. Padding is
 |      done using the specified fill character (default is a space)
 |  
 |  count(...)
 |      S.count(sub[, start[, end]]) -> int
 |      
 |      Return the number of non-overlapping occurrences of substring sub in
 |      string S[start:end].  Optional arguments start and end are
 |      interpreted as in slice notation.
 |  
 |  encode(...)
 |      S.encode(encoding='utf-8', errors='strict') -> bytes
 |      
 |      Encode S using the codec registered for encoding. Default encoding
 |      is 'utf-8'. errors may be given to set a different error
 |      handling scheme. Default is 'strict' meaning that encoding errors raise
 |      a UnicodeEncodeError. Other possible values are 'ignore', 'replace' and
 |      'xmlcharrefreplace' as well as any other name registered with
 |      codecs.register_error that can handle UnicodeEncodeErrors.
 |  
 |  endswith(...)
 |      S.endswith(suffix[, start[, end]]) -> bool
 |      
 |      Return True if S ends with the specified suffix, False otherwise.
 |      With optional start, test S beginning at that position.
 |      With optional end, stop comparing S at that position.
 |      suffix can also be a tuple of strings to try.
 |  
 |  expandtabs(...)
 |      S.expandtabs(tabsize=8) -> str
 |      
 |      Return a copy of S where all tab characters are expanded using spaces.
 |      If tabsize is not given, a tab size of 8 characters is assumed.
 |  
 |  find(...)
 |      S.find(sub[, start[, end]]) -> int
 |      
 |      Return the lowest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |      
 |      Return -1 on failure.
 |  
 |  format(...)
 |      S.format(*args, **kwargs) -> str
 |      
 |      Return a formatted version of S, using substitutions from args and kwargs.
 |      The substitutions are identified by braces ('{' and '}').
 |  
 |  format_map(...)
 |      S.format_map(mapping) -> str
 |      
 |      Return a formatted version of S, using substitutions from mapping.
 |      The substitutions are identified by braces ('{' and '}').
 |  
 |  index(...)
 |      S.index(sub[, start[, end]]) -> int
 |      
 |      Return the lowest index in S where substring sub is found, 
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |      
 |      Raises ValueError when the substring is not found.
 |  
 |  isalnum(...)
 |      S.isalnum() -> bool
 |      
 |      Return True if all characters in S are alphanumeric
 |      and there is at least one character in S, False otherwise.
 |  
 |  isalpha(...)
 |      S.isalpha() -> bool
 |      
 |      Return True if all characters in S are alphabetic
 |      and there is at least one character in S, False otherwise.
 |  
 |  isdecimal(...)
 |      S.isdecimal() -> bool
 |      
 |      Return True if there are only decimal characters in S,
 |      False otherwise.
 |  
 |  isdigit(...)
 |      S.isdigit() -> bool
 |      
 |      Return True if all characters in S are digits
 |      and there is at least one character in S, False otherwise.
 |  
 |  isidentifier(...)
 |      S.isidentifier() -> bool
 |      
 |      Return True if S is a valid identifier according
 |      to the language definition.
 |      
 |      Use keyword.iskeyword() to test for reserved identifiers
 |      such as "def" and "class".
 |  
 |  islower(...)
 |      S.islower() -> bool
 |      
 |      Return True if all cased characters in S are lowercase and there is
 |      at least one cased character in S, False otherwise.
 |  
 |  isnumeric(...)
 |      S.isnumeric() -> bool
 |      
 |      Return True if there are only numeric characters in S,
 |      False otherwise.
 |  
 |  isprintable(...)
 |      S.isprintable() -> bool
 |      
 |      Return True if all characters in S are considered
 |      printable in repr() or S is empty, False otherwise.
 |  
 |  isspace(...)
 |      S.isspace() -> bool
 |      
 |      Return True if all characters in S are whitespace
 |      and there is at least one character in S, False otherwise.
 |  
 |  istitle(...)
 |      S.istitle() -> bool
 |      
 |      Return True if S is a titlecased string and there is at least one
 |      character in S, i.e. upper- and titlecase characters may only
 |      follow uncased characters and lowercase characters only cased ones.
 |      Return False otherwise.
 |  
 |  isupper(...)
 |      S.isupper() -> bool
 |      
 |      Return True if all cased characters in S are uppercase and there is
 |      at least one cased character in S, False otherwise.
 |  
 |  join(...)
 |      S.join(iterable) -> str
 |      
 |      Return a string which is the concatenation of the strings in the
 |      iterable.  The separator between elements is S.
 |  
 |  ljust(...)
 |      S.ljust(width[, fillchar]) -> str
 |      
 |      Return S left-justified in a Unicode string of length width. Padding is
 |      done using the specified fill character (default is a space).
 |  
 |  lower(...)
 |      S.lower() -> str
 |      
 |      Return a copy of the string S converted to lowercase.
 |  
 |  lstrip(...)
 |      S.lstrip([chars]) -> str
 |      
 |      Return a copy of the string S with leading whitespace removed.
 |      If chars is given and not None, remove characters in chars instead.
 |  
 |  partition(...)
 |      S.partition(sep) -> (head, sep, tail)
 |      
 |      Search for the separator sep in S, and return the part before it,
 |      the separator itself, and the part after it.  If the separator is not
 |      found, return S and two empty strings.
 |  
 |  replace(...)
 |      S.replace(old, new[, count]) -> str
 |      
 |      Return a copy of S with all occurrences of substring
 |      old replaced by new.  If the optional argument count is
 |      given, only the first count occurrences are replaced.
 |  
 |  rfind(...)
 |      S.rfind(sub[, start[, end]]) -> int
 |      
 |      Return the highest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |      
 |      Return -1 on failure.
 |  
 |  rindex(...)
 |      S.rindex(sub[, start[, end]]) -> int
 |      
 |      Return the highest index in S where substring sub is found,
 |      such that sub is contained within S[start:end].  Optional
 |      arguments start and end are interpreted as in slice notation.
 |      
 |      Raises ValueError when the substring is not found.
 |  
 |  rjust(...)
 |      S.rjust(width[, fillchar]) -> str
 |      
 |      Return S right-justified in a string of length width. Padding is
 |      done using the specified fill character (default is a space).
 |  
 |  rpartition(...)
 |      S.rpartition(sep) -> (head, sep, tail)
 |      
 |      Search for the separator sep in S, starting at the end of S, and return
 |      the part before it, the separator itself, and the part after it.  If the
 |      separator is not found, return two empty strings and S.
 |  
 |  rsplit(...)
 |      S.rsplit(sep=None, maxsplit=-1) -> list of strings
 |      
 |      Return a list of the words in S, using sep as the
 |      delimiter string, starting at the end of the string and
 |      working to the front.  If maxsplit is given, at most maxsplit
 |      splits are done. If sep is not specified, any whitespace string
 |      is a separator.
 |  
 |  rstrip(...)
 |      S.rstrip([chars]) -> str
 |      
 |      Return a copy of the string S with trailing whitespace removed.
 |      If chars is given and not None, remove characters in chars instead.
 |  
 |  split(...)
 |      S.split(sep=None, maxsplit=-1) -> list of strings
 |      
 |      Return a list of the words in S, using sep as the
 |      delimiter string.  If maxsplit is given, at most maxsplit
 |      splits are done. If sep is not specified or is None, any
 |      whitespace string is a separator and empty strings are
 |      removed from the result.
 |  
 |  splitlines(...)
 |      S.splitlines([keepends]) -> list of strings
 |      
 |      Return a list of the lines in S, breaking at line boundaries.
 |      Line breaks are not included in the resulting list unless keepends
 |      is given and true.
 |  
 |  startswith(...)
 |      S.startswith(prefix[, start[, end]]) -> bool
 |      
 |      Return True if S starts with the specified prefix, False otherwise.
 |      With optional start, test S beginning at that position.
 |      With optional end, stop comparing S at that position.
 |      prefix can also be a tuple of strings to try.
 |  
 |  strip(...)
 |      S.strip([chars]) -> str
 |      
 |      Return a copy of the string S with leading and trailing
 |      whitespace removed.
 |      If chars is given and not None, remove characters in chars instead.
 |  
 |  swapcase(...)
 |      S.swapcase() -> str
 |      
 |      Return a copy of S with uppercase characters converted to lowercase
 |      and vice versa.
 |  
 |  title(...)
 |      S.title() -> str
 |      
 |      Return a titlecased version of S, i.e. words start with title case
 |      characters, all remaining cased characters have lower case.
 |  
 |  translate(...)
 |      S.translate(table) -> str
 |      
 |      Return a copy of the string S in which each character has been mapped
 |      through the given translation table. The table must implement
 |      lookup/indexing via __getitem__, for instance a dictionary or list,
 |      mapping Unicode ordinals to Unicode ordinals, strings, or None. If
 |      this operation raises LookupError, the character is left untouched.
 |      Characters mapped to None are deleted.
 |  
 |  upper(...)
 |      S.upper() -> str
 |      
 |      Return a copy of S converted to uppercase.
 |  
 |  zfill(...)
 |      S.zfill(width) -> str
 |      
 |      Pad a numeric string S with zeros on the left, to fill a field
 |      of the specified width. The string S is never truncated.
 |  
 |  ----------------------------------------------------------------------
 |  Static methods defined here:
 |  
 |  maketrans(x, y=None, z=None, /)
 |      Return a translation table usable for str.translate().
 |      
 |      If there is only one argument, it must be a dictionary mapping Unicode
 |      ordinals (integers) or characters to Unicode ordinals, strings or None.
 |      Character keys will be then converted to ordinals.
 |      If there are two arguments, they must be strings of equal length, and
 |      in the resulting dictionary, each character in x will be mapped to the
 |      character at the same position in y. If there is a third argument, it
 |      must be a string, whose characters will be mapped to None in the result.
(END)
```

## Dygresja: przykład

---

```
>>> help(str.replace)
Help on method_descriptor:

replace(...)
    S.replace(old, new[, count]) -> str
    
    Return a copy of S with all occurrences of substring
    old replaced by new.  If the optional argument count is
    given, only the first count occurrences are replaced.
```

```
s = "Python"

s.replace('yt', 'yyyyyt') # [obiekt].metoda
```

```
'Pyyyyython'
```

#

## Lista (`list`)

---

* sekwencja zmiennych dowolnego typu
* dynamiczny rozmiar
* inicjowana jest:
    * nawiasy kwadratowe
    * jawnie list([iterable]) (czyli konstruktor klasy list)
    * lista składana (list comprehension)

## Lista przez \[\]

---

```
lista = [1, 2, 'a', "Python"]  # 4-elementowa listę obiektów typu str i int
```

```
len(lista)  # długość listy
```

```
4
```

```
lista[0]  # pierwszy element listy
```

```
1
```

```
lista[-1][0]  # pierwszy element ostatniego elementu listy
```

```
'P'
```

## Lista przez konstruktor

---


```
lista = list([1,2,3])  # bez sensu, ale można
```

```
[1, 2, 3]
```

```
lista = list("Python")  # można stworzyć listę ze string
```

```
['P', 'y', 't', 'h', 'o', 'n']
```

```
lista = list(1)  # ale już nie z int
```

```
---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

<ipython-input-28-5b92e1b521a9> in <module>()
----> 1 lista = list(1) # ale już nie z int


TypeError: 'int' object is not iterable
```

## Lista składana

---

```
cyfry = ["jeden", "dwa", "trzy"]  # definiujemy listę

# [wartość] dla [obiektu] z [listy]
# pętle zostaną szerzej omówione na kolejnych wykładach
dlugosc = [len(cyfra) for cyfra in cyfry]
```

```
[5, 3, 4]
```

```
cyfry = ["jeden", "dwa", "trzy"]  # definiujemy listę

# [wartość] dla [obiektu] z [listy] jeśli [warunek]
# warunki zostaną szerzej omówione na kolejnych wykładach
dlugosc = [len(cyfra) for cyfra in cyfry if cyfra != 'dwa']
```

```
[5, 4]
```

## Lista jako rezultat funkcji

---

```
>>> help(str.split)

Help on method_descriptor:

split(...)
    S.split(sep=None, maxsplit=-1) -> list of strings

    Return a list of the words in S, using sep as the
    delimiter string.  If maxsplit is given, at most maxsplit
    splits are done. If sep is not specified or is None, any
    whitespace string is a separator and empty strings are
    removed from the result.
```

```
("Python is awesome, fast, and friendly!").split()
```

```
['Python', 'is', 'awesome,', 'fast,', 'and', 'friendly!']
```

#

## Krotka (`tuple`)

---

* sekwencja zmiennych dowolnego typu
* stały rozmiar
* inicjowana jest:
    * nawiasy okrągłe
    * ciąg elementów oddzielonych przecinkiem
    * jawnie tuple([iterable])

## Krotka - przykłady

---

```
krotka = (1, 2, 3, "Python")  # jak lista, ale () zamiast []
```

```
(1, 2, 3, 'Python')
```

```
krotka = 1, 2, 3, "Python"  # brak nawiasów = tuple
```

```
(1, 2, 3, 'Python')
```

```
lista = list("Python")  # lista ze stringa

krotka = tuple(lista)   # krotka z listy

print(lista)
print(krotka)
```

```
['P', 'y', 't', 'h', 'o', 'n']
('P', 'y', 't', 'h', 'o', 'n')
```

## Krotka vs lista

---

* krotka ma stały rozmiar a lista jest dynamiczna
* krotka jest "niezmienna" (*immutable*) w przeciwieństwie do listy (*mutable*)
* więcej o *mutable* vs *immutable* na kolejnym wykładzie
* jeśli sekwencja obiektów jest stała w czasie działania programu, lepiej używać krotek
    * szybsze
    * bezpieczniejsze
    * mogą być kluczami w słowniku (o słownikach na kolejnych wykładach)

## Krotka jest stała

---

```
lista = [1, 2, 3]

lista[0] = 2  # pierwszy element listy -> 2
```

```
[2, 2, 3]
```

```
krotka = (1, 2, 3)

krotka[0] = 2  # operacja niedozwolona dla krotek
```

```
---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

<ipython-input-38-9a057d2d95b0> in <module>()
      1 krotka = (1, 2, 3)
      2 
----> 3 krotka[0] = 2


TypeError: 'tuple' object does not support item assignment
```

#

## `range`

---

* uwaga: w Pythonie 2 `range()` jest funkcją wbudowaną; w Pythonie 3 jest to typ danych (klasa)
* reprezentuje (niezmienniczą) sekwencję liczb
* zajmuje mniej pamięci niż `list` lub `tuple` (przechowuje tylko informację o początku, końcu i kroku)

## `range`: przykład

---

```
x = range(10)  # od 0 do 10

print(x)  # w Pythonie 2 zobaczylibyśmy [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```
range(0, 10)
```

```
print(list(x))  # zrzutujemy na listę, żeby wydrukować
```

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```
x[0] = 1  # range jest immutable
```

```
---------------------------------------------------------------------------

TypeError                                 Traceback (most recent call last)

<ipython-input-41-3a9de573c036> in <module>()
----> 1 x[0] = 1 # range jest immutable


TypeError: 'range' object does not support item assignment
```

## `range` z krokiem

---

```
cyfry = range(0, 10)       # range(początek = 0, koniec) 
parzyste = range(2, 10, 2) # range(początek, koniec, krok)
nieparzyste = range(1, 10, 2)

print(list(cyfry))
print(list(parzyste))
print(list(nieparzyste))
```

```
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[2, 4, 6, 8]
[1, 3, 5, 7, 9]
```

#

## Sekwencyjne typy danych: podsumowanie

---

* `list` - dynamiczny ciąg zmiennych dowolnego typu
* `tuple` - niezmienniczy ciąg zmiennych dowolnego typu
* `range` - niezmienniczy ciąg liczba całkowitych
* `str` - niezmienniczy ciąg znaków
* (dla kompletności) są jeszcze binarne sekwencyjne typy danych: `bytes`, `bytearray`, `memoryview`

## Operacje na sekwencjach

---

```
"y" in "Python"        # True

"p" not in "Python"    # True

[1, 2, 3] + [4, 5, 6]  # [1, 2, 3, 4, 5, 6]

'-' * 10               # '----------'

(1, 2, 3) * 2          # (1, 2, 3, 1, 2, 3)
```

## Funkcje wbudowane i metody

---

```
len([1,2,-3])  # liczba elementów -> 3

min([1,2,-3])  # minimum          -> -3

max("Python")  # maximum          -> 'y'
```

```
[1, 2, 3, 2, 4, 2].count(2)  # liczba wystąpień     -> 3

[1, 2, 3, 2, 4, 2].index(2)  # pierwsze wystapienie -> 1
```

## Operacje na sekwencjach zmiennych

---

```
lista = [1, 2, 3]

lista[1] = 4          # -> [1, 4, 3]

lista[1:2] = [5, 6]   # -> [1, 5, 6, 3]

del lista[1:3]        # -> [1, 6, 3]

lista.append(7)       # -> [1, 6, 3, 7]

lista.extend([8, 9])  # -> [1, 6, 3, 7, 8, 9]

```

#

## Podsumowanie

---

* `str` jest podstawowym typem zmiennej to przechowywania tekstu

* `list` jest sekwencją zmiennych dowolnego typu

* `tuple` jest *stałą listą*

* `range` jest ciągiem arytmetycznym

* Na kolejnym wykładzie przedstawione zostaną podstawy programowania strukturalnego.