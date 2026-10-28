# Powtórka — 28.10.2026

**Klasa:** 5E MTAI, grupa 1  
**Pliki:** `index.html` + `script.js`  
**Ściąga:** `PODSUMOWANIE.md`

Otwórz `index.html` w przeglądarce. Skrypt jest podpięty. Kod pisz w `script.js`. Po zapisaniu odśwież stronę.

Najpierw osiem krótkich pytań (tematy z demo). Potem sześć zadań na stronie, od 1 do 6.

---

## Zadanie 1 — status zlecenia

**Cel:** po kliknięciu zmienić tekst i kolory jednego elementu.

**Elementy:**
- przycisk `#btn-z1`
- akapit `#status-z1`

**Zrób:**
1. Podepnij kliknięcie do id`#btn-z1`.
2. Znajdź `#status-z1` po id.
3. Ustaw tekst na `Status: w naprawie`.
4. Ustaw `backgroundColor` i `color`.

**Zaliczone, gdy:** po kliknięciu widać nowy tekst i zmienione kolory.

---

## Zadanie 2 — kafelki części

**Cel:** jednym kliknięciem zmienić wygląd wszystkich elementów z klasą `czesc`.

**Elementy:**
- przycisk id `btn-z2`
- kilka elementów `.czesc`

**Zrób:**
1. Podepnij kliknięcie do `#btn-z2`.
2. Zbierz elementy przez klasę.
3. W pętli `for` ustaw każdemu bg kolor i kolor czcionki.

**Zaliczone, gdy:** po kliknięciu kolor zmienia się na wszystkich kafelkach, nie tylko na jednym.

---

## Zadanie 3 — nazwa klienta (String)

**Cel:** odczytać tekst z pola i pokazać wyniki metod String.

**Elementy:**
- pole `#nazwa-z3`
- przycisk `#btn-z3`
- panel `#wynik-z3`

**Zrób:**
1. Po kliknięciu `#btn-z3` odczytaj `value` z `#nazwa-z3`.
2. W `#wynik-z3` wypisz:
   - `length`
   - `indexOf("a")`
   - `toUpperCase()`
   - `toLowerCase()`
   - `substr(0, 3)` albo `replace(...)`
3. Wypisz samo nazwisko
**Zaliczone, gdy:** zmiana tekstu w polu i ponowne kliknięcie dają wyniki dla nowej wartości. Dla `Jan Kowalski`: długość to 12, `indexOf("a")` to 1, `substr(0, 3)` to `Jan`, dodatkowo wytnij samo nazwisko.

---

## Zadanie 4 — kafelek i mysz

**Cel:** cztery reakcje na tym samym elemencie.

**Elementy:**
- kafelek `#kafelek-z4`

**Zrób:**
1. `onclick` — zmień treść, np. `Przyjęte do naprawy`.
2. `ondblclick` — inna treść, np. `Gotowe do odbioru`.
3. `onmouseover` — dodaj klasę w css z kolorem bg i zmień klasę na ten event.
4. `onmouseout` — przywróć tło (pusty string w przy background oddaje kolor z CSS).

**Zaliczone, gdy:** widać osobną reakcję na klik, podwójny klik, najechanie i zejście kursora. Przy podwójnym kliknięciu przeglądarka najpierw puszcza `click`.

---

## Zadanie 5 — lista usterek

**Cel:** dodać pozycję, usunąć ostatnią i podmienić pierwszą.

**Elementy:**
- lista `#lista-z5`
- `#btn-dodaj-z5`, `#btn-usun-z5`, `#btn-podmien-z5`
- panel `#wynik-z5`

**Zrób:**
1. Dodaj: element li , ustaw tekst, i dodaj JSem do `#lista-z5`.
2. Usuń: jeśli jest ostatni potomek, to usuń. Pusta lista nie może rzucić błędu.
3. Podmień: jeśli jest pierwszy element, zrób nowe element listy i zamień.


**Zaliczone, gdy:** da się dodawać, kasować ostatni punkt i podmieniać pierwszy. Usuwanie przy pustej liście pokazuje komunikat, a konsola jest czysta.

---

## Zadanie 6 — formularz zgłoszenia

**Cel:** odczytać radio, checkbox i select, podświetlić pozycje z klasą.

**Elementy:**
- radio `name="priorytet"`
- checkbox `#chk-backup`
- select `#usluga-z6`
- podpowiedź `#hint-z6`
- przycisk `#btn-z6`
- panel `#wynik-z6`
- elementy `.pozycja` na liście (jeden punkt listy tej klasy nie ma)

**Zrób:**
1. Na `#usluga-z6` podepnij event 'zmiany' i zmieniaj tekst `#hint-z6` zależnie od wybranej opcji.
2. Po kliknięciu `#btn-z6` odczytaj:
   - zaznaczone radio ,
   - stan checkboxa ,
   - wartość selecta.
3. Wypisz podsumowanie w `#wynik-z6`.
4. ustaw tym elementom z klasą pozycja wyróżnienie (klasa albo `style`). Punkt bez klasy `pozycja` zostaje bez zmian.

**Zaliczone, gdy:** zmiana selecta aktualizuje hint, podsumowanie zgadza się z formularzem, a podświetlone są tylko `.pozycja`.

---
