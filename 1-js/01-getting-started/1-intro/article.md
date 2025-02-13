# Uvod u JavaScript

Pogledajmo šta je tako posebno u JavaScriptu, šta možemo postići sa njim i koje druge tehnologije se sa njim dobro 'igraju'.

## Šta je JavaScript ?

*JavaScript* je prvobitno kreiran kako bi *"oživio web stranice"*.

Programi na ovom jeziku se nazivaju *skripte*. Mogu se napisati pravo u HTML-u veb stranice i pokrenuti automatski kada se stranica učita.

Skripte se pružaju i izvode u obliku običnog teksta. Za pokretanje im nisu potrebne posebne pripreme ili kompilacije.

U ovom aspektu, JavaScript se veoma razlikuje od drugog jezika koji se zove [Java](https://en.wikipedia.org/wiki/Java_(programming_language)).

```smart header="Zašto <u>Java</u>Script?"
Kada je kreiran JavaScript, u početku je imao drugo ime: "LiveScript". Ali Java je u to vreme bila veoma popularna, pa je odlučeno da će pozicioniranje novog jezika Java-ovog „mlađeg brata“

Ali kako se razvijao, JavaScript je postao potpuno nezavisan jezik sa sopstvenom specifikacijom [ECMAScript](http://en.wikipedia.org/wiki/ECMAScript), a sada uopšte nema veze sa Javom.
```

Danas JavaScript može da se izvršava ne samo u pregledaču, već i na serveru, ili zapravo na bilo kom uređaju koji ima poseban program koji se zove [the JavaScript engine](https://en.wikipedia.org/wiki/JavaScript_engine).

Preglednik ima ugrađeni motor koji se ponekad naziva i „JavaScript virtuelna mašina“.

Različite mašine imaju različita "kodna imena". Na primer:

- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) -- u Chrome-u i Opera.
- [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey) -- u Firefox-u.
- ... Postoje i druga kodna imena poput "Trident" i "Chakra" za različite verzije IE-a, "ChakraCore" za Microsoft Edge, "Nitro" i "SkuirrelFish" za Safari, itd.

Gore navedene pojmove dobro je zapamtiti jer se koriste u člancima za programere na Internetu. Koristićemo i njih. Na primer, ako „odliku X podržava V8“, ona verovatno funkcioniše u Chrome-u i Operi.

```smart header="Kako rade mašine ?"

Motori su komplikovani. Ali osnove su jednostavne.

1. Motor (ugrađen ako je pretraživač) čita („analizira“) skriptu.
2. Zatim pretvara ("kompajlira") skriptu u mašinski jezik.
3. A onda mašinski kod radi prilično brzo.

Motor primenjuje optimizacije na svakom koraku procesa. Čak posmatra sastavljenu skriptu dok radi, analizira podatke koji prolaze kroz nju i primenjuje optimizacije na mašinskom kodu na osnovu tog znanja. Kada je gotov, skripte se pokreću prilično brzo.
```

## Šta JavaScript u internet pretraživaču može da radi?

Savremeni JavaScript je "siguran" programski jezik. Ne pruža pristup memoriji ili CPU-u nižeg nivoa, jer je prvobitno kreiran za pregledače koji to ne zahtevaju.

Mogućnosti JavaScript-a u velikoj meri zavise od okruženja u kome se nalazi. Na primjer [Node.js](https://wikipedia.org/wiki/Node.js) podržava funkcije koje omogućuju JavaScriptu da čita / piše proizvoljne datoteke, izvršava mrežne zahteve itd.

JavaScript u pretraživaču može učiniti sve što se odnosi na manipulaciju web stranicama, interakciju sa korisnikom i web serverom.

Na primer, JavaScript u pregledaču može:

- Dodajte novi HTML na stranicu, promenite postojeći sadržaj, izmenite stilove.
- Reaguje na akcije korisnika, pokretanje određene radnje klikom miša, pokretanje pokazivača, klik na tasteru.
- Slanje zahteva preko mreže udaljenim serverima, preuzimanje i učitavanje datoteka (takozvani [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)) i [COMET](https://en.wikipedia.org/wiki/Comet_(programming)) tehnologije).
- Dobijajte i postavljajte kolačiće, postavljajte pitanja posetiocu, pokažite poruke.
- Zapamtite podatke na strani klijenta ("lokalna memorija").

## Šta NE MOŽETE u JavaScript pretraživaču?

Mogućnosti JavaScripta u pretraživaču su ograničene zbog bezbednosti korisnika. Cilj je sprečiti zlo veb stranici da pristupi privatnim podacima ili našteti korisnikovim podacima.

Primeri takvih ograničenja uključuju:

- JavaScript na veb stranici možda ne može čitati / pisati proizvoljne datoteke na hard disku, kopirati ih ili izvršavati programe. Nema direktan pristup funkcijama sistema OS.

    Savremeni pregledači omogućavaju mu da radi sa datotekama, ali je pristup ograničen i pruža se samo ako korisnik izvrši određene radnje, poput „puštanja“ datoteke u prozor pregledača ili izbora pomoću „<input>“ taga.

    Postoje načini za interakciju s kamerom / mikrofonom i drugim uređajima, ali za njih je potrebno izričito odobrenje korisnika. Dakle, stranica sa omogućenim JavaScriptom možda ne dozvoljava da večno omogućuju veb kameru, posmatrajte okolinu i šaljite informacije na [NSA](https://en.wikipedia.org/wiki/National_Security_Agency).
    
- Različiti tabovi / prozori uglavnom ne znaju jedni o drugima. Ponekad to urade, na primer kada jedan prozor koristi JavaScript da otvori drugi. Ali čak i u ovom slučaju, JavaScript s jedne stranice možda ne može pristupiti drugoj ako dolaze sa različitih veb lokacija (sa drugog domena, protokola ili porta).

    To se naziva „Politika istog porekla“. Da biste to rešili, * obe stranice * moraju se složiti za razmenu podataka i sadržavati poseban JavaScript kod koji njime rukuje. Doći ćemo i do toga tutorijala.

    Ovo ograničenje je, opet, zbog bezbednosti korisnika. Stranica sa `http: // anisite.com` koju je korisnik otvorio ne smije biti u mogućnosti da pristupi drugoj kartici pregledača sa URL-om `http://gmail.com` i krade informacije odatle.
    
- JavaScript može lako da komunicira preko mreže sa serverom odakle je došla trenutna stranica. Ali njegova sposobnost da prima podatke sa drugih lokacija / domena je osakaćena. Iako je moguće, zahteva izričit dogovor (izražen u HTTP zaglavima) sa udaljene strane. Još jednom, to je sigurnosno ograničenje.

![](limitations.svg)

Takva ograničenja ne postoje ako se JavaScript koristi izvan pregledača, na primer na serveru. Savremeni pregledači takođe dozvoljavaju dodatak / proširenja koji mogu tražiti proširenja dozvola.

## Po čemu je JavaScript jedinstven?

Postoje najmanje *tri* sjajne stvari o JavaScript-i :

```compare
+ Potpuna integracija sa HTML-om/CSS-om.
+ Jednostavne stvari se rade jednostavno.
+ Podrška svih glavnih pregledača i omogućena podrazumijevano.
```
JavaScript je jedina tehnologija pretraživača koja kombinuje ove tri stvari.

To čini JavaScript jedinstvenim. Zato je to najrasprostranjeniji alat za kreiranje interfejsa pretraživača.

Uz to, JavaScript takođe omogućava kreiranje servera, mobilnih aplikacija itd.

## Jezici "preko" JavaScript-e

Sintaksa JavaScript ne odgovara svačijim potrebama. Različiti ljudi žele različite karakteristike.

To je očigledno, jer su projekti i zahtevi za svakoga različiti.

Tako se nedavno pojavila mnoštvo novih jezika koji su * prevedeni * (pretvoreni) u JavaScript pre nego što se pokrenu u pretraživaču.

Savremeni alati čine transpilaciju veoma brzom i preglednom, ustvari omogućavajući programerima da kodiraju na drugom jeziku i automatski ga pretvaraju "pod haubom".

Primeri takvih jezika:

- [CoffeeScript](http://coffeescript.org/) je "sintaktički šećer" za JavaScript. Uvodi kraću sintaksu, omogućavajući nam pisanje jasnijeg i preciznijeg koda. Obično se Ruby programerima sviđa.
- [TypeScript](http://www.typescriptlang.org/) koncentrisana je na dodavanje „strogog unosa podataka“ radi pojednostavljenja razvoja i podrške složenih sistema. Razvio ga je Microsoft.
- [Flow](http://flow.org/) takođe dodaje podatke za unos podataka, ali na drugačiji način. Razvijen od strane Facebook-a.
- [Dart](https://www.dartlang.org/) je samostalan jezik koji ima svoj motor koji radi u okruženjima koja nisu u pretraživaču (poput mobilnih aplikacija), ali takođe se može prevesti u JavaScript. Razvio Google.

Postoji više. Naravno, čak i ako koristimo jedan od prevedenih jezika, trebalo bi da znamo i JavaScript da bismo zaista razumeli šta radimo.

## Rezime

- JavaScript je u početku kreiran kao jezik samo za pregledač, ali se sada koristi i u mnogim drugim okruženjima.
- Danas JavaScript ima jedinstvenu poziciju kao najšire prihvaćeni jezik pregledača sa potpunom integracijom sa HTML-om / CSS-om.
- Postoji mnogo jezika koji se "prevode" u JavaScript i pružaju određene funkcije. Preporučuje se da ih sagledate, bar na kratko, nakon savladavanja JavaScripta.
