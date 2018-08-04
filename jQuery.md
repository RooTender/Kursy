# jQuery Notes
<br/>

## O jQuery

**jQuery** to biblioteka programistyczna dla języka <u>Javascript</u>. Pozwala na robienie multum rzeczy sto razy szybciej. Dodatkowo potrafi dynamiczniej posługiwać się **DOM**'em, **CSS**'em, **HTML**'em  oraz **AJAX**'em. Zaleca się ustawianie go w stopce strony internetowej, jednak powinien być on zarówno wczytywany przez stronę w <u>pierwszej kolejności</u>.
<br/><br/><br/><br/>

## Podstawy

### Działanie jQuery

Wygląd działania jQuery:

```javascript
$(selector).action()
```

- ***$*** - informacja, że chcesz skorzystać z jQuery
- ***(selector)*** - to, czemu konkretnie chcesz przypisać funkcję
- ***action()*** - metoda/funkcja/akcja, która ma zostać wywołana.

<br/><br/>

Przykłady:

```javascript
$("p").hide()  // ukrywa wszystkie elementy <p>
$(".demo").hide()  // ukrywa wszystkie elementy z class="demo"
$("#demo").hide()  // ukrywa wszystkie elementy z id="demo"
```

<br/><br/>

> **Czy wiesz, że...?**
>
> Selektory możesz również definiować w podany sposób:
>
> ```javascript
> $("p[id=test]").hide()  // ukrywa wszystkie elementy <p> o id równym nazwie "test"
> ```
>
> lub
>
> ```javascript
> $("p#test").hide()  // ukrywa wszystkie elementy <p> o id równym nazwie "test"
> ```

<br/><br/><br/><br/>

### Eventy

Jednym z najpopularniejszych eventów jest funkcja **ready**. Jest używania w przypadkach, gdy chcemy, aby nasz skrypt zaczął działać <u>po wczytaniu</u> naszej strony wraz z komponentami od A do Z. Można ją zadeklarować na dwa sposoby.

Dłuższy - *bardziej czytelny*:

```javascript
$(document).ready(function() {
    //Twój kod jQuery
});
```

<br/><br/>

Krótszy - *szybszy w napisaniu*:

```javascript
$(function() {
    //Twój kod jQuery
});
```

<br/><br/>

> **Czy ty to też widzisz?**
>
> jQuery pozwala nie tylko na prostsze i szybsze pisanie skryptów, ale i jednocześnie przyzwala na tworzenie <u>**funkcji w tej samej funkcji!**</u> - *nested methods*

<br/><br/><br/><br/>

### Manipulacja CSS'em

Załóżmy, że chcemy stworzyć skrypt, który będzie zmieniał jakieś atrybuty CSS'a. Aby zintegrować ten pomysł z jQuery należy napisać odpowiednią funkcję. Mniej więcej taką:

```javascript
$("#logo").css({
    color:'red',
    'font-weight':'bold',
    textAlign: 'center'
});
```

Dokonajmy analizy. Skrypt wskazuje na obiekt o id **logo**, a następnie wywołuje funkcję **css**, która ustawia kolor tekstu na ***czerwony***. Jest on również ***pogrubiony*** i ***wyśrodkowany***.

<br/><br/>

> **Różne sposoby zapisu**
>
> W domyślnym pliku CSS atrybuty ustalające gubość czcionki, czy pozycjonowanie tekstu, są zapisane kolejno w ten sposób: **font-weight**, **text-align**.
>
> jQuery nie zezwala na stosowanie myślników przy deklarowaniu funkcji zajmującej się CSS'em. Dlatego należy albo <u>wsadzić nazwę atrybutu pomiędzy pojedyncze cudzysłowie</u>, albo <u>pozbyć się myślnika i zacząć drugi wyraz od wielkiej litery</u>.

<br/><br/>

Dodawanie klas do elementów:

```javascript
$(function() {
    $('li').on('click', function() {
    	$(this).addClass('klasa');
    });
});
```
<br/><br/><br/><br/>

### Zmienne

Wyobraź sobie, że masz stronę internetową z czterema guzikami, które mają tą samą klasę **panel-button**, jednak inne - unikatowe wartości w atrybutach ***data-panelID***. Chcesz, aby, za każdym razem, kiedy klikniesz jeden z przycisków, <u>wyskakiwał Ci komunikat</u> informujący o wartości tego atrybutu (chodzi wciąż o data-panelID) oraz <u>ukrywało ten panel</u>.

```javascript
$('.panel-button').on('click', function() {
    
    var panelID = $(this).attr('data-panel');	//  utwórz zmienną 'panelID', która będzie 													przechowywała wartość atrybutu 'data-panel'
    
    alert(panelID);							  //  wyświetl komunikat ze zmienną
    
    $('#'+panelID).toggle();				   //  ukryj panel poprzez zastosowanie 														konkatenacji
});
```

**Podsumowanie:**

- ***var*** - deklaracja zmiennej
- ***$(this)*** - informacja, że chcemy nawiązać do obiektu, którego ten skrypt dotyczy
- ***.attr*** - funkcja, która pobiera wartość z określonego **atr**ybutu
- ***alert*** - potrzebna dokumentacja JavaScripta?! No bez przesady...
- *konkatenacja* - sposób łączenia dwóch ciągów wyrazów. Tutaj ją zastosowaliśmy w celu znalezienia panelu ID ('**#**'), który jest określony w zmiennej (**panelID**).

<br/><br/><br/><br/>

### Poruszanie się po DOM'ie

**DOM** *(Document Object Model)* jest to API pozwalające na modyfikowanie, przetwarzanie, usuwanie elementów dokumentu takiego jak <u>HTML</u> czy <u>XML</u>.

Aby znaleźć konkretną rzecz w dokumencie musimy standardowo użyć początkowej składni wraz selektorem **_$(selektor)_**, a następnie dodać akcję, w której jest zawarte, co konkretnie chcemy zaznaczyć.

Kilka przykładów na podstawie kodu

Kod HTML:

```html
<ul class="list">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>
    	<ul class="sublist">
      		<li>4</li>
    		<li>5</li>
    		<li>6</li>
    	</ul>
    </li>
</ul>
```

<br/><br/>

Kod jQuery:

```javascript
$('li')				//  zaznacza wszystkie elementy <li>
$('li').first()		        //  1
$('li').last()		        //  6
$('li').eq(0)		        //  1, ponieważ zaznacza <li> o index'ie 0'wym

$('ul:first').children() 	//  Oznacza wszystkie 'dzieci' pierwszego obiektu <ul>
$('li:first').siblings() 	//  Zaznacza całe 'rodzeństwo' pierwszego obiektu <ul>
$('li:first').parent()	 	//  Zaznacza 'rodzica' pierwszego obiektu <li>
$('li:first').prev()	 	//  Zaznacza element ZA pierwszym el. <li>
$('li:first').next()	 	//  Zaznacza element PRZED pierwszym el. <li>

$('li').eq(4).parent()	 	//  Zaznacza obiekt <ul class="sublist">
$('li').eq(4).parent().prev()  	//  4

```

