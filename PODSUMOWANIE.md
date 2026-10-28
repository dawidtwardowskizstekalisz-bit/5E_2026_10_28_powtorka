# Co macie umieć — JavaScript, grupa 1

**Klasa:** 5E MTAI, grupa 1  
**Zakres:** folder `2026_09_14__powtorka_js_dom` — cztery strony: DOM, operacje na elementach, zdarzenia, formularze i String. Do tego ćwiczenia z 23.09 i 30.09, które w tym folderze są.

Na sprawdzianie piszecie obsługę zdarzenia i zmianę strony: znaleźć element, odczytać pole, zmienić tekst albo styl, dodać lub usunąć element.

## Poza sprawdzianem

To było na lekcji 7.10 albo jako zadanie dodatkowe. W zakresie folderu tego nie ma:

- `isNaN` i telefon o długości dokładnie 9 znaków
- licznik znaków w `textarea` na zdarzeniu `oninput`
- właściwość `disabled`
- `onsubmit` i `event.preventDefault()`
- wiersze tabeli (`tr`, `td`)
- wgrywanie obrazka (`FileReader`, `URL.createObjectURL`)

## Było na demo — też jest w zakresie

Tych rzeczy nie pisaliście jako własnego zadania. Są na stronach powtórki i wchodzą na sprawdzian. Krótko, po jednej linii, w `ZADANIA.md` na początku.

- `getElementsByTagName` — kolekcja po nazwie tagu
- `setAttribute` / `getAttribute` — ustawienie i odczyt atrybutu
- `innerHTML` — treść razem ze znacznikami HTML
- `document.write` — wpisuje HTML i zastępuje dokument
- `ondblclick` — podwójny klik
- `onkeydown`, `onkeypress`, `onkeyup` — klawiatura (`event.key`)
- `onload` — po załadowaniu strony
- `onresize` — po zmianie rozmiaru okna
- `onfocusin` / `onfocusout` — fokus wszedł w pole albo je opuścił
- `search` i `substr` — obok `indexOf` i reszty metod String

---

## 1. DOM — wyszukiwanie i zmiana

| Metoda | Co zwraca |
| --- | --- |
| `document.getElementById("status")` | jeden element o tym `id`, albo `null` |
| `document.querySelector("#lista .pozycja")` | pierwszy element pasujący do selektora CSS, albo `null` |
| `document.querySelectorAll(".pozycja")` | wszystkie pasujące |
| `document.getElementsByClassName("czesc")` | kolekcja elementów z klasą `czesc` |
| `document.getElementsByName("priorytet")` | kolekcja elementów z tym `name` (radio) |
| `element.getElementsByTagName("p")` | kolekcja tagów `p` wewnątrz `element` |

`getElementById` i `querySelector` dają jeden element. Reszta daje kolekcję — idziesz po niej pętlą `for`.

```js
const czesci = document.getElementsByClassName("czesc");
for (let i = 0; i < czesci.length; i++) {
  czesci[i].style.backgroundColor = "#e0f2f1";
  czesci[i].style.color = "#0d6e6e";
}
```

Tekst na stronie to `textContent`. HTML ze znacznikami to `innerHTML`.

```js
document.getElementById("status").textContent = "Status: w naprawie";
document.getElementById("box").innerHTML = "<strong>Nowa treść</strong>";
```

`textContent` wstawia znaki tak, jak są. `innerHTML` czyta `<strong>` jako znacznik.

Styl przez obiekt `style`. W CSS jest myślnik, w JS camelCase.

| CSS | JS |
| --- | --- |
| `background-color` | `style.backgroundColor` |
| `color` | `style.color` |
| `font-size` | `style.fontSize` |
| `font-style` | `style.fontStyle` |
| `font-weight` | `style.fontWeight` |
| `list-style-type` | `style.listStyleType` |
| `text-decoration` | `style.textDecoration` |

```js
const panel = document.getElementById("panel");
panel.style.backgroundColor = "#e0f2f1";
panel.style.fontWeight = "bold";
panel.style.textDecoration = "line-through";
```

Pusty string cofa styl ustawiony w JS: `panel.style.backgroundColor = ""`.

Atrybut ustawiasz właściwością albo `setAttribute`. Odczyt: właściwość albo `getAttribute`.

```js
const link = document.getElementById("demo-link");
link.setAttribute("href", "https://www.w3schools.com");
link.setAttribute("target", "_blank");
link.getAttribute("href");

const img = document.getElementById("demo-img");
img.alt = "Naprawa komputera";
img.title = "Podpowiedź po najechaniu";
```

Klasę CSS dodajesz i zdejmujesz przez `classList`:

```js
element.classList.add("hit");
element.classList.remove("hit");
```

---

## 2. Operacje na elementach

`createElement` tworzy element w pamięci. Na stronie go nie ma, dopóki nie wstawisz go rodzicowi.

```js
const lista = document.getElementById("lista");
const li = document.createElement("li");
li.textContent = "Wymiana pasty";
lista.appendChild(li);
```

| Metoda | Co robi |
| --- | --- |
| `appendChild(nowy)` | dokleja `nowy` jako ostatnie dziecko |
| `removeChild(stary)` | usuwa `stary` z rodzica |
| `replaceChild(nowy, stary)` | w rodzicu podmienia `stary` na `nowy` |
| `lastElementChild` | ostatnie dziecko-element, albo `null` |
| `firstElementChild` | pierwsze dziecko-element, albo `null` |

Usuwanie ostatniej pozycji. Najpierw sprawdź, czy lista coś ma — na pustej `removeChild` rzuca błąd.

```js
const ostatni = lista.lastElementChild;
if (ostatni) {
  lista.removeChild(ostatni);
}
```

Podmiana pierwszego punktu:

```js
const stary = lista.firstElementChild;
if (stary) {
  const nowy = document.createElement("li");
  nowy.textContent = "PILNE: odzysk danych";
  lista.replaceChild(nowy, stary);
}
```

`document.write("...")` wpisuje HTML do dokumentu. Wywołane po załadowaniu strony kasuje to, co już jest, i zostawia sam nowy zapis. Na demo jest schowane w ramce, żeby nie zniszczyć powtórki.

---

## 3. Zdarzenia

Przypisanie funkcji do właściwości `on...`. Funkcję podajesz bez nawiasów — nawiasy odpalają ją od razu, przy podpinaniu.

```js
document.getElementById("btn").onclick = function () {
  document.getElementById("status").textContent = "Status: w naprawie";
};
```

To samo przez `addEventListener`. Pierwszy argument to nazwa zdarzenia bez `on`.

```js
document.getElementById("btn").addEventListener("click", function () {
  document.getElementById("status").textContent = "Status: w naprawie";
});
```

Mysz:

| Właściwość | Kiedy |
| --- | --- |
| `onclick` | pojedynczy klik |
| `ondblclick` | podwójny klik |
| `onmouseover` | kursor wszedł na element |
| `onmouseout` | kursor zszedł z elementu |

Przy podwójnym kliknięciu przeglądarka najpierw puszcza `click`, potem `dblclick`.

Klawiatura. W funkcji dostajesz obiekt zdarzenia. `event.key` to nazwa klawisza (`"Enter"`, `"a"`). `event.code` to fizyczny klawisz.

| Właściwość | Kiedy |
| --- | --- |
| `onkeydown` | klawisz poszedł w dół |
| `onkeypress` | klawisz, który wpisuje znak |
| `onkeyup` | klawisz puściłeś |

Enter w polu — skopiuj wartość i wyczyść pole:

```js
const pole = document.getElementById("pole");
pole.onkeydown = function (event) {
  if (event.key === "Enter") {
    document.getElementById("wynik").textContent = pole.value;
    pole.value = "";
  }
};
```

Okno i fokus:

| Właściwość | Kiedy |
| --- | --- |
| `window.onload` | strona jest załadowana |
| `window.onresize` | zmienił się rozmiar okna (`window.innerWidth`, `window.innerHeight`) |
| `onfocusin` | fokus wszedł w pole (można pisać) |
| `onfocusout` | fokus opuścił pole |

```js
window.onload = function () {
  document.getElementById("wynik").textContent = "Strona załadowana";
};

document.getElementById("pole").addEventListener("focusin", function () {
  document.getElementById("wynik").textContent = "Pole ma fokus";
});
```

`onchange` na `select` odpala się po zmianie opcji. `oninput` na suwaku `range` odpala się przy każdym ruchu i służy do podglądu liczby.

---

## 4. Formularze i String

Odczyt pól:

| Pole | Odczyt |
| --- | --- |
| `input` text, password, number | `.value` (zawsze string) |
| `textarea` | `.value`, długość: `.value.length` |
| `select` | `.value` wybranej opcji |
| checkbox | `.checked` to `true` albo `false` |
| radio | `getElementsByName` i pętla, szukasz `.checked === true` |

```js
const opcje = document.getElementsByName("priorytet");
let wybrany = "(brak)";
for (let i = 0; i < opcje.length; i++) {
  if (opcje[i].checked) {
    wybrany = opcje[i].value;
  }
}
```

Hasło na stronie pokazujesz przez długość, nie przez treść: `haslo.length`.

Zaznaczenie wszystkich `.pozycja` i wyróżnienie:

```js
const pozycje = document.querySelectorAll(".pozycja");
for (let i = 0; i < pozycje.length; i++) {
  pozycje[i].style.backgroundColor = "#e0f2f1";
}
```

Element bez klasy `pozycja` ta pętla omija.

Metody String **nie zmieniają** oryginału. Wynik zapisujesz albo wstawiasz na stronę.

```js
const t = document.getElementById("nazwa").value;
t.length;              // liczba znaków, bez nawiasów
t.indexOf("a");        // indeks pierwszej litery "a", albo -1
t.search("ski");       // indeks dopasowania, albo -1
t.substr(0, 3);        // 3 znaki od indeksu 0
t.replace("Jan", "Anna");
t.toUpperCase();
t.toLowerCase();
```

`indexOf` szuka zwykłego tekstu. `search` przyjmuje też wyrażenie regularne. Dla zwykłego kawałka tekstu obie zwracają indeks albo `-1`.

```
J a n   K o w a l s k i
0 1 2 3 4 5 6 7 8 9 10 11
indexOf("a")  → 1
search("ski") → 9
substr(0, 3)  → "Jan"
```

E-mail: pusty albo bez `@` to błąd. Poprawny pokazujesz małymi literami.

```js
const email = document.getElementById("email").value;
const wynik = document.getElementById("wynik");
if (email.length === 0 || email.indexOf("@") === -1) {
  wynik.textContent = "Błąd: podaj e-mail ze znakiem @";
  wynik.style.backgroundColor = "#fce8e6";
} else {
  wynik.textContent = email.toLowerCase();
  wynik.style.backgroundColor = "#e0f2f1";
}
```

`indexOf("@") === -1` znaczy: znaku `@` w tekście nie ma.
