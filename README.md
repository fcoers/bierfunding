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
img/                  Foto's en het CO&CO-beeldmerk
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
| Home | De drie pakketten: aantal flesjes en prijs, en hoeveel deelnemersvoordeel je op een pakket geeft |
| Home + Hoe het werkt | **Het minimumaantal bestellingen** en de uiterste datum. Diezelfde twee getallen staan in artikel 5.2 en 11 van de voorwaarden — vul ze overal gelijk in |
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

**Alle fotoplekken zijn gevuld.** Wat er staat:

| Waar | Bestanden | Bron |
|---|---|---|
| Homepage, breedbeeld bovenaan | `proefglazen-*` | `proefglazen v2.jpg` |
| Homepage + Over ons, Coen & Coers | `coen-coers-*` | `co_en_co.jpeg` |
| Homepage + Kandidaten, vier glazen | `kandidaat-1-*` t/m `-4-*` | `bier-1.jpg` t/m `bier-4.jpg` |
| Hoe het werkt, breedbeeld | `proefavond-*` | `hoe-het-werkt.jpg` |
| Over ons, de brouwerij | `brouwerij-*` | `brouwerij-wythem.jpeg` |
| Menubalk, CO&CO-beeldmerk | `coco-logo-wit.png` | `Logo ondertitel wit.png` |

**De vier bierglazen zijn voorbeeldfoto's.** Zodra je foto's van de échte
proefbrouwsels hebt, maak je daar dezelfde bestandsnamen van en zijn ze
ingewisseld — de HTML hoeft niet aangeraakt te worden. De koppeling is nu:
kandidaat 1 = goudblond, 2 = bijna zwart, 3 = amber, 4 = troebel lichtgeel.
**Let op:** de alt-teksten beschrijven die kleuren, dus pas ze aan als de
nieuwe foto's er anders uitzien.

### Twee foto's zijn niet in Wijthmen gemaakt

De foto van Coen & Coers is bij **Brouwerij Allema** genomen en de sfeerfoto
op *Hoe het werkt* is een **proeflokaal, niet de eigen brouwerij**. Dat staat
bij beide in het bijschrift en het staat bewust níét in de alt-tekst. Schrijf
er dus ook geen sitetekst omheen die suggereert dat dit Wijthmen is. De enige
foto van de eigen brouwerij is `brouwerij-*` op *Over ons*.

De sfeerfoto op *Hoe het werkt* is bovendien **bijgesneden om een krijtbord
weg te laten**: in het origineel ligt vooraan op tafel een bord met "Zwolse
Speciaalbier Proeverij" en zes bierstijlen. Dat is een ander evenement, en
Bierfunding heeft vier kandidaten. Vervang je die foto, kijk dan opnieuw of er
geen tekst in beeld staat die iets anders belooft.

### De foto bovenaan de homepage wordt bijgesneden, en de titel ligt erin

Twee dingen om te weten als je deze foto vervangt.

**1. Hij wordt aan alle kanten bijgesneden.** De hoogte is begrensd op
**maximaal 300 px** (en lager op een klein venster), anders duwt hij op een
laptop de uitleg en de knop onder de vouw — dat was de fout van de eerste
versie. Verticaal zie je dus alleen de middenband, precies het midden
(`object-position: 50% 50%` in `css/site.css`). Op een telefoon wordt er
daarnaast links en rechts een strook af gesneden: ongeveer 5% aan elke kant
op 390 px, 10% op 320 px. Kies dus een foto waarvan **het onderwerp in het
midden zit**, verticaal én horizontaal. Boven 1000 px loopt de foto niet meer
door tot de schermrand maar staat hij in dezelfde kolom als de tekst; anders
wordt de uitsnede op een breed scherm nóg smaller.

**2. De titel ligt over de onderste strook van de foto**, met een donker
verloop eronder dat de leesbaarheid garandeert. Daar staan twee regels: de
`<h1>` **Bierfunding** groot, en daaronder kleiner de ondertitel *Welk bier
brouwen we hierna?* Zet dus **niets belangrijks in de onderste 60%** van de
nieuwe foto: dat deel gaat op een breed scherm schuil onder de titel en het
verloop (35% op een telefoon, 60% op een laptop). Een rustig, egaal vlak daar
(een tafelblad, een muur) is precies goed. Het verloop is zo sterk dat de
tekst er ook op een spierwitte foto nog 6,2:1 haalt, dus je hoeft bij het
kiezen niet op contrast te letten.

**3. De glazen passen er maar net in, en daarom staat de uitsnede op 50%.**
Gemeten in de bronfoto van 2754 x 1536: de glazen lopen van y 372 (de
schuimkraag van het middelste glas) tot y 1168 (de glasvoeten), samen 796
beeldpunten. Op een laptop van 1280 x 633 is het zichtbare venster 802
beeldpunten hoog — zes over. De uitsnede kan daar dus maar op één plek staan.
Bij 52% wordt de schuimkraag afgesneden, bij 48% de glasvoeten; beide
gecontroleerd in de browser. Voor de vorige foto met lege glazen stond dit op
54%, want lege glazen zijn lager. **Vervang je de foto opnieuw, meet dit dan
opnieuw** — het is de eerste instelling die stukgaat.

**4. Op een laag venster past het glas er niet meer in, en dat is met opzet.**
Is het browservenster lager dan ongeveer 650 px, dan krimpt het beeldblok mee
(de 46vh-regel) — op 1280 × 520 is het nog 239 px. Daar valt de schuimkraag
bovenaan weg en zie je onderaan alleen de stelen, niet de glasvoeten;
nagekeken op vergroting. Dat is een ruil, geen fout: een hoger beeldblok duwt
op zo'n venster de knop weer onder de vouw, precies het probleem dat in ronde
2 is opgelost. Aan de uitsnede valt het niet te repareren — het midden van de
glazen valt samen met het midden van de foto, dus 50% geeft aan beide kanten
evenveel weg. Wil je het tóch anders, dan zit de knop in de `height`-regel van
`.hero` en niet in `object-position`. Vanaf 1280 × 633 is het glas compleet,
en op een telefoon wordt er alleen links en rechts een strook af gesneden.

### De breedbeeldfoto op *Hoe het werkt*

Die loopt van rand tot rand, maar **boven 1000 px blijft hij in de kolom van
de tekst** — dezelfde grens als de headerfoto, en om dezelfde reden: zonder
die grens zou hij op een scherm van 1920 px 747 px hoog worden en driekwart
van het venster vullen. Met de grens is hij 389 px. Dat regelt de klasse
`shot--band` in `css/site.css`.

### Het CO&CO-beeldmerk in de menubalk

Het logo staat vóór het woord BIERFUNDING en is **26 px hoog**. Dat is geen
smaakkwestie: de regel waarin dat woord staat is 30 px hoog, dus alles tot
30 px past erin **zonder dat de balk hoger wordt**. Nagemeten op elf
schermbreedtes: de balk is nog steeds 62 px op een breed scherm en 158 px op
een telefoon, precies zoals ervoor. Maak je het logo groter dan 30 px, dan
groeit de balk op élke pagina mee.

Het is een uitsnede van `Logo ondertitel wit.png`: **alleen het beeldmerk
C&O, zonder de regel CRAFT BEERS**. Op 26 px is die ondertitel een grijze
veeg van een paar beeldpunten hoog — dan is het geen logo meer maar een
vlekje. De uitsnede loopt door de lege strook tussen beide, dus er is niets
vervormd. Wil je het volledige logo tóch in de balk, dan kan dat, maar reken
op een onleesbare ondertitel of een hogere balk.

De `alt` van het logo is **leeg**, met opzet: logo en woord vormen samen één
link naar de homepage, en die heeft één naam nodig. Met een alt-tekst op het
logo zou een schermlezer op elke pagina "CO&CO Craft Beers Bierfunding, link"
voorlezen. Dát CO&CO erachter zit, staat in gewone tekst in de voettekst van
elke pagina.

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

## 3b. Twee woorden die je niet door elkaar mag halen

Sinds versie 2 van de voorwaarden maakt de tekst een hard onderscheid, en de
sitecopy volgt dat overal:

- **Aanmelden** gaat over de **proefavond**. Je meldt je aan voor een plek op
  een vaste datum en betaalt vooraf.
- **Bestellen** gaat over het **bierpakket**, ná de stemming. Je betaalt pas
  nadat wij bevestigen dat er genoeg besteld is: de helft direct, de helft bij
  het ophalen.

"Reserveren", "boeken" en "afnemen" komen er niet meer in voor — niet in de
voorwaarden en niet in de sitecopy. Schrijf je nieuwe tekst, houd dat dan aan;
een onderscheid dat de voorwaarden wél maken en de homepage niet, is niets
waard.

## 3c. Wees niet stelliger dan de werkelijkheid

Waar de proefavond precies is, hangt af van de groepsgrootte: binnen bij de
brouwerij of buiten op de plek ernaast. De sitecopy zegt daarom **"bij onze
eigen brouwerij"** en noemt de plaats één keer per pagina hooguit; de precieze
plek krijgt een deelnemer bij zijn aanmelding. Hetzelfde geldt voor het aantal
plekken, de duur van de avond en de tijden: dat staan allemaal plaatshouders.

Het **bedrijfsadres** in de voettekst, op *Over ons* en in artikel 1 van de
voorwaarden blijft gewoon staan — dat is een wettelijk verplichte vermelding en
geen belofte over de avond. Ook de alt-tekst bij de brouwerijfoto mag Wijthmen
noemen: die foto ís daar gemaakt.

### De originele bestanden

`proefglazen v2.jpg` (plus de kopie `proefglazen-v2.jpg` zonder spatie in de
naam, waar het bouwcommando mee werkt), `header.jpg`, `co_en_co.jpeg`,
`bier-1.jpg` t/m `bier-4.jpg`, `brouwerij-wythem.jpeg`, `hoe-het-werkt.jpg` en
`Logo ondertitel wit.png` zijn jouw originelen: **samen ruim 34 MB**.
`header.jpg` is de vorige headerfoto met lége glazen; die is vervangen maar
blijft staan. De site gebruikt ze niet — die laadt de
verkleinde versies. Ze staan daarom in `.gitignore` en gaan niet mee naar de
repo; 30 MB in de Git-geschiedenis krijg je er later niet makkelijk meer uit.

Ze blijven wel gewoon in `img/` op je eigen schijf staan. Bewaar ze ergens
buiten de repo als je die map ooit opruimt — zonder de originelen kun je geen
nieuwe uitsnede of een groter formaat meer maken.

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
- **Gewicht:** de homepage is op een telefoon ongeveer **140 KB** bij eerste
  weergave; de foto's onder de vouw worden pas geladen als je erbij komt. De
  twee foto's die er in ronde 5 bij kwamen staan allebei onder de vouw en
  kosten op een telefoon 52 KB (*Hoe het werkt*) en 71 KB (*Over ons*). Het
  CO&CO-beeldmerk in de balk is 3,3 KB. Alles bij elkaar wat naar de repo
  gaat: **2,3 MB**; de originelen die de site niet gebruikt zijn 30 MB en
  staan in `.gitignore`.
- **Vaste regel: de kop staat vóór het beeld, in de HTML zelf.** Op een smal
  scherm stapelt elke tweekolomsrij, en dan verschijnt in de code-volgorde wat
  in de HTML bovenaan staat. Stond de foto eerst, dan kom je binnen op een
  foto en weet je niet waar je bent — dat gebeurde op *Over ons*. Zet de
  `<h1>`/`<h2>` dus als eerste in de rij en laat de rasterindeling bepalen
  waar de foto op een breed scherm terechtkomt. Nooit met `order` in CSS:
  dan lopen de voorgelezen volgorde en de zichtbare volgorde uit elkaar.
  Op de homepage ligt de titel sinds ronde 3 *in* de foto: hij staat als
  eerste in de HTML, maar het beeldblok tekent hem visueel onderin. Zo lopen
  de voorgelezen volgorde en het beeld weer gelijk op, en is er geen
  uitzondering meer op deze regel.
- **De ondertitel op de homepage is een `<p>`, geen `<h2>`.** *Welk bier
  brouwen we hierna?* hoort bij de `<h1>` Bierfunding en kondigt geen nieuwe
  sectie aan; een `<h2>` zou een sectie beloven die er niet is en de
  koppenstructuur van de pagina scheeftrekken. Sinds ronde 5 is **Bierfunding
  de grote regel** (34 px op een telefoon, 60 px op een breed scherm) en staat
  de vraag er kleiner onder (17-24 px). Wil je die verhouding ooit wijzigen:
  het verloop achter de tekst hangt aan de titelmaat (`--hero-title`), dus dat
  schaalt mee — maar meet het contrast daarna opnieuw, want de bovenste regel
  ligt in het zwakste deel van het verloop.
- **Toegankelijkheid:** getoetst op contrast (WCAG AA), één `<h1>` per pagina,
  kloppende koppenstructuur, klikzones van minimaal 44 px, alt-teksten,
  zichtbare focus, en `prefers-reduced-motion`.
- **Wijzig je `css/site.css`?** Verhoog dan het versienummer in de
  `<link>`-regel van alle zes de pagina's — nu `?v=6` — anders houden
  bezoekers die de site al bezocht hebben de oude opmaak uit hun cache.
