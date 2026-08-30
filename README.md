# bierfunding.nl

Statische website voor Bierfunding, een initiatief van CO&CO Craft Beers.
Vijf pagina's, platte HTML en CSS. **Geen build-stap, geen framework, geen
JavaScript, geen tracking.** Wat in deze map staat, is wat de server serveert.

```
index.html            Home
hoe-het-werkt.html    De route van reserveren tot je pakket ophalen
kandidaten.html       De vier proefbrouwsels
voorwaarden.html      De voorwaarden
over-ons.html         Coen & Coers en de brouwerij
404.html              Foutpagina
css/site.css          De enige stylesheet
fonts/                Archivo + Archivo Narrow, zelf gehost (52 KB, SIL OFL)
img/                  Foto's
.htaccess             Cache- en compressieregels (alleen op Apache)
robots.txt            
sitemap.xml           
favicon.svg           
```

---

## 1. Wat er nog ingevuld moet worden

**Alles tussen `[rechte haken]` is een gat.** Op de pagina zijn die geel
gemarkeerd, dus je ziet in één oogopslag wat er nog ontbreekt. Zoek in de
bestanden op `[` en je hebt ze allemaal.

| Waar | Wat |
|---|---|
| Overal | Datum van de eerste ronde, prijs per plek, aantal plekken, e-mailadres |
| Home + Kandidaten | De vier biernamen, alcoholpercentages, en één zin per bier |
| Home | De drie pakketten: aantal flesjes en prijs, en de zin over het minimum |
| Kandidaten | Per bier: waar het recept vandaan komt, wat je proeft, waarom het kandidaat is. Er staat per veld een voorbeeldzin die je kunt vervangen |
| Hoe het werkt | Duur van de avond, adres, tijden, wat er inbegrepen zit, levertermijn |
| Over ons | Sinds welk jaar jullie brouwen, hoe het begon, en het blok met jullie eigen woorden |
| Voorwaarden | Bedrijfsgegevens, bedragen, termijnen — en drie echte besluiten (zie hieronder) |

### Besluiten die niemand voor je kan opzoeken

Deze staan als notitieblok op de voorwaardenpagina en moeten door jou
beslist worden:

1. **Afmeldbeleid** (art. 3.5) — wat gebeurt er als iemand niet kan?
2. **Betaalconstructie** (art. 5.3) — 50/50 of alles vooruit? Juristenvraag.
3. **Retourkosten** (art. 8.2) — voor de klant of voor de brouwerij?

En verder, buiten de site om: **bel de gemeente Zwolle** over de
alcoholvergunning voordat je de eerste plek verkoopt. Dat punt staat als
blokkerend gemarkeerd in de voorwaarden.

---

## 2. Checklist vóór livegang

- [ ] Alle `[rechte haken]` ingevuld
- [ ] De **conceptbalk** weggehaald: het blok `<div class="draft">…</div>`
      bovenaan elk van de vijf pagina's. Zoek op `CONCEPTBALK`
- [ ] De **notitieblokken** op de voorwaardenpagina weggehaald: elk
      `<div class="note">…</div>`. Dat zijn aantekeningen voor jou, geen
      paginatekst
- [ ] `<meta name="robots" content="noindex">` uit `voorwaarden.html` gehaald
      (staat er zolang de pagina een concept is)
- [ ] De voorwaardentekst door een jurist laten lezen
- [ ] De **voorbeeldfoto's** van de vier bierglazen vervangen door foto's van
      de échte proefbrouwsels (zie hieronder)
- [ ] De knop **"Bestelling ontbinden"** op de voorwaardenpagina naar het
      juiste adres laten wijzen — zie de opmerking in punt 5

---

## 3. Foto's toevoegen

**Al ingebouwd:** de proefglazen bovenaan de homepage (`proefglazen-*`), de
foto van Coen & Coers (`coen-coers-*`) en de vier bierglazen (`kandidaat-1-*`
t/m `kandidaat-4-*`).

**De vier bierglazen zijn voorbeeldfoto's.** Zodra je foto's van de échte
proefbrouwsels hebt, maak je daar dezelfde bestandsnamen van en zijn ze
ingewisseld — de HTML hoeft niet aangeraakt te worden. De koppeling is nu:
kandidaat 1 = goudblond, 2 = bijna zwart, 3 = amber, 4 = troebel lichtgeel.
**Let op:** de alt-teksten beschrijven die kleuren, dus pas ze aan als de
nieuwe foto's er anders uitzien.

**Nog echte plaatshouder:** de sfeerfoto van de proeftafel op *Hoe het werkt*
(`avond-*`) en de foto van de installatie op *Over ons* (`installatie-*`).

Elke plaatshouder ziet er in de HTML zo uit:

```html
<figure class="shot shot--glass">
  <p><b>Foto</b> een glas van dit bier</p>
  <!-- FOTO KLAAR? Verwijder de <p> hierboven en haal onderstaande <img> uit
       commentaar. …
  <img src="img/kandidaat-1-480.jpg" srcset="…" …>
  -->
</figure>
```

Dus: **bestanden in `img/` zetten, de `<p>` weghalen, de `<img>` uit
commentaar halen.** De bestandsnamen die de HTML verwacht staan in de
`srcset` en in `img/LEESMIJ.txt`.

### Drie breedtes maken

Zet nooit één grote foto neer. Een telefoon downloadt dan de versie voor een
groot scherm, en dat is precies wat coco-craftbeers.nl traag maakt. Maak per
foto drie breedtes met `sips` (zit standaard op macOS):

```bash
cd img
# vier keer, voor kandidaat-1 t/m kandidaat-4
sips -s format jpeg -s formatOptions 65 --resampleWidth 320 bron.jpg --out kandidaat-1-320.jpg
sips -s format jpeg -s formatOptions 62 --resampleWidth 480 bron.jpg --out kandidaat-1-480.jpg
sips -s format jpeg -s formatOptions 58 --resampleWidth 640 bron.jpg --out kandidaat-1-640.jpg
```

Richtlijn: **de grootste variant onder 200 KB.** Controleer met `ls -lh`.
Wordt hij groter, verlaag dan `formatOptions` met stappen van 5.

`--resampleWidth` en niet `-Z`: `-Z` schaalt op de langste zijde, dus bij een
staande foto krijg je een verkeerde breedte en klopt de `srcset` niet meer.

### webp of avif erbij (optioneel)

Kan, maar **alleen als je alle drie de formaten compleet hebt**. Een
`<picture>` met een `<source type="image/avif">` die niet bestaat levert een
lege plek op — de browser valt dan niet terug op de JPEG. Daarom staat er nu
bewust een gewone `<img>` met alleen JPEG's. Dat werkt overal en is
ruimschoots snel genoeg.

### De originele bestanden

`header.jpg`, `co_en_co.jpeg` en `bier-1.jpg` t/m `bier-4.jpg` zijn jouw
originelen: **samen 20 MB**. De site gebruikt ze niet — die laadt de
verkleinde versies. Alles wat de site écht nodig heeft is samen 1,7 MB.

Je kunt de originelen dus uit de repo halen (bewaar ze wel ergens anders);
20 MB in de Git-geschiedenis krijg je er later niet makkelijk meer uit. Wil je
ze houden, dan kan dat ook — ze worden nooit door een bezoeker gedownload,
alleen door Plesk meegekopieerd.

---

## 4. Naar Plesk

De site staat in de **root van de repo**, zodat Plesk hem rechtstreeks als
docroot kan gebruiken. Er draait geen Node en er is geen buildstap: wat
binnenkomt, wordt geserveerd.

1. Plesk → **Websites & Domeinen** → `bierfunding.nl` → **Git**
2. **Repository toevoegen** → *Remote Git hosting*
3. Repository-URL: `https://github.com/fcoers/bierfunding.git`, branch `main`
4. **Deployment-pad: `/httpdocs`** — dus de repo-root landt rechtstreeks in de
   docroot. Géén submap.
5. Deployment-modus: *automatisch* als je de webhook aanzet, anders handmatig
   met de knop **Nu deployen**
6. Is de repo privé? Kopieer dan de publieke SSH-sleutel die Plesk toont naar
   GitHub → repo → *Settings* → *Deploy keys*

Na de eerste deploy hoort `index.html` direct in `httpdocs` te staan, niet in
`httpdocs/bierfunding/`. Staat het een niveau te diep, dan klopt het
deployment-pad niet.

`.htaccess` regelt caching en compressie op Apache. Draait er nginx, dan wordt
het bestand genegeerd en zet je de cache-instellingen in Plesk zelf. Het kan
geen kwaad laten staan.

---

## 5. Twee dingen om te weten

**Er staat geen leeftijdspoort op deze site, en dat is een bewuste keuze.**
Deze site verkoopt niets: bestellen gebeurt in de CO&CO-webshop, en dáár zit
de harde controle (het vinkje vóór het afronden, en nog een keer bij de
levering). Een poort hier zou een lege witte pagina als eerste indruk geven —
precies het probleem dat op coco-craftbeers.nl is gemeten. In plaats daarvan
staat "vanaf 18 jaar" bij elke knop naar de webshop en een 18+-markering in de
voettekst van elke pagina.

**De knop "Bestelling ontbinden"** op de voorwaardenpagina wijst nu naar een
plaatshouder. De wettelijke herroepingsfunctie hoort te staan wáár de
bestelling wordt geplaatst — dus in de CO&CO-webshop. Laat de knop hier
verwijzen naar die functie in de webshop.

---

## 6. Techniek

- **Geen JavaScript.** Geen enkele regel, op geen enkele pagina.
- **Geen externe verzoeken.** De lettertypen staan in `fonts/`, dus er gaat
  niets naar Google. Daardoor is er ook geen cookiemelding nodig.
- **Lettertypen:** Archivo en Archivo Narrow, variabel, samen 52 KB. Licentie
  SIL Open Font License 1.1 — zie `fonts/OFL.txt`.
- **Gewicht:** de homepage is op een telefoon ongeveer **137 KB** bij eerste
  weergave en 370 KB als je helemaal doorscrolt. De foto's onder de vouw
  worden pas geladen als je erbij komt.
- **Toegankelijkheid:** getoetst op contrast (WCAG AA), één `<h1>` per pagina,
  kloppende koppenstructuur, klikzones van minimaal 44 px, alt-teksten,
  zichtbare focus, en `prefers-reduced-motion`.
- **Wijzig je `css/site.css`?** Verhoog dan `?v=1` in de `<link>`-regel van de
  vijf pagina's, anders houden bezoekers de oude versie uit hun cache.
