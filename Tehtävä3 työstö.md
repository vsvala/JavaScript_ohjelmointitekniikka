
http://ohtekjs.github.io/#olioliteraalitetc
tän lopussa ...

# 3. oliot, protoryypit ja periytyminen

Javascriptissä on olemassa kolmenlaisia olioita: funktio-olioita, niihin liittyviä prototyyppiolioita ja "tavallisia" olioita. Oliot perivät ominaisuuksia prototyyppiolioltaan. Vain funktiolla Funktion, prototyyppi ja prototyyppiolio-olio ovat sama asia.

Prototyyppiperiytyminen perustuu **Object ja Function** olioihin(funktioihin), jotka pitävät sisällään joukon kenttiä, kielen peruskalustoa. Ne molemmat toimivat myös konstruktorifunktioina joiden avulla luodaan uusia olioita ja funktioita.

Kuten alla oleva kuva havainnollistaa kaikki oliot perivät **Object-funktion prototyyppiolion** kentät. Kaikki funktiot puolestaan perivät lisäksi **Function-funktion prototyyppiolion** kentät. 

<img src="https://github.com/vsvala/JavaScript_ohjelmointitekniikka/blob/master/Untitled%20Diagram.jpg" >

### __ proto__-kenttä ja prototyyppiketju

Jokaiselta oliolta löytyy yksi kenttä **__proto__** "minun prototyyppini", jonka osoittaa oman prototyyppiketjun lähimpään prototyyppiolioon.Konstruktorifunktioiden prototyyppiolioista muodostuu linkitettyjä perintäketjuja. Luokkametodilla Object.getPrototypeOf(olio) saa selvitettyä mihin prototyyppiolioon __proto__ kenttä viittaa. Toinen tapa selvittää asia a on Käsky  x.__proto__, mutta tämä ei kuitenkaan välttämättä toimi vanhoilla selaimilla, joten on varmempaa käyttää ensimmäistä tapaa.

JavaScriptin perintä perustuu siis __proto__ -kenttiin, joista muodostuu keskenään perintäketjuja. __proto__ kenttä viittaa aina perittävään prototyyppiolioon, jonka __proto__ -kenttä puolestaan viittaa taas sen prototyyppiolioon. Perintä jatkuu **prototyyppiketjua** ylöspäin aina Function funktion prototyyppikenttään asti jonka __proto__-kenttä osoittaa null:ia. Normaalisti jokaisen olion prototyyppien ketju päättyykin Object-funktion prototyyppiolioon.


------------------------------alla vielä suoraa lainausta:

"Kun olion x kenttään viitataan arvoa kysellen, ensin etsitään olion omista kentistä. Ellei löydy, tutkitaan olion Object.getPrototypeOf(x) kentät. Ellei niistäkään löydy haettua, tutkitaan olio Object.getPrototypeOf(Object.getPrototypeOf(x)), jne. Näin voidaan edetä aina Object.prototype-kentän osoittamaan olioon eli Object-funktion prototyyppiolioon saakka.
Siihen ketju päättyy: Object.getPrototypeOf(Object.prototype)===null. Jos kentän arvoa haettaessa päästään ketjun loppuun haettua kenttää löytämättä, palautetaan arvo undefined."Suoraa Lainausta muokkaa...


tähän voisi ottaa koodi esimerkin ja piirtää...

** Eli kuvan konstruktorifunktion F prototyyppiketju menisi seuraavasti.
F.__proto__===Function.prototype
F.__proto__.__proto__===Object.prototype
F.__proto__.__proto__.__proto__===null

Funktio "F perii yleiset funktio-ominaisuutensa Function-funktion prototyyppioliolta ja yleiset olio-ominaisuutensa Object-funktion prototyyppioliolta."

------------------


### Prototyyppiperinnän käyttö copy-paste -koodin välttämiseksi
Perinnän avulla voidaan poistaa turhaa koodin kopioimista. 


Konstruktorifunktion prototyyppiolioon voidaan liittää ominaisuuksia, jotka kaikki kyseisellä funktiolla konstruoidut oliot jakavat keskenään.Jos konstruktorin avulla olioita tehtaillessa olioilla on samoja funktioita tai ominaisuuksia, olisikin parempi ohjelmointityyli liittää yhteiset ominaisuudet prototyyppiolioon kaikkien perittäväksi, jotta vältytään koodin toisteisuudelta.

```
function Henkilo(nimi, ika) { this.nimi = nimi; this.ika = ika; }

noora = new Henkilo("Noora", 35);
virva = new Henkilo("Virva", 5);

Henkilo.prototype.tuplaaIka = function() {return this.ika * 2} 

console.log(noora.tuplaaIka()); //70
console.log(virva.tuplaaIka()); //10

```

## a) ratkaistavan ohjelmointiongelman käsitteiden luonteva mallintaminen ja siten siis ongelman ratkaisijan ajattelun selkeyttäminen ja helpottaminen.

##  b) koodin turhan kopioimisen välttäminen, koodin uudelleenkäyttö.

Pyrkikää hahmottamaan ja löytämään, millaiset JavaScriptin ohjelmointitekniikat mahdollisimman hyvin palvelisivat näitä tavoitteita. Perusteluja tarvitaan!




## perintä prototyypilltä...
## perintä Object.createn avulla (huom varovaisuus--> kaksjalkinen leijona!!!)
JavaScriptin versioon 1.8.5 ja ECMAScriptin 5. editioon on lisätty funktio Object.create, jonka tarkoituksena on  kloonata olio suoraan toisesta oliosta. Tämä ei kuitenkaan toimi aina odotetulla tavalla ja saattaa aiheuttaa ongelmia esim.....
esimerkki???
