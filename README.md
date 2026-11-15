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

## Obrázky (autoři)

Obrázky v `img/` jsou z Wikimedia Commons (volné licence). V aplikaci se autoři neuvádějí, jen tady.
Do úkolu se přidávají polem `"imageUrl": "img/rostliny/lipa.jpg"` (a `"emoji"` jako záloha, když se obrázek nenačte).

| Soubor | Autor | Licence | Zdroj |
| --- | --- | --- | --- |
| `img/rostliny/bazalka.jpg` | Andrew Bossi | CC BY-SA 2.5 | [Commons](https://commons.wikimedia.org/wiki/File:2008_03_15_-_Ocimum_basilicum_7.JPG) |
| `img/rostliny/bez.jpg` | neuvedeno | Public domain | [Commons](https://commons.wikimedia.org/wiki/File:Illustration_Sambucus_nigra0.jpg) |
| `img/rostliny/durman.jpg` | neuvedeno | Public domain | [Commons](https://commons.wikimedia.org/wiki/File:Illustration_Datura_stramonium0.jpg) |
| `img/rostliny/hermanek.jpg` | Franz Eugen Köhler, in Köhler's Medizinal-Pflanzen | Public domain | [Commons](https://commons.wikimedia.org/wiki/File:Matricaria_recutita_-_K%C3%B6hler%E2%80%93s_Medizinal-Pflanzen-091.jpg) |
| `img/rostliny/kopriva.jpg` | neuvedeno | Public domain | [Commons](https://commons.wikimedia.org/wiki/File:Illustration_Urtica_dioica0.jpg) |
| `img/rostliny/majoranka.jpg` | Dobromila | CC BY-SA 4.0 | [Commons](https://commons.wikimedia.org/wiki/File:Majeranek2.jpg) |
| `img/rostliny/mata.jpg` | Franz Eugen Köhler, Köhler's Medizinal-Pflanzen | Public domain | [Commons](https://commons.wikimedia.org/wiki/File:Mentha_%C3%97_piperita_-_K%C3%B6hler%E2%80%93s_Medizinal-Pflanzen-095.jpg) |
| `img/rostliny/naprstnik.jpg` | Jensflorian | CC BY-SA 3.0 | [Commons](https://commons.wikimedia.org/wiki/File:Digitalis_Purpurea.jpg) |
| `img/rostliny/zvonek.jpg` | Hans Hillewaert | CC BY-SA 3.0 | [Commons](https://commons.wikimedia.org/wiki/File:Campanula_rotundifolia_(plant).jpg) |
| `img/rostliny/spenat.jpg` | Rasbak | CC BY-SA 3.0 | [Commons](https://commons.wikimedia.org/wiki/File:Spinacia_oleracea_Spinazie_bloeiend.jpg) |
| `img/rostliny/lipa.jpg` | Franz Eugen Köhler, Köhler's Medizinal-Pflanzen | Public domain | [Commons](https://commons.wikimedia.org/wiki/File:Tilia_cordata_-_K%C3%B6hler%E2%80%93s_Medizinal-Pflanzen-139.jpg) |
| `img/rostliny/pampeliska.jpg` | Walther Otto Müller | Public domain | [Commons](https://commons.wikimedia.org/wiki/File:Taraxacum_officinale_-_K%C3%B6hler%E2%80%93s_Medizinal-Pflanzen-135.jpg) |
