# Katalog Seriali i ich Ocen (TV Series Catalog)

Prosty zestaw danych o kilku serialach (*Better Call Saul*, *Arcane*, *From*, *Ojciec Mateusz*) — ich ocenach, gatunkach, liczbie sezonów i platformach, na których można je obejrzeć. Nazwy pól są po angielsku, żeby zachować spójność w kodzie i schematach.

Całość powstała po to, żeby zestawić te same informacje w trzech popularnych formatach (**XML + XSD**, **JSON** i **CSV**) i zobaczyć w praktyce, czym różni się ich struktura, walidacja oraz wygoda odczytu.

---

## Co jest w środku?

- `series.xml` – baza seriali zapisana w XML-u.
- `series_schema.xsd` – schemat XSD pilnujący poprawnej struktury i typów danych w pliku XML.
- `series.json` – te same dane w formacie JSON.
- `series.csv` – płaska tabela w formacie CSV.
- `README.md` – opis projektu, który właśnie czytasz.

---

## Porównanie formatów

| Cecha | XML + XSD | JSON | CSV |
| :--- | :--- | :--- | :--- |
| **Struktura** | Drzewiasta (znaczniki) | Drzewiasta (obiekty i tablice) | Płaska (wiersze i kolumny) |
| **Walidacja typów** | Tak – wymuszana przez `series_schema.xsd` | Brak wbudowanej (potrzebny osobny JSON Schema) | Brak – wszystko jest zwykłym tekstem |
| **Listy (`genres`, `platforms`)** | Zagnieżdżone tagi `<genre>` i `<platform>` | Natywne tablice `["a", "b"]` | Sklejone w jednej komórce separatorem `\|` |
| **Rozmiar pliku** | Największy (powtarzające się tagi zamykające) | Średni (klucze i nawiasy) | Najmniejszy (same wartości po nagłówku) |
| **Czytelność** | Dobra przy odpowiednich wcięciach | Bardzo wysoka | Dobra tylko przy prostych danych |

### Co widać w praktyce?

- **Pilnowanie poprawności danych:** Dzięki `series_schema.xsd` parser od razu odrzuci błędny plik XML – schemat pilnuje kolejności tagów oraz zakresów wartości (np. `<rating>` musi mieścić się między `0.0` a `10.0`, a `<seasons>` być dodatnią liczbą całkowitą).
- **Kilka wartości w jednym polu:** Seriale takie jak *Arcane* czy *From* mają po kilka gatunków i platform. W XML-u i JSON-ie można je wygodnie zapisać jako listę, ale w płaskim CSV trzeba było ratować się separatorem `|` wewnątrz jednej komórki.
- **Sposób zapisu ID:** W XML-u identyfikator trafił jako atrybut do tagu otwierającego (`<series id="1">`), natomiast w JSON-ie i CSV jest po prostu kolejnym polem lub kolumną.

---

## Jak to otworzyć?

Wszystkie pliki są zapisane w **UTF-8**, więc podejrzysz je bezpośrednio tutaj na GitHubie albo w dowolnym edytorze kodu (np. VS Code). Jeśli wolisz wygodniejszy podgląd:

- **`series.csv`** najlepiej wrzucić do Excela, LibreOffice Calc lub Google Sheets (jako separator kolumn wybierz przecinek `,`). Na GitHubie plik od razu renderuje się jako przeszukiwalna tabela.
- **`series.json`** i **`series.xml`** (razem z `series_schema.xsd`) możesz przeciągnąć bezpośrednio do okna przeglądarki (Chrome, Firefox) – automatycznie sformatuje ona strukturę i pozwoli zwijać poszczególne gałęzie.

---

**Krótko mówiąc:** `series.csv` wygrywa, gdy chcesz szybko rzucić okiem na tabelkę, `series.json` najwygodniej przesyłać między aplikacjami, a duet `series.xml` + `series_schema.xsd` sprawdza się tam, gdzie liczy się rygorystyczna kontrola struktury i typów.
