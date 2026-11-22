# Katalog Seriali i ich Ocen (TV Series Catalog)

Repozytorium zawiera ustrukturyzowany zbiór danych przedstawiający wybrane seriale telewizyjne oraz streamingowe (*Better Call Saul*, *Arcane*, *From*, *Ojciec Mateusz*) wraz z ich ocenami, gatunkami, liczbą sezonów oraz platformami emisji. Nazwy pól i struktura danych zostały zapisane w języku angielskim zgodnie ze standardami projektowymi.

> **Cel projektu:** Przedstawienie tego samego zestawu danych w trzech różnych formatach tekstowych (**XML + XSD**, **JSON**, **CSV**) oraz analiza różnic w ich strukturze i sposobie odczytu.

---

## Zawartość repozytorium

* `series.xml` – główny zbiór danych zapisany w języku znaczników XML.
* `series_schema.xsd` – schemat XML Schema definiujący strukturę dokumentu oraz ograniczenia typów danych.
* `series.json` – reprezentacja danych w formacie JSON.
* `series.csv` – płaska reprezentacja tabelaryczna w formacie CSV.
* `README.md` – dokumentacja projektu.

---

## Porównanie formatów danych

| Cecha | XML + XSD | JSON | CSV |
| :--- | :--- | :--- | :--- |
| **Struktura danych** | Hierarchiczna (drzewiasta) | Hierarchiczna (obiekty i tablice) | Płaska (wiersze i kolumny) |
| **Definicja typów** | **Tak** – ścisła specyfikacja w `series_schema.xsd` | Brak wbudowanej (wymaga zewn. JSON Schema) | **Nie** – wszystko traktowane jest jako tekst |
| **Obsługa list (`genres`, `platforms`)** | Zagnieżdżone znaczniki `<genre>` / `<platform>` | Natywne tablice `["a", "b"]` | Wymaga własnego separatora wewnątrz komórki (`\|`) |
| **Rozmiar pliku (narzut)** | Duży (powtarzające się tagi zamykające) | Średni (klucze i nawiasy) | Najmniejszy (brak powtarzania nazw pól) |
| **Czytelność dla człowieka** | Dobra przy wcięciach | Bardzo wysoka | Dobra tylko dla prostych tabel |

### Główne różnice w praktyce:
1. **Kontrola struktury (`series_schema.xsd`):** Schemat XSD określa dokładną kolejność znaczników i dopuszczalne zakresy wartości (np. pole `<rating>` od `0.0` do `10.0`, a `<seasons>` jako dodatnia liczba całkowita).
2. **Zagnieżdżanie danych:** Seriale takie jak *Arcane* czy *From* mają po kilka gatunków i platform. W **XML** i **JSON** są one osobnymi elementami listy, natomiast w **CSV** trzeba było połączyć je znakiem `|` w jednej komórce.
3. **Atrybuty vs klucze:** W XML identyfikator `id` został zapisany jako atrybut znacznika (`<series id="1">`), podczas gdy w JSON i CSV jest zwykłym polem/kolumną.

---

## Jak czytać i otwierać pliki?

Wszystkie pliki są plikami tekstowymi kodowanymi w **UTF-8**, dzięki czemu można je otworzyć bezpośrednio w przeglądarce na GitHubie, w dowolnym edytorze tekstu (np. *Notatnik*, *VS Code*, *Notepad++*) lub w dedykowanych aplikacjach:

1. **`series.csv` (arkusze kalkulacyjne):**
   * Najwygodniej otworzyć w programach **Microsoft Excel**, **LibreOffice Calc** lub **Google Sheets**, wybierając przecinek (`,`) jako separator kolumn.
   * Na **GitHubie** plik po kliknięciu automatycznie wyświetla się jako czytelna tabela z możliwością wyszukiwania.
2. **`series.json` (przeglądarki i edytory):**
   * Można otworzyć bezpośrednio w przeglądarce internetowej (np. **Mozilla Firefox**, **Google Chrome**), która automatycznie sformatuje strukturę obiektów i pozwoli zwijać poszczególne rekordy.
3. **`series.xml` oraz `series_schema.xsd` (przeglądarki i edytory XML):**
   * Po otwarciu w przeglądarce internetowej dane wyświetlają się w formie przejrzystego drzewa znaczników, które można rozwijać i zwijać.

---

## Podsumowanie

* Do szybkiego przeglądania w formie tabeli najlepiej sprawdza się plik **`series.csv`**.
* Do lekkiej wymiany danych z zachowaniem list i zagnieżdżeń służy **`series.json`**.
* Do pełnego opisu struktury oraz narzucenia ścisłych reguł dotyczących typów i zakresu wartości wykorzystywana jest para plików **`series.xml`** i **`series_schema.xsd`**.
