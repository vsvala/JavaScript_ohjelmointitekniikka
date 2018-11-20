# JavaScript_ohjelmointitekniikka

## Sulkeuma ja sen käyttötavat

### näkyvyysalue

Näkyvyysalueen(scope) perusteella meillä on kahdenlaisia muuttujia: paikalliset(local) ja globaalit(global). Näkyvyysalue määrittelee, missä ja milloin muuttuja on olemasssa ja sen arvo on saatavilla. Totutusta Java kielen lohkoajattelusta  poiketen Javascript kielssä funktio muodostaa oman näkyvyysalueensa(scope). Tällöin funktion muodolliset parametrit, paikalliset muuttujat ja paikalliset funktiot näkyvät ja ovat käytettävissä vain ko.funktion sisällä. Funktion  näkyvyyaluetta kutsutaan toisinaan myös viittausympäristöksi tai nimiavaruudeksi. JavaScript kieli ei ole Javan tavoin "litteä", sillä funktiot voivat myös muodostaa useita sisäkkäisiä näkyyysalueita/miniavaruuksia. Perusideana JavaScriptin sisäkkäisillä näkyvyysalueilla on se, että "sisältä näkee ulos, mutta ulkoa ei näe sisään". Sulkeuma poikkeaa näkyvyysalueen normaalista määrittelystä, sillä siinä funktio suoritetaan oman näkvyysalueen sijasta sulkeuman määrittelyn funktion näkyvyysalueessa.
 
### sulkeuma

JavaScriptissä funktio voi saada parametrikseen toisen funktion. Tällöin sulkeumassa funktion parametrin mukana voidaan välittää myös sen muuttujia. Jos funktion sisällä luodaan sisempi funktio, sen näkyvyysalueeseen kuuluvat myös ulomman funktion muuttujat. Eli kun parametrin saanut funktio suorittaa parametrina saamansa funktion, suoritetaan se parametrina annetun funktion näkyvyysalueessa.

### sidotut muuttujat
"Funktion sidotuiksi muuttujiksi kutsutaan funktion muodollisia parametreja sekä funktion sisällä määriteltyjä paikallisia muuttujia. Toisin sanoen muuttujia, joilla on merkitys vain funktion sisällä ja jotka suoritusaikana ovat olemassa vain funktion suorituksen ajan.(Tämä vielä suoraan lainausta luentomatskusta..muokkaa)
### vapaat muuttujat
Funktion vapaiksi muuttujiksi kutsutaan sellaisia funktioon sisältymättömiä, mutta funktiossa viitattuja muuttujia, jotka funktiosta näkyvyyssääntöjen sallimana nähdään."(Tämä vielä suoraan lainausta luentomatskusta..mukkaa)

Nimensä "sulkeuma" (closure) saa siitä, kun funktio välitetään parametrina sen käyttämät vapaat muuttujat "suljetaan" mukaan funktion suoritusta varten.


### 1. Sulkeumaan suljetut vapaat muuttujat säilyvät sulkeuman suorituksen jälkeiseen aikaan.
### 2. Sulkeumaan suljetuttujen vapaiden muuttujien määritellyt funktio päättyy, mutta sulkeuma säilyy

function sulkeumaEsimerkki() {
  var a = "sul", b = "keuma";
  return function() { return a + b };
}
 
Kyseinen funktio palauttaa toisen funktion, joka näkee ulomman funkpalauttaa arvon "sulkeuma", vaikka ulkoisen funktion suoritus onkin päättynyt.


Normaalisti olemme tottuneet siihen että Paikallinen muuttuja ja sen arvo säilyvät vain tämän funktion elinajan. 

### kapselointi...?

"Edellä nähtiin, miten kutsuttu funktio voi sulkeuman vapaiden muuttujien avulla päästä muokkaamaan muuttujia, jotka eivät kuulu funktion omaan näkyvyysalueeseen. Noissa esimerkeissä nuo muuttujat ovat kuitenkin olleet olemassa – "kun funktio käynnistyy, sen paikalliset muuttujat syntyvät, kun funktion suoritus päättyy, sen paikalliset muuttujat häviävät" Tämä tekniikka osoittautuu aikanaan vahvaksi: sitä käyttäen voi toteuttaa mm. olioiden kenttien piilottamisen ja kätkettyjen kenttien "aksessorimetodit" Javan hengessä.(lainaus suoraan luentomatskusta... muokkaa)

### ehkä...?vielä esimerkki kapseloinista?...sen turvallisuus?


## Oliot ja niiden käyttäytyminen: Olioiden käytön hyviä (ja jos mahdollista turvallisia) ohjelmointityylejä ja -malleja.

### Olion luominen

Olion voidaan ajatella olevan jonkin asian yleinen käsite tai esimerkiksi kokoelma tietoja. OLio sisältää ominaisuuksia eli atribuutteja jotka tallennetaan muuttujiin sekä metodeja, joilla käsitellään olion sisältämää tietoa. Ominaisuuksia voidaan kutsua myös olioiden kentiksi. Olioiden voidaan ajatella olevan functioiden ilmentymiä jotka luodaan sanalla -New- . Olit voi käsittää myös assosiaatiotaulukoksi joka sisältää avain- arvopareja, joita käytetään Hashmappien tavoin. 

**Yksinkertainen aaltosuluilla luotu olioliteraali:**
("This" viitteet tarvitaan, jotta tiedetään viitattavan juuri kyseisen olion kenttiin.)

let noora = {nimi: "Noora", syntymavuosi: 2000, yearnow: 2018, ika: function(){return this.yearnow - this.syntymavuosi}};

write(rnoora.ika()); //18

tai määritellään ominaisuudet dynaamisesti jälkeenpäin:

let virva = {};
virva.nimi = "Virva";
virva.ika = 18;


**Object Olion avulla:**

let noora = new Object();
noora.nimi = "Noora";
noora.ika = 35;


Se millä tavalla oliota lähdetään luomaan, riippu aina käyttötarkoituksesta. Yllä esitetyt tavat ovat nopeita ja nidien avulla voi luoda yksittäisiä  ns kertakäyttöoliota joilla ei ole yhteisiä ominaisuuksia.
Jos kuitenkin tarvitaan useampia samantyyppisiä oliota on se kätevää tehdä konstruktorifunktion avulla. Olioiden luontiin käytettävät funktiot kirjoitetaan hyvien ohjelmointitapojen tapojen mukaan isoilla kirjaimilla alkaviksi


**Konstruktorifunktion:**

function Henkilo(nimi, ika) {
  this.nimi = nimi;
  this.ika = ika;
}
noora = new Henkilo("Noora", 35);

  
Konstruktorifunktion prototyyppiolioon voidaan liittää ominaisuuksia, jotka kaikki kyseisellä funktiolla konstruoidut oliot jakavat keskenään....Jos konstruktorin avulla olioita tehtaillessa olioilla on samoja funktioita, olisikin parempi ohjelmointityyli liittää yhteiset ominaisuudet prototyyppiolioon kaikkien perittäväksi, jotta vältytään koodin toisteisuudelta... tähän esimerkki..


Object.create-funktio puolestaan taas vain luo instanssin parametrinä annetusta olioprototyypistä. Luotavaa oliota ei siis voida alustaa samalla tapaa monipuolisesti kuin konstruktorifunktion avulla. Tämän tavan etu on kuitenkin se, että Object.create-funktiolle annettava prototyyppi voidaan valita vapaasti, eli se mahdollistaa olioiden luomisen myös olioista, joille ei ole erikseen määritelty konstruktorifunktiota. Se myös mahdollistaa erityyppisten olioiden luomisen dynaamisesti samassa funktiossa, sillä parametrinä voi antaa minkä tahansa tyyppisen olion. (Tämä suora kopio, pitää muokata:)

**tai vielä Object.create-funktion avulla:**

var Henkilo = {
  nimi : "",
  ika : "",
  }
  
  var noora = Object.create(Henkilo);
  noora.nimi = "Noora";
  noora.ika = 35;
 
**Olioden luonti JavaScriptin "luokka" eli class-määrittelyn avulla...**
 UUsin tapa... Class tästä esimerkki 
ECMAScript 6 esitteli class-rakenteen, joka ns. syntaktista sokeria jo edellä opitulle konstruktorifunktiotekniikalle.

 
### Olioden dynaamisuudesta:
Javascritissa olion kentät ovat julkisia eli niihin voidaan dynaamisesti lisätä ja niistä  voidaan poistaa kenttiä ja muuttaa arvoja olion luonnin jälkeen. Tämän piirteen kanssa tulee olla huolellinen, ettei tule uutta arvoa sijoittaessa vahingossa lisänneeksi ylimääräistä kenttää,jos esim. vahngossa kirjoittaa kentän nimen väärin. 
 
  tähän esimerkki...kentän muutto?
 kuinka  poistetaan?
 
olion kentistä:
"Kenttänimenä voi käyttää melkein mitä tahansa: tunnus, merkkijono (jopa tyhjä), luku, ..., kaikki sellaiset kielen arvot" jotka voi muuttaa merkkijonoksi:

**Olion kenttiin viittaamine ja läpikäynti**
"Vain tunnuksen muotoisiin kenttiin voi viitata pisteilmauksella, kaikkiin muihin on viitattava hakasulkein!"
olion kenttiin voidaan viitata joko pisteilmauksella tai taulukon ideksoinnin tapaan:
write(noora.ika)
nora["ika"]
 
 Koska olioden kentät assosiaatiotauoita, Olioiden  numeroituvia kenttiä voidaan käydä läpi taulukon tavoin for kentta in olio raneteella, mukana tulostuu myös perityt kentät
 tähän esimekki
 lisää kenttirn läpikäynti mahdollisuuksia...
 
 
Lähteet:  
  
https://fi.wikipedia.org/wiki/Sulkeuma_(ohjelmointi)

https://www.cs.helsinki.fi/u/wikla/OTjs/materiaalia/funktiot/
