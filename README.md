# skola
Učení ČJ, AJ, matematika, Člověk a jeho svět – jeden soubor `index.html` + JSON data. Běží na GitHub Pages.

## Struktura

| Soubor | K čemu |
| --- | --- |
| `index.html` | aplikace, vestavěné otázky a vtipy |
| `data/kraje-cr.json` | sada „Člověk a jeho svět – Kraje ČR“ (načítá se vždy) |
| `data/maps/cr.json` | mapa ČR: obrysy 14 krajů, řeky, města a hory |
| `questions.json` | seznam dalších sad, které se mají načíst (`{ "files": [...] }`) |

## Jak přidat novou sadu otázek

1. Nahraj soubor třeba `data/sada-2026-11-02.json`:
   ```json
   { "added": "2026-11-02",
     "questions": [ ... ],
     "jokes": [ { "q": "otázka", "a": "pointa" } ] }
   ```
2. Přidej ho do `questions.json`: `{ "files": ["data/sada-2026-11-02.json"] }`

Nové (neviděné) otázky se dítěti ukážou nahoře s nálepkou NOVÉ. Otázka se stejným `id` přepíše starší.
Celý popis formátu je na začátku `index.html` a v aplikaci v Rodičovském panelu (Otázky → Jak přidávat nové sady).

## Typy úkolů

`abcd` (výběr), `input` (psaní), `pairs` (spojování dvojic – klikání i přetahování), `order` (skládání),
`fill` (doplňování slov do věty), `map` (slepá mapa), `tip` (výuková karta).

```json
{ "id": "prv_x_01", "subject": "prv", "topic": "Řeky", "type": "fill",
  "question": "Doplň slova:", "text": "Vltava teče přes {{Prahu}} a ústí do {{Labe}}.", "extra": ["Odru"] }

{ "id": "prv_x_02", "subject": "prv", "topic": "Kraje", "type": "map",
  "map": "cr", "layer": "regions", "target": "jihocesky", "question": "Klikni na Jihočeský kraj." }

{ "id": "prv_x_03", "subject": "prv", "topic": "Řeky", "type": "abcd",
  "map": "cr", "highlight": ["rivers:vltava"], "show": ["rivers:labe", "rivers:morava"],
  "question": "Která řeka je zvýrazněná?", "options": ["Vltava", "Labe", "Morava"], "correct": "Vltava" }
```

Mapu lze přidat ke kterémukoliv typu (`map`, `highlight`, `show`, `labels`). `layer` u slepé mapy je
`regions` (kraje), `rivers` (řeky) nebo `points` (města, hory, pohoří); `candidates` omezí, co se na mapě zobrazí.
ID krajů, řek a bodů jsou v `data/maps/cr.json` (např. `jihocesky`, `vltava`, `brno`, `snezka`).
Další mapu (třeba Evropu) stačí přidat jako `data/maps/<nazev>.json` ve stejném formátu a odkázat se na ni přes `"map": "<nazev>"`.

Mapa ČR vznikla ze zjednodušených dat Natural Earth (public domain); Praha je zvětšená, aby šla snadno trefit.
Menší řeky a body jsou schematické.

## Vtipy za odměnu

Vtip se ukáže na konci bloku 10 a více úkolů, když dítě odpovědělo napoprvé správně aspoň na 90 % z nich (9 z 10).
Oprava chyb a opakování chyb vtip nespouští. Vtipy se neopakují, dokud se nevystřídají všechny.
Konstanty `JOKE_BLOCK` a `JOKE_RATIO` jsou na začátku skriptu v `index.html`.
