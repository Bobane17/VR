# TenisAnaliza — Forehand vs Backhand Detekcija

Spletna aplikacija za zajem in analizo teniškega udarca (forehand/backhand) s pomočjo žiroskopa in pospeškometra iPhona prek aplikacije **phyphox**.

## Gostovanje na GitHub Pages

1. Ustvari nov repozitorij na GitHubu: `tenis-analiza` (ali dodaj v obstoječi)
2. Skopiraj `index.html` in `manifest.json` v korenski imenik repozitorija
3. Pojdi na: **Settings → Pages → Source: main branch, / (root)**
4. Aplikacija bo dostopna na: `https://bobane17.github.io/tenis-analiza/`

## Potek eksperimenta

### 1. Nastavitev phyphox
- Odpri phyphox → **Gyroscope** → nastavi frekvenco na **100 Hz**
- Opcijsko: vzporedno odpri **Acceleration (without g)** v drugem eksperimentu

### 2. Izvedba
- Odpri TenisAnaliza aplikacijo v brskalniku
- Vnesi metapodatke (ime, oseba, hitrost)
- Drži iPhone v dominantni roki (navpično, zaslon navznoter)
- Začni snemanje v phyphox
- Za vsak udarec pritisni **FH** ali **BH** gumb v aplikaciji (beleži časovni žig)
- Izvedi **30 forehand + 30 backhand** udarcev

### 3. Izvoz podatkov
- phyphox: meni → **Export Data → CSV (Comma, decimal point)**
- TenisAnaliza: gumb **Izvozi beležnico (JSON)** za časovne žige

### 4. Analiza
- Naloži CSV v zavihku **Analiza**
- Aplikacija samodejno:
  - Izračuna statistike (povprečje, std, min, max)
  - Najde vrhove in doline (FH = pozitiven vrh Z osi, BH = negativen vrh)
  - Izriše signal in porazdelitev
  - Izračuna confusion matrix + accuracy/precision/recall
  - Potrdi ali zavrne obe hipotezi

## Struktura CSV iz phyphox

phyphox izvozi CSV z naslednjimi stolpci (Gyroscope):
```
time (s), gyrX (rad/s), gyrY (rad/s), gyrZ (rad/s)
```

Aplikacija samodejno prepozna stolpce ne glede na natančna imena.

## Hipotezi

**H1:** Z žiroskopom (os Z) pri 100 Hz vzorčenja lahko ločimo forehand od backhanda z natančnostjo ≥ 85%.

**H2:** Hitri udarci imajo statistično značilno višjo amplitudo žiroskopa (Z os) kot počasni (p < 0.05).

## Tehnične opombe

- **Klasifikacijski prag:** ± 1.2 × standardni odklon signala Z osi
- **FH detekcija:** pozitivni vrh presega prag
- **BH detekcija:** negativni vrh presega prag (v absolutni vrednosti)
- Za natančnejšo analizo uvozi JSON beležnico in CSV v Python/Excel za ročno označevanje

## Datoteke

| Datoteka | Namen |
|----------|--------|
| `index.html` | Celotna aplikacija (PWA) |
| `manifest.json` | PWA manifest za namestitev na domači zaslon |
| `README.md` | Ta datoteka |
