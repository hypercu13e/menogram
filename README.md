# Menogram

Początkowa wersja tego dokumentu znajdująca się na forum gry zniknęła w niewyjaśnionych
okolicznościach, ale dostępny jest jej [zrzut][capture] w internetowym archiwum [Wayback
Machine][wayback-machine]. Niniejszy dokument jest odtworzeniem usuniętego tematu z forum gry.

## Definicje oraz założenia

1. Wszystkie używane zmienne oraz liczby są traktowane domyślnie jak liczby rzeczywiste, chyba że w
   danym kontekście zdefiniowane są one inaczej. **Należy pamiętać, że silnik gry operuje na
   liczbach zmiennoprzecinkowych, co czasem może prowadzić do rozbieżności.**
2. Wykorzystywane oznaczenia zbiorów:
    - $\mathbb{N}$ – zbiór liczb naturalnych włącznie z $0$.
    - $\mathbb{N}^*$ – zbiór liczb naturalnych bez $0$.
    - $\mathbb{Z}$ – zbiór liczb całkowitych
    - $\mathbb{Z}^*$ – zbiór liczb całkowitych bez $0$.
    - $a..b$ – zbiór liczb całkowitych większych od lub równych $a$ i mniejszych od lub równych $b$.
3. Wykorzystywane oznaczenia profesji:
    - w – wojownik
    - p – paladyn
    - b – tancerz ostrzy
    - m – mag
    - t – tropiciel
    - h – łowca
4. Łączenia profesji zapisywane są jako ciąg jednoliterowych skrótów poszczególnych profesji w
   kolejności zgodnej z kolejnością oznaczeń profesji zdefiniowaną w poprzednim punkcie.
5. Wykorzystywane funkcje:

    - $\mathop{\mathrm{round}}(x)$ – zaokrąglenie liczby $x$ do najbliższej liczby całkowitej.
      **Połówki zaokrąglane są w kierunku od $0$:**

    $$
    \begin{align*}
        \mathop{\mathrm{round}}(5.5) &= 6 \\
        \mathop{\mathrm{round}}(-5.5) &= -6
    \end{align*}
    $$

    - $\lfloor x \rfloor$ – zaokrąglenie liczby $x$ w dół do najbliższej liczby całkowitej.
    - $\lceil x \rceil$ – zaokrąglenie liczby $x$ w górę do najbliższej liczby całkowitej.
    - $\mathop{\mathrm{sgn}}(x)$ – znak liczby $x$:

    $$
    \mathop{\mathrm{sgn}}(x) = \begin{cases}
        1, & x > 0 \\
        0, & x = 0 \\
        -1, & x < 0
    \end{cases}
    $$

    - $x \bmod n$ – reszta z dzielenia $x$ przez $n$, $x \in \mathbb{N}, n \in \mathbb{N}^*$.
    - $\min(x, y)$ – mniejsza z liczb $x$ i $y$.
    - $\max(x, y)$ - większa z liczb $x$ i $y$.

## Przedmioty

Sekcja zawierająca opis bonusów przedmiotów. Przedstawione tutaj wzory stosują się jedynie do
przedmiotów, których statystyki utworzone są przez system, a nie do przedmiotów utworzonych ręcznie.
Ponadto twórcy gry mają możliwość modyfikacji utworzonych systemowo statystyk.

### Definicje i założenia

1. Zmienne używane we wzorach w nieniejszej sekcji:

    - $l \in \mathbb{N}^*$ – poziom wymagany do założenia przedmiotu. Jeżeli przedmiot nie posiada
      takiego przedmiotu, to przyjmowana jest wartość $1$.
    - $u \in 0..5$ – poziom ulepszenia przedmiotu.
    - $n \in \mathbb{Z}$ – liczba bonusów rozdanych w daną statystykę przedmiotu.
    - $x \in \mathbb{N}^*$ – poziom przedmiotu, tj. poziom używany do obliczania wartości bonusów,
      który uwzględnia ulepszenie:

    $$x = l + \mathop{\mathrm{sgn}}(n) \cdot u \cdot \mathop{\mathrm{round}}(0.03l)$$

    - $p$ – siła przedmiotu:
        - $0.75$ dla tarcz,
        - $0.33$ dla hełmów,
        - $0.3$ dla butów,
        - $0.25$ dla rękawic,
        - $1.0$ dla pozostałych przedmiotów.

2. Funkcje liczące wartości bonusów stosowane są tylko wtedy gdy $n \in \mathbb{Z}^*$. Jeśli
   $n = 0$, to wartość bonusu zawsze wynosi $0$.
3. Uzależnienie wartości bonusu od rzadkości przedmiotu określone jest przez następującą funkcję:

    $$R(x) = x^2 + \left(130 + \left\lceil \frac{10r}{3} \right\rceil\right)x + (130 + 390r)\mathop{\mathrm{sgn}}(r),$$

    gdzie $r$ wynosi:

    - $0$ dla przedmiotów zwykłych,
    - $1$ dla przedmiotów unikatowych,
    - $2$ dla przedmiotów ulepszonych i heroicznych,
    - $3$ dla przedmiotów legendarnych,
    - $4$ dla artefaktów.

4. Jeśli przedmiot posiada statystykę, która ma jednocześnie bonus natywny i bonus zwykły, to bonusy
   te nie są zaokrąglane osobno, a zaokrąglana jest ich suma. Zaokrąglanie sumy nie zawsze ma
   miejsce, co jest [błędem silnika][bug].
5. Zmienna $l$ w przypadku błogosławieństw, które nie posiadają wymaganego poziomu, jest równa
   poziomowi gracza, dzięki czemu błogosławieństwa te skalują się wraz z poziomem gracza.
   Błogosławieństwa, które posiadają wymóg poziomowy, nie posiadają takiego skalowania.

### Liczba bonusów

Większość przedmiotów posiada zestandaryzowaną liczbę bonusów, która zależy od typu i rzadkości
przedmiotu. Wyjątkiem od tej zasady są zazwyczaj stare lub testowe przedmioty.

#### Zbroje, bronie jednoręczne, półtoraręczne, dwuręczne, dystansowe i pomocnicze, różdżki, orby i tarcze

-   1 bonus dla przedmiotów zwykłych,
-   3 bonusy dla przedmiotów unikatowych,
-   7 bonusów dla przedmiotów ulepszonych,
-   6 bonusów dla przedmiotów heroicznych,
-   9 bonusów dla przedmiotów legendarnych.

#### Strzały

-   1 bonus dla przedmiotów zwykłych,
-   4 bonusy dla przedmiotów unikatowych,
-   6 bonusów dla przedmiotów ulepszonych,
-   8 bonusów dla przedmiotów heroicznych,
-   12 bonusów dla przedmiotów legendarnych.

#### Hełmy, rękawice, buty

-   1 bonus dla przedmiotów zwykłych,
-   4 bonusy dla przedmiotów unikatowych,
-   8 bonusów dla przedmiotów ulepszonych i heroicznych,
-   12 bonusów dla przedmiotów legendarnych.

#### Pierścienie

-   5 bonusów dla przedmiotów zwykłych,
-   9 bonusów dla przedmiotów unikatowych,
-   13 bonusów dla przedmiotów ulepszonych i heroicznych,
-   17 bonusów dla przedmiotów legendarnych.

#### Naszyjniki

-   6 bonusów dla przedmiotów zwykłych,
-   10 bonusów dla przedmiotów unikatowych,
-   14 bonusów dla przedmiotów ulepszonych i heroicznych,
-   18 bonusów dla przedmiotów legendarnych.

#### Dodatkowe modyfikatory

Pochodzenie przedmiotu może dodatkowo modyfikować liczbę bonusów:

-   1 dodatkowy bonus, jeśli przedmiot jest zdobyczą z tytana,
-   1 dodatkowy bonus, jeśli przedmiot jest pozyskiwany za pomocą rzemiosła,
-   1 dodatkowy bonus, jeśli przedmiot jest nagrodą z questa (lub pochodzi ze sklepu dostępnego po
    ukończeniu questa),
-   1 dodatkowy bonus, jeśli przedmiot pochodzi z limitowanych licytacji.

### Bonusy zwykłe

Bonusy przedstawione w tej sekcji są bonusami rozdanymi ręcznie przez twórców przedmiotów.

#### Pancerz

$f(x, n) = \mathop{\mathrm{round}}(0.003np(x^2 + 130x))$

#### Niszczenie pancerza

$f(x, n) = \mathop{\mathrm{round}}(0.0003nc(x^2 + 130x) + 1),$

gdzie $c$ wynosi:

-   $\frac{4}{3}$ dla broni,
-   $1$ dla pozostałych przedmiotów.

#### Redukcja niszczenia pancerza

Bonus, który prawdopodobnie aktualnie liczony jest [niepoprawnie][bug].

#### Absorpcja

$f(x, n) = \mathop{\mathrm{round}}(0.012n(x^2 + 130x))$

#### Niszczenie absorpcji

$f(x, n) = \mathop{\mathrm{round}}(0.006nc \cdot R(x)),$

gdzie $c$ wynosi:

-   $1.1$ dla broni jednoręcznych z wyjątkiem broni dla samego paladyna,
-   $1.0$ dla broni jednoręcznych dla samego paladyna,
-   $1.1$ dla broni półtoraręcznych,
-   $1.2$ dla broni dwuręcznych,
-   $1.0$ dla broni dystansowych,
-   $1.0$ dla różdżek,
-   $0.8$ dla broni pomocniczych,
-   $0.7$ dla orbów,
-   $0.4$ dla strzał.

#### Odporność magiczna

$f(n) = 3n$

#### Odporność na truciznę

$f(n) = 5n$

#### Niszczenie odporności

$f(n) = n$

#### Cios krytyczny

$f(n) = n$

#### Obniżanie ciosu krytycznego

$f(n) = 2n$

#### Siła ciosu krytycznego

$f(n) = 6n$

#### Obniżanie siły ciosu krytycznego

Bonus, który prawdopodobnie aktualnie liczony jest [niepoprawnie][bug].

#### Siła, zręczność, intelekt

$f(x, n) = \mathop{\mathrm{round}}(\frac{5}{9}nx + 4)$

#### Wszystkie cechy

$f(x, n) = \mathop{\mathrm{round}}(0.25nx + 8)$

#### Energia

$f(x, n) = \mathop{\mathrm{round}}(\frac{n}{15}(x + 150))$

#### Niszczenie energii

$f(x, n) = \mathop{\mathrm{round}}(0.02n(x + 100))$

#### Obniżanie niszczenia energii

Bonus, który prawdopodobnie aktualnie liczony jest [niepoprawnie][bug].

#### Mana

$f(x, n) = \mathop{\mathrm{round}}(0.25nx)$

#### Niszczenie many

$f(x, n) = \mathop{\mathrm{round}}(0.04n(x + 125))$

#### Obniżanie niszczenia many

Bonus, który prawdopodobnie aktualnie liczony jest [niepoprawnie][bug].

#### Życie

$f(x, n) = \mathop{\mathrm{round}}(3.08 \cdot (0.004np(x^2 + \frac{100x}{3}(\frac{7.5}{p} + 3.9)) + 8))$

#### Leczenie

$f(x, n) = \mathop{\mathrm{round}}(0.004np(x^2 + \frac{100x}{3}(\frac{6}{p} + 3.9)) + 8)$

#### Obniżanie leczenia

$f(x, n) = \mathop{\mathrm{round}}(0.5 \cdot (0.004np(x^2 + \frac{100x}{3}(\frac{7.5}{p} + 3.9)) + 8))$

Bonus obniżania leczenia jest bonusem negatywnym, tj. jest on traktowany tak jakby $n$ było liczbą
przeciwną przy zliczaniu liczby bonusów w przedmiocie.

#### Obniżanie leczenia przeciwnika

$f(x, n) = \mathop{\mathrm{round}}(0.75 ⋅ (0.004np(x^2 + \frac{100x}{3}(\frac{6}{p} + 3.9)) + 8))$

#### Unik

$f(x, n) = \mathop{\mathrm{round}}(0.1nx)$

#### Obniżanie uniku

$f(x, n) = \mathop{\mathrm{round}}(0.1nx)$

#### Blok

$f(x, n) = \mathop{\mathrm{round}}(0.15nx)$

#### Szybkość ataku

$f(x, n) = 0.01 \cdot \mathop{\mathrm{round}}(0.25nx + 8)$

#### Spowolnienie przeciwnika

$f(x, n) = 0.01 \cdot \mathop{\mathrm{round}}(\frac{2}{7}nx + 8)$

### Bonusy manualne

Bonusy manualne są bonusami zwykłymi, których wartość należy do zestandaryzowanego zakresu i jest, w
większości przypadków, ustalana ręcznie przez twórcę przedmiotu. Większość bonusów manualnych jest
liczona jako konkretna liczba bonusów, stąd są one przeniesione do osobnej sekcji.

#### Kontra

Pojedynczy bonus: $40\%$ lub $50\%$.

Podwójny bonus: $60\%$.

#### Przebicie

Pojedynczy bonus: $15\%$ lub $20\%$.

Podwójny bonus: $25\%$.

#### Blok przebicia

Zawsze pojedynczy bonus o wartości $40\%$, $50\%$ lub $60\%$.

#### Głęboka rana

Nie wlicza się do liczby bonusów. Osłabia istniejący bonus obrażeń fizycznych.

Szansa na głęboką ranę ustalana jest ręcznie i wynosi $20\%$, $23\%$ lub $25\%$.

Obrażenia głębokiej rany liczone są przez system:
$f(x) = \mathop{\mathrm{round}}(0.0051c \cdot R(x))$,

gdzie $c$ wynosi:

-   $2.75$ dla broni jednoręcznych,
-   $3.25$ dla broni dystansowych,
-   $1.15$ dla broni pomocniczych.

#### Trucizna

Nie wlicza się do liczby bonusów. Osłabia istniejący bonus obrażeń fizycznych.

Spowolnienie trucizny liczone jest przez system: $f(x) = 0.01 \cdot \mathop{\mathrm{round}}(cx)$,

gdzie $c$ wynosi:

-   $0.892475$ dla broni jednoręcznych,
-   $0.892475$ dla broni półtoraręcznych,
-   $0.4462375$ dla broni dystansowych,
-   $0.6375$ dla broni pomocniczych,
-   $0.4462375$ dla strzał.

Obrażenia trucizny liczone są przez system: $f(x) = \mathop{\mathrm{round}}(0.0051c \cdot R(x))$,
gdzie $c$ wynosi:

-   $2.5$ dla broni jednoręcznych,
-   $2.5$ dla broni półtoraręcznych,
-   $3.5$ dla broni dystansowych,
-   $1.05$ dla broni pomocniczych,
-   $0.85$ dla strzał.

#### Modyfikator rzadkości

W Margonem istnieje niewidoczny bonus modyfikujący rzadkość przedmiotu, często określany jako „bonus
w atak” w broniach lub jako „bonus w obronę” w pozostałych przedmiotach. Bonus ten nie jest
wyświetlany przez klienta gry, ale liczony jest on do liczby bonusów przedmiotu przez silnik gry.

Bonus ten jest zawsze pojedynczym bonusem, dodatnim lub ujemnym, który odpowiednio podnosi lub
obniża rzadkość przedmiotu (o 1 stopień), tj. parametr $r$ w funkcji $R(x)$, zatem wpływa on na
wszystkie bonusy zależne od rzadkości przedmiotu. W przedmiotach zwykłych nie występuje ujemny
modyfikator rzadkości, a w przedmiotach legendarnych nie występuje dodatni modyfikator rzadkości.

### Bonusy natywne

Bonusy natywne są bonusami automatycznie występującymi w przedmiocie ze względu na jego typ i
profesje, jakie mogą ubrać dany przedmiot. Bonusy natywne nie są wliczane do liczby bonusów.

#### Pancerz

Występuje w:

-   zbrojach,
-   tarczach,
-   hełmach,
-   rękawicach,
-   butach.

$f(x) = \mathop{\mathrm{round}}(0.02pc \cdot R(x)),$

gdzie $c$ zależy od wymaganych przez przedmiot profesji:

-   w: $1.4$,
-   p: $1.0$,
-   b: $0.9$,
-   m: $0.5$,
-   t: $0.7$,
-   h: $0.8$,
-   wp: $1.2$,
-   wb: $1.15$,
-   pt: $0.85$,
-   pm: $0.75$,
-   bh: $0.85$,
-   mt: $0.6$,
-   th: $0.75$,
-   pmt: $0.75$,
-   bth: $0.8$,
-   wpbmth: $0.9$,
-   pozostałe profesje: $1.0$.

#### Absorpcja

Występuje w:

-   zbrojach,
-   tarczach,
-   hełmach,
-   rękawicach,
-   butach.

Absorpcja fizyczna: $f(x) = \mathop{\mathrm{round}}(0.01pc \cdot R(x))$.

Absorpcja magiczna: $f(x) = \mathop{\mathrm{round}}(0.005pc \cdot R(x))$.

$c$ zależy od wymaganych przez przedmiot profesji:

-   m: $6.0$,
-   t: $4.0$,
-   pm: $3.0$,
-   mt: $5.0$,
-   ​pmt: $3.4$,
-   pozostałe profesje: $0$.

#### Odporność magiczna

Występuje w:

-   zbrojach,
-   tarczach,
-   hełmach,
-   rękawicach,
-   butach.

Bazowy rodzaj natywnej odporności magicznej zależy od parametru $c = l \bmod 3$:

-   Odporność na ogień, jeśli $c = 0$.
-   Odporność na zimno, jeśli $c = 1$.
-   Odporność na błyskawice, jeśli $c = 2$.

Należy pamiętać, że twórcy przedmiotów często zmieniają rodzaj natywnej odporności magicznej.

Wartość odporności wynosi $mr + c$, gdzie $m$ i $c$ odpowiednio zależą od wymaganych przez przedmiot
profesji:

-   p: $1$ i $6$,
-   b: $1$ i $2$,
-   m: $2$ i $10$,
-   t: $2$ i $8$,
-   h: $1$ i $4$,
-   wp: $1$ i $3$,
-   wb: $1$ i $1$,
-   pm: $2$ i $8$,
-   pt: $1$ i $7$,
-   bh: $1$ i $3$,
-   mt: $2$ i $9$,
-   th: $1$ i $6$,
-   wbh: $1$ i $2$,
-   pmt: $2$ i $8$,
-   bht: $1$ i $5$,
-   pozostałe profesje: $0$ i $0$.

Wartość $r$ zdefiniowana jest identycznie jak w przypadku funkcji $R(x)$.

#### Odporność na truciznę

Występuje w:

-   zbrojach,
-   hełmach,
-   rękawicach,
-   butach.

Wartość odporności wynosi $c$, gdzie $c$ zależy od wymaganych przez przedmiot profesji:

-   b: $8$,
-   t: $12$,
-   h: $16$,
-   wb: $4$,
-   pt: $6$,
-   bh: $12$,
-   mt: $6$,
-   th: $14$,
-   wbh: $8$,
-   pmt: $4$,
-   bht: $12$,
-   pozostałe profesje: $0$.

#### Mana

Występuje w zbrojach.

$f(x) = \mathop{\mathrm{round}}(\frac{1}{3}cx)$,

gdzie $c$ zależy od wymaganych przez przedmiot profesji:

-   m: $1.0$,
-   t: $0.5$,
-   mt: $0.5$,
-   pmt: $0.5$,
-   pozostałe profesje: $0$.

#### Bonus życia za siłę

Występuje w zbrojach.

$f(x) = 0.1 \cdot \mathop{\mathrm{round}}(cx)$,

gdzie $c$ zależy od wymaganych przez przedmiot profesji:

-   w: $1.0$,
-   p: $1.0$,
-   wp: $1.0$,
-   pozostałe profesje: $0$.

#### Unik

Występuje w zbrojach.

$f(x) = \mathop{\mathrm{round}}(\frac{1}{3}cx)$,

gdzie $c$ zależy od wymaganych przez przedmiot profesji:

-   b: $1.0$,
-   pozostałe profesje: $0$.

#### Szybkość ataku

Występuje w zbrojach.

$f(x) = 0.01 \cdot \mathop{\mathrm{round}}(cx)$,

gdzie $c$ zależy od wymaganych przez przedmiot profesji:

-   h: $0.5$,
-   t: $0.25$,
-   bh: $\frac{1}{3}$,
-   th: $\frac{1}{3}$,
-   bth: $\frac{1}{3}$,
-   pozostałe profesje: $0$.

#### Blok

Występuje w tarczach.

$f(x) = \mathop{\mathrm{round}}(cx)$,

gdzie $c$ zależy od wymaganych przez przedmiot profesji:

-   p: $1.2$,
-   wp: $1.1$,
-   pozostałe profesje: $1.0$.

#### Obrażenia fizyczne

Występują w:

-   broniach jednoręcznych,
-   broniach półtoraręcznych,
-   broniach dwuręcznych,
-   broniach dystansowych,
-   broniach pomocniczych.

Wartość minimalna obrażeń: $f(x) = \mathop{\mathrm{round}}(9 \cdot 0.0051c \cdot R(x))$.

Wartość maksymalna obrażeń: $f(x) = \mathop{\mathrm{round}}(11 \cdot 0.0051c \cdot R(x))$.

$c$ wynosi:

-   $1.06$ dla broni jednoręcznych z wyjątkiem broni dla samego paladyna,
-   $0.9$ dla broni jednoręcznych dla samego paladyna,
-   $0.83$ dla broni jednoręcznych z trucizną lub głęboką raną,
-   $1.25$ dla broni półtoraręcznych,
-   $1.025$ dla broni półtoraręcznych z trucizną lub głęboką raną,
-   $1.75$ dla broni dwuręcznych z wyjątkiem broni dla samego paladyna,
-   $1.53$ dla broni dwuręcznych dla samego paladyna,
-   $1.35$ dla broni dystansowych z wyjątkiem broni dla samego tropiciela,
-   $0.7$ dla broni dystansowych dla samego tropiciela,
-   $0.91$ dla broni dystansowych z trucizną lub głęboką raną,
-   $0.755$ dla broni pomocniczych,
-   $0.595$ dla broni pomocniczych z trucizną lub głęboką raną,
-   $0$ dla pozostałych przedmiotów.

#### Obrażenia dystansowe

Występują w strzałach.

$f(x) = \mathop{\mathrm{round}}(0.04845 \cdot R(x))$

#### Obrażenia od ognia

Występują w:

-   broniach jednoręcznych,
-   broniach dystansowych,
-   różdżkach,
-   orbach,
-   strzałach.

Obrażenia te mogą występować również w broniach półtoraręcznych i dwuręcznych, ale ze względu na
brak dostępu do takich przedmiotów, nie są one tu uwzględnione.

$f(x) = \mathop{\mathrm{round}}(10 \cdot 0.0051c \cdot R(x))$,

gdzie $c$ wynosi:

-   $0.5$ dla broni jednoręcznych,
-   $0.71$ dla broni dystansowych,
-   $1.0$ dla różdżek,
-   $0.475$ dla orbów,
-   $0.15$ dla strzał.

#### Obrażenia od błyskawic

Bonus, który prawdopodobnie aktualnie liczony jest [niepoprawnie][bug].

#### Obrażenia od zimna

Występują w:

-   broniach jednoręcznych,
-   broniach dwuręcznych,
-   broniach dystansowych,
-   różdżkach,
-   orbach,
-   strzałach.

Obrażenia te mogą występować również w broniach półtoraręcznych, ale ze względu na brak dostępu do
takich przedmiotów, nie są one tu uwzględnione.

Spowolnienie: $f(x) = 0.01 \cdot \mathop{\mathrm{round}}(cx)$,

gdzie $c$ wynosi:

-   $0.95635$ dla broni jednoręcznych,
-   $0.95635$ dla broni dwuręcznych,
-   $0.733125$ dla broni dystansowych,
-   $1.0$ dla różdżek,
-   $0.733125$ dla orbów,
-   $0.733125$ dla strzał.

Obrażenia: $f(x) = \mathop{\mathrm{round}}(10 \cdot 0.0051c \cdot R(x))$,

gdzie $c$ wynosi:

-   $0.45$ dla broni jednoręcznych,
-   $0.675$ dla broni dwuręcznych,
-   $0.64$ dla broni dystansowych,
-   $0.85$ dla różdżek,
-   $0.425$ dla orbów,
-   $0.135$ dla strzał.

#### Niszczenie pancerza

Występuje w strzałach.

$f(x) = \mathop{\mathrm{round}}(0.0008c(x^2 + 130x + 620))$,

gdzie $c$ zależy od wymaganych przez przedmiot profesji:

-   h: $1.0$,
-   ht: $1.0$,
-   pozostałe profesje: $0$.

#### Niszczenie odporności

Występuje w:

-   broniach jednoręcznych dla samych paladynów,
-   broniach półtoraręcznych dla samych paladynów,
-   broniach dwuręcznych dla samych paladynów,
-   strzałach dla samych tropicieli.

Wartość zawsze wynosi $1$.

[capture]:
	https://web.archive.org/web/20221107192408/https://forum.margonem.pl/?task=forum&show=posts&id=514625&ps=0
	'Wayback Machine – zrzut tematu'
[wayback-machine]: https://web.archive.org/ 'Wayback Machine'
[bug]:
	https://forum.margonem.pl/?task=forum&show=posts&id=514101
	'„Wartości bonusów i wpływ ulepszeń na nie” – temat na forum Margonem'

## Potwory

Sekcja zostanie dodana w przyszłości.

## Mechaniki ogólne

Wzory i zależności ogólnych mechanik gry, które nie są związane bezpośrednio z poprzednimi sekcjami.

### Zwiększona liczba łupów

Aby grupa graczy miała szansę uzyskać z potwora więcej niż 1 łup, to spełniona musi być następująca
nierówność:

$$l + \max(\mathop{\mathrm{round}}(cl) + 4, 14) \le u$$

gdzie:

-   $l$ – poziom gracza, który ma najniższy poziom w grupie,
-   $u$ – poziom gracza, który ma najwyższy poziom w grupie,
-   $c$ – $0.2$ dla światów zwykłych i $0.4$ dla światów prywatnych.

Oznacza to, że dla gracza z poziomem $l$:

-   Dolny limit poziomu innych graczy w grupie to:

    $$\max\left( \min\left( \left\lceil \frac{l - 4.5}{1 + c} \right\rceil, \, l - 14 \right), \, 1 \right)$$

-   Górny limit poziomu innych graczy w grupie to:

    $$\min(\max(\mathop{\mathrm{round}}((1 + c)l) + 4, \, l + 14), \, 500)$$

### Czas odradzania gracza

$l$ oznacza poziom gracza.

Jeśli $l \le 20$, to czas odradzania gracza wynosi $10 + l$.

Jeśli $l > 20$, to czas odradzania gracza wynosi $30 + 10(l − 20)$.

Czas odradzania gracza wyrażony jest w sekundach.

### Zasięg widoczności herosów zwykłych

Aby gracz widział zwykłego herosa znajdującego się na tej samej mapie co gracz, to spełniona musi
być następująca nierówność:

$$(x_p - x_h)^2 + (y_p - y_h)^2 < 144,$$

gdzie:

-   $x_p$ – pozioma współrzędna pozycji gracza na mapie,
-   $y_p$ – pionowa współrzędna pozycji gracza na mapie,
-   $x_h$ – pozioma współrzędna pozycji herosa na mapie,
-   $y_h$ – pionowa współrzędna pozycji herosa na mapie.

Warunek ten jest konieczny, ale nie wystarczający. Obowiązują dodatkowo wymagania poziomowe dostępne
w oficjalnej mechanice gry.

### Zasięg udziału w walce grupy

Aby gracz znajdujący się w grupie uczestniczył w grupowej walce toczącej się na tej samej mapie, na
której gracz się znajduje, to spełniona musi być następująca nierówność:

$$\max(|x_p − x_a|, |y_p − y_a|) ≤ 20,$$

gdzie:

-   $x_p$ – pozioma współrzędna pozycji gracza na mapie,
-   $y_p$ – pionowa współrzędna pozycji gracza na mapie,
-   $x_a$ – pozioma współrzędna pozycji gracza inicjującego walkę na mapie,
-   $y_a$ – pionowa współrzędna pozycji gracza inicjującego walkę na mapie.
