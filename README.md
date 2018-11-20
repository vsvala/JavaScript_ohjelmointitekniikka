# JavaScript_ohjelmointitekniikka

## Sulkeuma ja sen käyttötavat

### näkyvyysalue

Näkyvyysalueen(scope) perusteella meillä on kahdenlaisia muuttujia: paikalliset(local) ja globaalit(global). Näkyvyysalue määrittelee, missä ja milloin muuttuja on olemasssa ja sen arvo on saatavilla. Totutusta Java kielen lohkoajattelusta  poiketen Javascript kielssä funktio muodostaa oman näkyvyysalueensa(scope). Tällöin funktion muodolliset parametrit, paikalliset muuttujat ja paikalliset funktiot näkyvät ja ovat käytettävissä vain ko.funktion sisällä. Funktion  näkyvyyaluetta kutsutaan toisinaan myös viittausympäristöksi tai nimiavaruudeksi. JavaScript kieli ei ole Javan tavoin "litteä", sillä funktiot voivat myös muodostaa useita sisäkkäisiä näkyyysalueita/miniavaruuksia. Perusideana JavaScriptin sisäkkäisillä näkyvyysalueilla on se, että "sisältä näkee ulos, mutta ulkoa ei näe sisään". Sulkeuma poikkeaa näkyvyysalueen normaalista määrittelystä, sillä siinä funktio suoritetaan oman näkvyysalueen sijasta sulkeuman määrittelyn funktion näkyvyysalueessa.
 
### sulkeuma

JavaScriptissä funktio voi saada parametrikseen toisen funktion. Tällöin sulkeumassa funktion parametrin mukana voidaan välittää myös sen muuttujia. Jos funktion sisällä luodaan sisempi funktio, sen näkyvyysalueeseen kuuluvat myös ulomman funktion muuttujat. Eli kun parametrin saanut funktio suorittaa parametrina saamansa funktion, suoritetaan se parametrina annetun funktion näkyvyysalueessa.

**Sidotut muuttujat** muuttujat ovat funktion muodollisia parametreja sekä funktion sisällä määriteltyjä paikallisia muuttujia. Näillä funktioilla on merkitys vain funktion sisällä ne ovat olemassa vain funktion suorituksen ajan.

**Vapaat muuttujat** ovat funktion ulkopuolella olevia, mutta funktiossa viitattuja muuttujia, jotka funktiosta näkyvyyssääntöjen:"sisältä näkee ulos", sallimana nähdään.

Nimensä "sulkeuma" (closure) saa siitä, kun funktio välitetään parametrina sen käyttämät vapaat muuttujat "suljetaan" mukaan funktion suoritusta varten.

### 1. Sulkeumaan suljetut vapaat muuttujat säilyvät sulkeuman suorituksen jälkeiseen aikaan.

esimerkki...

### 2. Sulkeumaan suljetuttujen vapaiden muuttujien määritellyt funktio päättyy, mutta sulkeuma säilyy

function sulkeumaEsimerkki() {
  var a = "sul", b = "keuma";
  return function() { return a + b };
}
 
Normaalisti olemme tottuneet siihen että paikallinen muuttuja ja sen arvo säilyvät vain tämän funktion elinajan. Tästä poiketen ylläoleva funktio palauttaa toisen funktion, joka näkee ulomman funktion muuttujat a ja b  ja palautta arvon "sulkeuma", vaikka ulkoisen funktion suoritus onkin jo päättynyt. 

### kapselointi...?

"Edellä nähtiin, miten kutsuttu funktio voi sulkeuman vapaiden muuttujien avulla päästä muokkaamaan muuttujia, jotka eivät kuulu funktion omaan näkyvyysalueeseen. Noissa esimerkeissä nuo muuttujat ovat kuitenkin olleet olemassa – "kun funktio käynnistyy, sen paikalliset muuttujat syntyvät, kun funktion suoritus päättyy, sen paikalliset muuttujat häviävät" Tämä tekniikka osoittautuu aikanaan vahvaksi: sitä käyttäen voi toteuttaa mm. olioiden kenttien piilottamisen ja kätkettyjen kenttien "aksessorimetodit" Javan hengessä.(lainaus suoraan luentomatskusta... muokkaa)

### ehkä...?vielä esimerkki kapseloinista?...sen turvallisuus?


## Oliot ja niiden käyttäytyminen: Olioiden käytön hyviä (ja jos mahdollista turvallisia) ohjelmointityylejä ja -malleja.

### Olion luominen

Olion voidaan ajatella olevan jonkin asian yleinen käsite tai esimerkiksi kokoelma tietoja. OLio sisältää ominaisuuksia eli atribuutteja jotka tallennetaan muuttujiin sekä metodeja, joilla käsitellään olion sisältämää tietoa. Ominaisuuksia voidaan kutsua myös olioiden kentiksi. Olioiden voidaan ajatella olevan functioiden ilmentymiä jotka luodaan sanalla -New- . Olit voi käsittää myös assosiaatiotaulukoksi joka sisältää avain- arvopareja, joita käytetään Hashmappien tavoin. 

**Yksinkertainen aaltosuluilla luotu olioliteraali:**
("This" viitteet tarvitaan, jotta tiedetään viitattavan juuri kyseisen olion kenttiin.)

let noora = {nimi: "Noora", syntymavuosi: 2000, ika: 35};


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
var tokahenkilo = new Henkilo("Virva", 15);

Olion ilmentymät luodaan new-operaattorilla,ja jolloin sille viedään parametreina henkilön tiedot: etunimi ja ikä.
 
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
 
**Olioden luonti JavaScriptin "luokka" eli class-määrittelyn avulla.**

ECMAScript 6 esitteli class-rakenteen luokkien ja olioiden luomiseen.
```
 class Henkilo{
 constructor(nimi, yearnow, syntymavuosi);{
 this.nimi=Tytti;
 this.yearnow=2018;
 this.syntymavuosi=200;
}
ika(){
this.yernow - this.syntymavuosi}
} 
} //18
´´´

### Olion metodit
Javasta  poiketen olion kentiksi voi antaa myös metodeja, jotka määritellään vastaavalla tavalla kuin funktio. Metodissa viitataan olion muuttujiin this-osoittimen avulla this.yearnow, this.syntymavuosi. Eli metodin ika-muuttujiin sijoitetaan arvo olion yearnow ja syntymavuosi-muuttujista.Metodiin viitataan/sitä kutsutaan syntaksilla olio.metodi().

let noora = {nimi: "Noora", syntymavuosi: 2000, yearnow: 2018, ika: function(){return this.yearnow - this.syntymavuosi}};

write(noora.ika()); //18

 
### Olioden dynaamisuudesta:
Javascritissa olion kentät ovat julkisia eli niihin voidaan dynaamisesti lisätä ja niistä  voidaan poistaa kenttiä ja muuttaa arvoja olion luonnin jälkeen. Tämän piirteen kanssa tulee olla huolellinen, ettei tule uutta arvoa sijoittaessa vahingossa lisänneeksi ylimääräistä kenttää,jos esim. vahngossa kirjoittaa kentän nimen väärin. Huom. Oleellinen ero arvoa sijoittaessa ja haetaessa on siis se, sijoittaessa jos kenttää ei ole, se lisätään, huolimatta siitä löytyykö sitä "ylemmästä oliosta" kun taas  haettaessa kuljetaan prototyyppiketjuapitkin aina Objectolioon asti kysymään "ylemmältä" oliolta löytyykö kenttä sieltä. Jos ei löydy palautetaan undefined.
 
  tähän esimerkki...kentän muutto?

**poisto**
Ainut hyvä tapa olion ominaisuuden poistoon on käyttää delete-operaattoria. Ominaisuuden asettaminen joko arvoon undefined tai null poistaa vain siihen liittyneen arvon muttei itse avainta, kuten seuraavasta esimerkistä käy ilmi.

var olio={
eka:1,
toka:2,
kolmas:3
};
olio.eka=undefined;
olio.toka=null;
delete olio.kolmas;

for(var i in olio) {
    if (olio.hasOwnProperty(i)) {
        console.log(i, '' + olio[i]);
    }
}  
Ohjelma tulostaa  m1 undefined ja m2 null. vain m3 on poistettu
Huomaa myös, että oliolion prototyyppiolion kentäntai metodin poisto poistaa kentäät kaikilta sen perineiltä olioilta.
 
olion kentistä:
"Kenttänimenä voi käyttää melkein mitä tahansa: tunnus, merkkijono (jopa tyhjä), luku, ..., kaikki sellaiset kielen arvot" jotka voi muuttaa merkkijonoksi:

**Olion kenttiin viittaamine ja läpikäynti**
olion kentän tietoihin tietoihin pääsee käsiksi syntaksilla olio.ominaisuus tai vaihtoehtoisesti tietoihin voidaan osoittaa indeksin avulla  hakasulkunotaatiolla, jolloin ominaisuuksien arvoja voidaan asettaa dynaamisesti.
	
 var elain = {nimi: 'Miuku'}
	elain.nimi ; //Miuku
	elain[‘nimi’]:  //Miuku


 
 Koska olioden kentät assosiaatiotaulukoita, olioiden  numeroituvia kenttiä voidaan käydä läpi taulukon tavoin for kentta in olio raneteella, mukana tulostuu myös perityt kentät

 
Object.prototype.lintu = "Peippo";
var nisakas {kissa: "Miuku"};
for(var i in elain) {
    console.log(i); // tulostaa sekä lintu että kissa
}

 lisää kenttirn läpikäynti mahdollisuuksia...???

Jos halutaan selvittää pelkästään olion omat kentät voisi sen suorittaa Tämä on mahdollista käyttäen Object.prototype-olion hasOwnProperty-metodia. Seuraavassa metodissa tulostuu vain kissa
 
 Object.prototype.lintu = "Peippo";
var nisakas {kissa: "Miuku"};
 for(var i in elain) {
    if (foo.hasOwnProperty(i)) {
        console.log(i);
    }
}
 
Lähteet:  
  
https://fi.wikipedia.org/wiki/Sulkeuma_(ohjelmointi)

https://www.cs.helsinki.fi/u/wikla/OTjs/materiaalia/funktiot/
