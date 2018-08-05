# Gulp Notes

<br/>

## O Gulp'ie

**Gulp** to narzędzie służace do automatyzacji dużych i czasochłonnych zadań. Jest on oparty na środowisku **Node.js**, który głównie wspiera język *JavaScript*, jakim akurat Gulp się zajmuje. Sam Gulp wykorzystywany jest przez osoby zajmujące się technologiami: ***HTML5***, ***CSS*** czy ***JavaScript***. Gulp jest określany mianem najprostszego języka do automatyzacji zadań na stronach, dlatego jest dedykowany dla <u>początkujących-średnio zaawanowanych</u> programistów.

<br/><br/>

## Podstawy

<br/>

### Teoria

Gulp składa się z 4 głównych funkcji. Jest to m.in.  Gulp:

- **task** - definicja zadań
- **src** - (*ang. <u>s</u>ou<u>rc</u>e*) info. o wejściu plików czy folderów, na których będzie on operował
- **dest** - (*ang. <u>dest</u>ination*) miejsce zapisywania wyników przebiegu operacji Gulp'a. (output)
- **watch** - nasłuchiwanie zmian w ścieżkach plików, gdzie w przypadku ich modyfikacji, Gulp uruchomi odpowiednią instrukcję napisaną przez nas

<br/>

Przydatne metody to:

- **pipe** - stosowana w przypadku użycia z np. funkcją ***return***, która zawiera listę instrukcji w jednej linijce. Kod zapisany z użyciem "pipe" wyglądałby tak:

  ```js
  return gulp.src(...).pipe(INSTRUKCJA_1).pipe(INSTRUKCJA_2);
  ```

  Jak widać, dzięki tej metodzie możemy używać wielu instrukcji naraz w kłopotliwych sytuacjach.



<br/><br/><br/>

### Deklarowanie Gulp'a w skrypcie

Na samym początku należy utworzyć plik o nazwie **gulpfile.js**. Trzeba tak go nazwać, ponieważ ta nazwa jest informacją dla kompilatora, że konkretnie ten właśnie plik jest napisany w języku Gulp. W pierwszej linijce piszemy:

```js
var gulp = require('gulp');
```

- **var** - (*ang. <u>var</u>iable*) deklaracja zmiennej
- **require** - informacja o ***wymogu*** załadowania danego modułu.

<br/>

Podana linijka kodu informuje, że aby skrypt poprawnie działał to musi on wczytać moduł czy plugin o nazwie **gulp** - czyli naszego Gulp'a.

> **Wszystkie pluginy** również się w ten sposób **definiuje!!!**

<br/><br/><br/><br/>

### Wykonywanie zadań

Aby stworzyć zadanie dla Gulp'a należy użyć danej składni:

```js
gulp.task('nazwa_zadania', ['funkcje_do_wywołania'], function() {...});
```

- **gulp.task** - definicja zadania
- *nazwa_zadania*
- *funkcje_do_wywołania* - (opcjonalne) tablica z listą zadań, które mają zostać wykonane w czasie działania instrukcji
- **function** - instrukcja zadań do wykonania w danym zadaniu

<br/>

Przykład:

```js
gulp.task('test', function() {
    console.log("Hello World!");
});
```

Podane zadanie po wywołaniu wypisuje: "Hello World!".

<br/>

> **Jak to sprawdzić?**
>
> Uruchom wiersz poleceń, a następnie używając komend przejdź do folderu projektu. Następnie wpisz komendę:
>
> ```sh
> gulp test
> ```
>
> Jeżeli wszystko było zapisane ***bezbłędnie*** to wsród tekstu infromacji o kompilowaniu się pliku dostrzeżesz wyjście skryptu, które w przypadku napisanego przykładu, zostanie wyświetlony tekst: "Hello World!".

<br/>

> **Czy wiesz, że...?**
>
> Gulp może posiadać swoje "zadanie domyślne", które jest wywołane po prostu komendą:
>
> ```sh
> gulp
> ```
>
> Aby to zrobić należy nazwać zadanie **"default"**. Polecam wypróbowanie tego. Możesz to zrobić przykładowo zmieniając nazwę naszego przykładowego zadania z "test" na "default".

<br/><br/><br/><br/>

## Instalacja Gulpa

Aby zainstalować środowisko Gulp, należy uprzednio zainstalować platformę **Node.js**. Moją rekomendacją jest zainstalowanie wersji **LTS** - "Last Stable", ponieważ, jak sama nazwa wskazuje to jest ona najbardziej stabilna.

<br/>

### Krok 1

Po zainstalowaniu otwórz kolejno:

> Start > Wiersz polecenia (w skrócie *"cmd"*)

<br/><br/>

### Krok 2

Wpisz w konsolę, w celu sprawdzenia czy wszystko działa:

```js
node -v
```

- **node** - informacja o tym, że chcemy się odwołać do programu ***node.js***
- **-v** - *(ang. version)* wyświetla wesje programu.

Jeżeli pokazał Ci się numer tej samej wersji node'a, którą pobrałeś/aś to wszystko jest w porządku.

<br/><br/>

### Krok 3

Przejdź do folderu projektu używając komendy **cd**:

```sh
cd C:\<ścieżka do folderu projektu>
```

<br/><br/>

### Krok 4

Aby rozpocząć działanie z Gulp'em, **Node.js** musi stworzyć nam specjalną przestrzeń roboczą w folderze projektu. W tym celu napisz:

```sh
npm init
```

- **npm** - *(ang. Node Package Manager)* informacja, że chcemy korzystać z menadżera paczek Node.js
- **init** - *(ang. initialize)* komunikat, iż mamy zamiar stworzyć nowy projekt i chcemy aby ***npm*** wszystko nam zainstalowało i skonfigurowało

<br/>

Wyświetlą się zapytania dotyczące struktury projektu. Podane w okrągłych nawiasach informacje to *domyślnie proponowane wartości* dla poszczególnych konfiguracji. Jeżeli chcesz zostawić tak, jak jest to klikasz ***enter***. Możesz pominąć wszystkie zapytania.

<br/><br/>

### Krok 5

Aby w końcu zainstalować język Gulp. Wpisz:

```sh
npm install -g gulp
```

- **-g** - *(ang. globally)* argument oznacza, że platforma Gulp będzie można wywołać dosłownie z każdego miejsca na komputerze. Może być to o tyle, iż nie trzeba będzie każdorazowo wymagać instalacji przy nowych projektach.
