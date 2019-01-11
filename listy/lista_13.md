# Lista 13

# Zadanie 1 (15 pkt)

Napisz program do rozegrania jednej rundy *Shut the Box*.

Gra rozpoczyna się z 9 odkrytymi kartami z cyframi od 1 do 9:

```bash
*****   *****   *****   *****   *****   *****   *****   *****   *****
* 1 *   * 2 *   * 3 *   * 4 *   * 5 *   * 6 *   * 7 *   * 8 *   * 9 *
*****   *****   *****   *****   *****   *****   *****   *****   *****
```

Jeśli suma odkrytych cyfr jest większa od 6, gracz rzuca dwiema koścmi 6-ściennymi. W przeciwnym wypadku rzuca jedną.

Gracz sumuje wyrzuczone oczka i zakrywa dowolną liczbę kart, których suma odpowiada sumie oczek, np. dla rzutu *2* i *4* można zamknąć:

* 6
* 1, 5
* 2, 4
* 1, 2, 3

Po rzucie kostką gracz wybiera karty do zakrycia, po czym następuje aktualizacja stanu gry, np.

```bash
Wyrzuciłeś 2 i 4, które karty chcesz zakryć: 2, 4

*****   *****   *****   *****   *****   *****   *****   *****   *****
* 1 *   *****   * 3 *   *****   * 5 *   * 6 *   * 7 *   * 8 *   * 9 *
*****   *****   *****   *****   *****   *****   *****   *****   *****
```

*Uwaga: gra musi odpowiednio reagować, jeśli podane karty są nieprawidłowe (np. podano już zakrytą kartę lub suma się nie zgadza).*

Gra się kończy, gdy wyrzucona suma oczek uniemożliwia zamknięcie karty, a końcowym wynikiem jest suma pozostałych odkrytych cyfr.



