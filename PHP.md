# PHP - podstawy

Okej, wiem, że trochę jest tu zerżnięte ze slajdów, ale ma to być streszczenie, a nie kompletnie nowy dokument. Ma to Tobie pomóc zrozumieć php najszybciej jak to możliwe. Mam nadzieję, że to streszczenie będzie pomocne.

*Autor: Hubert Lewandowski*



## O języku

**PHP** to język skryptowy do generowania stron WWW i budowania aplikacji webowych.
Działa po stronie serwera w czasie rzeczywistym. Charakteryzuje go:

- dynamiczne typowanie
- posiadanie własnego *Garbage Collectora*
- bycie [językiem wieloparadygmowym](https://www.math.uni.lodz.pl/~kowalcr/ParadygmatyZaoczne/Wprowadzenie.pdf)



## Pisanie skryptów

### Bloki z instrukcjami

Pliki PHP są zakończone rozszerzeniem **.php**. Sam PHP umieszczamy w blokach, które możemy mieszać z HTML-em (ale nie musimy).

Preferowana powszechnie instrukcja bloku to: **<?php ... ?\>**. 
Przykład:

```php
<?php
	phpinfo();
?>
```

> Powyższy kod wyświetla info o zainstalowanej wersji PHP na serwerze



### Zmienne

Zmienne w PHP są dynamicznie typowane, czyli **nie** wymagają definiowania ich typu. PHP posiada te same typy, co inne wysokopoziomowe języki, czyli *int, float, double, bool, string, object, itp*. 

Przykład:

```php
<?php
	$name = "James"; //string
	$age = 25; //integer
	$height = 187.8; //float
	$isTrue = true; //boolean
?>
```

> Tak, jak prawie wszędzie można definiować zmienne statyczne, stałe, itd.



#### Stałe

Są dwa sposoby definiowania stałych:

1. **const** - przetwarzanie na etapie generowania kodu (*od razu*)
2. **define()** - przetwarzanie w czasie działania skryptu (*w trakcie działania*)



Przykład:

```php
const PI = 3.14;
define('E', 2.71);

$katalog = '/opt/upload';
$plik = 'data.xml';

const SCIEZKA = $katalog . '/' . $plik; 	//NIEpoprawne!
define('SCIEZKA', $katalog . '/' . $plik);	//poprawne!
```

> Zauważ **brak** znaku dolara przy deklarowaniu zmiennych!



#### Statyczne

Działanie, jak w innych językach programowania.

```php
static $zmiennaStatyczna = 0;
```



#### Superglobalne

Są to zmienne, które są dostępne na obszarze całego projektu. Można je wywołać dosłownie wszędzie.

```php
$a = 1;

function myFunction() {
	global $a = 2;
	++$a;
}

myFunction();
echo $a; // $a = 3
```



### Ciągi znaków

Są 4 sposoby definiowania ciągów znaków:

1. Podwójne cudzysłowie **"..."**
2. Pojedyncze cudzysłowie **'...'**
3. Składnia heredoc
4. Składnia nowdoc



#### Podwójne cudzysłowie

Pozwala na parsowanie znaków specjalnych oraz zmiennych.

```php
$username = "Bob";
$points = 50;

$text = "$username ma:\t$points punktów!";
```

> Bob ma:	50 punktów!



#### Pojedyncze cudzysłowie

Nie parsuje znaków spec. ani zmiennych.

```php
$username = "Bob";
$points = 50;

$text = '$username ma:\t$points punktów!';
```

> $username ma:\t$points punktów!



#### Heredoc

Działa jak podwójny cudzysłów, ale i pozwala na deklarowanie w wielu linijkach kodu.

```php
$username = "Bob";
$points = 50;

$text = <<<TEKST
$username wygrał konkrurs!\n
Otrzymał wynik: $points puktów!\n
Gratulacje!!!
TEKST;
```

> Bob wygrał konkurs!
> Otrzymał wynik: 50 punktów!
> Gratulacje!!!

*TEKST to nazwa etykiety, która jest zastosowana w powyższej składni Heredoc.*



#### Nowdoc

Nie parsuje znaków spec. i pozwala na pisanie ciągu znaków w wielu linijkach. *Zauważ, że nazwa etykiety jest w cudzysłowu.*

```php
$username = "Bob";
$points = 50;

$text = <<<'TEKST'
$username wygrał konkrurs!\n
Otrzymał wynik: $points puktów!\n
Gratulacje!!!
TEKST;
```

> $username wygrał konkrurs!\n
> Otrzymał wynik: $points puktów!\n
> Gratulacje!!!



#### W skrócie

Parsuje:

- Podwójne cudzysłowie **"..."**
- Heredoc **<<<ETYKIETA**

Czysty tekst:

- Pojedyncze cudzysłowie **'...'**
- Nowdoc **<<<'ETYKIETA'**



#### Operatory do działania na ciągach znaków

##### Konkatenacja

Konkatenacja to inaczej łączenie ciągów znaków ze sobą - sklejanie w jeden ciąg.
Pozwala na to operator **kropki**.

```php
$name = "Jim";
$quote = $name." nie wie co to jest konkatenacja...";
```

> Jim nie wie co to jest konkatenacja...



##### Operator indeksowania

Ciągi znaków można traktować jako tablice znaków, których wartości na poszczególnych indeksach można zmieniać.

```php
$surname = "Jackson";
$surname[1] = '@';
$surname[5] = '0';
```

> J@cks0n



***Uwaga!*** *Wiele funkcji operują na bajtach ciągu, a nie na znakach. Dlatego polskie znaki specjalne mogą generować tzw. "krzaczki". Aby tego uniknąć należy sprawdzić czy istnieje odpowiednik danej funkcji, który operuje na bajtach, a nie na samych znakach.*



### NULL

W php istnieje typ specjalny NULL, który reprezentuje zmienną bez żadnej wartości.

```php
$variable = null;
```



### Instrukcja echo

Stosuje się ją do wypisywania treści ze skryptu. Wypisywana treść staje się częścią HTML-a. Są dwa sposoby pisania tej instrukcji i obie robią to samo:

- **<?php echo *$zdanie* ?\>**
- **<?= *$zdanie* ?\>**

```php+HTML
<?php
$message = "Hello World!";
?>

<div>
	<p>
		<?php echo $message ?>
	</p>
</div>
```

> Hello World!



### If-y, pętle, operatory, itp.

Jest identycznie, jak w JavaScript'cie. Proszę... Bez przesady.



### Przydatne operatory (z PHP 7)

```php
$a = null;
$b = 100;
$c = 250;

$foo = $a ?? $b ?? $c;	// zwraca pierwszą zmienną, z wartością inną niż NULL
$bar = $b <=> $c;		/* zwraca 0 gdy są równe,
						   wart. mniejszą od zera jeśli $b < $c
                           wart. większą od zera jeśli $b > $c
```



### Przeplatanie PHP z HTML-em

PHP zezwala na mieszanie kodu z HTML. To już wiadomo. Można jednak dodatkowo robić takie myki, że rozpoczynasz instrukcję w PHP, piszesz coś dotyczącego HTML-a, a następnie zamykasz tamtą instrukcje co była z PHP.

Aby zamknąć taki tag, można używać instrukcji z przedrostkiem **end-**. Czyli: endif, endfor, endforeach itp.

```php+HTML
<div>
    <?php foreach ($promocje as $promocja): ?>
        <?php if (jest_aktywna($promocja)): ?>
            <p>
                <span>...</span>
                ...
            </p>
        <?php endif ?>
    <?php endforeach ?>
</div>
```

> Wypisze tylko te wartości, w których funkcja **jest_aktywna()** zwróciła wartość



### Kończenie pracy skryptu

Funkcje poniżej przerywają działanie skryptu. Działają identycznie.

```php
exit;
exit();
die;
die();
```





# PHP - zaawansowany

Nie ma tu w zasadzie nic strasznego. Potrzebowałem sobie po prostu oddzielić prosty kontent od tego bardziej skompilowanego.



## Tablice

Zakładam, że wiesz, jak działa mechanizm tablic. Działają one tutaj identycznie, jak w [JavaScript'cie](https://www.w3schools.com/js/js_arrays.asp). Na końcu podam 2 przydatne funkcje, o których warto wiedzieć.



### Klucze i tablice

PHP pozwala na tworzenie kluczy do elementów z tablicy, czyli wartości z tablicy mogą posiadać jeszcze jakieś wartości przypisane do siebie. Te wartości mogą być **różnych** typów!

```php
$klienci = [
	'Anna' => 21,
	'Marek' => 27,
	'Barbara' => 45
];

foreach ($klienci as $imie => $wiek) {
	echo "$imie ma $wiek lat.".'<br/>';
}
```



### Tablice wielowymiarowe

```php
$zdjecia = [
	['tytul' => 'A', 'src' => "D:/zdj1.png"],
	['tytul' => 'B', 'src' => "D:/zdj2.png"],
	['tytul' => 'C', 'src' => "D:/image.jpg"],
];
```



### Przydatne funkcje

#### *array(..., ..., ...)*

Służy do inicjowania tablic:

```php
$subjects = array('matematyka', 'angielski', 'geografia');
```



#### *print_r($...)*

Wypisuje treść tablicy, w elegancki sposób:

```php
print_r($subjects);
```

> Array
> (
> 	[0] => matematyka
> 	[1] => angielski
> 	[2] => geografia
> )



## Dołączanie plików

W przypadku dużych projektów, warto podzielić sobie go na kilka plików. Aby wczytywać kod z zewnętrznych plików, należy korzystać z instrukcji:

```php
include 'sciezka/do/pliku.php';	// Dołącza plik, jeśli go nie ma to skrypt działa
require 'sciezka/do/pliku.php'; // Robi to samo, ale przerywa skrypt jeśli pliku nie ma
```

> **include** stosuje się zazwyczaj, kiedy chcesz wczytywać pliki *opcjonalne*.



Aby **jednorazowo** wczytać plik należy korzystać z podanych instrukcji:

```php
include_once 'sciezka/do/pliku.php';
require_once 'sciezka/do/pliku.php';
```



## Funkcje

Działają identycznie, jak w JavaScript'cie. Można sobie spojrzeć na [dokumentację](https://www.php.net/manual/en/functions.user-defined.php), jeśli ktoś nie jest przekonany.



### Przekazywanie argumentów przez referencje

Czyli działanie bezpośrednio na zmiennej, a nie jej kopii (jak przez wskaźnik do zmiennej). Stosuje się do tego ampersand (**&**).

```php
$a = 5;

function incrementBy10(&$number) {
	$number += 10;
}

echo $a; // 15
```



### Przekazywanie wartości przez referencje

Czyli odwoływanie się referencyjnie do elementów z funkcji. Przynajmniej tak to rozumiem z tego [przykładu](https://www.tutorialspoint.com/cplusplus/returning_values_by_reference.htm).

```php
function &find_contractor($name)
{
    static $contractors = [];
    if (!isset($contractors[$name])) {
    	$contractors[$name] = [
    	'rendezvous' => 1,
    	'status' => 'PENDING'
    	];
	}
	return $yellow_pages[$name];
}
$contractor = &find_contractor('WK');
//...
$contractor['status'] = 'CONFIRMED';
```



### Funkcje anonimowe

Nie posiadające nazwy, anonimowe. Mogą być przypisane do zmiennej, bądź stosowane, jako argument.

```php
$callback = function ($status) {
if ($status === 200) {
	//...
	} else {
	//...
}};

load_data($db, $callback);
```



## Zmienne zmiennych i zmienne funkcje

Wystarczy spojrzeć na przykład i można zrozumieć:

```php
// Zmienna zmiennych
$name = "Bob";
$myVariable = "name";

echo $$myVariable;
```



```php
// Zmienne funkcji
function pozdrowienie($name){
	return "Witaj, $name!";
}

$name = "Bob";
$shout = 'pozdrowienie';
echo $shout('Waldemar');
```



```php
// Mix tego i tego
function pozdrowienie($name){
	return "Witaj, $name!";
}

$name = 'Bob';
$choosen_function = 'pozdrowienie';
$choosen_name = 'name';
echo $choosen_name($$choosen_function);
```