

# 3. oliot, protoryypit ja periytyminen

Javascriptissä on olemassa kolmenlaisia olioita: funktio-olioita, niihin liittyviä prototyyppiolioita ja "tavallisia" olioita. Oliot perivät ominaisuuksia prototyyppiolioltaan. Vain funktiolla Funktion, prototyyppi ja prototyyppiolio-olio ovat sama asia.

Prototyyppiperiytyminen perustuu **Object ja Function** olioihin(funktioihin), jotka pitävät sisällään joukon kenttiä, kielen peruskalustoa. Ne molemmat toimivat myös konstruktorifunktioina joiden avulla luodaan uusia olioita ja funktioita.

Kuten alla oleva kuva havainnollistaa kaikki oliot perivät **Object-funktion prototyyppiolion** kentät. Kaikki funktiot puolestaan perivät lisäksi **Function-funktion prototyyppiolion** kentät. 

<img src="https://github.com/vsvala/JavaScript_ohjelmointitekniikka/blob/master/Untitled%20Diagram.jpg" >

### __ proto__-kenttä ja prototyyppiketju

Jokaiselta oliolta löytyy yksi kenttä **__proto__** "minun prototyyppini", jonka osoittaa oman prototyyppiketjun lähimpään prototyyppiolioon.Konstruktorifunktioiden prototyyppiolioista muodostuu linkitettyjä perintäketjuja. Luokkametodilla Object.getPrototypeOf(olio) saa selvitettyä mihin prototyyppiolioon __proto__ kenttä viittaa. Toinen tapa selvittää asia a on Käsky  x.__proto__, mutta tämä ei kuitenkaan välttämättä toimi vanhoilla selaimilla, joten on varmempaa käyttää ensimmäistä tapaa.

JavaScriptin perintä perustuu siis __proto__ -kenttiin, joista muodostuu keskenään perintäketjuja. __proto__ kenttä viittaa aina perittävään prototyyppiolioon, jonka __proto__ -kenttä puolestaan viittaa taas sen prototyyppiolioon. Perintä jatkuu **prototyyppiketjua** ylöspäin aina Function funktion prototyyppikenttään asti jonka __proto__-kenttä osoittaa null:ia. Normaalisti jokaisen olion prototyyppien ketju päättyykin Object-funktion prototyyppiolioon.

"Kun olion x kenttään viitataan arvoa hakien, haetaan ensin olion omista kentistä. Jos ei löydy, tutkitaan olion Object.getPrototypeOf(x) kentät. Jos niistäkään ei löydy haettua arvoa, etsitään Object.getPrototypeOf(Object.getPrototypeOf(x)), jne. Näin edetään Object.prototype-kentän osoittamaan olioon eli Object-funktion prototyyppiolioon saakka, mihin ketju päättyy: Object.getPrototypeOf(Object.prototype)===null. Tällöin palautetaan arvo undefined.

### Prototyyppiperinnän käyttö copy-paste -koodin välttämiseksi
Perinnän avulla voidaan poistaa turhaa koodin kopioimista. Konstruktorifunktion prototyyppiolioon voidaan liittää ominaisuuksia, jotka kaikki kyseisellä funktiolla konstruoidut oliot jakavat keskenään.Jos konstruktorin avulla olioita tehtaillessa olioilla on samoja funktioita tai ominaisuuksia, olisikin parempi ohjelmointityyli liittää yhteiset ominaisuudet prototyyppiolioon kaikkien perittäväksi, jotta vältytään koodin toisteisuudelta. Esimerkissä noora ja virva perivät molemmat asuinmaakseen Suomen.

```
function Henkilo(nimi, ika) { this.nimi = nimi; this.ika = ika;  }

noora = new Henkilo("Noora", 35);
virva = new Henkilo("Virva", 5);

Henkilo.prototype.opiskelupaikka = "Helsingin yliopisto"} 
Henkilo.prototype.asuinmaa = "Suomi"

console.log(noora.tuplaaIka()); //70
console.log(virva.tuplaaIka()); //10
console.log(virva.asuinmaa); //Suomi 
console.log(noora.asuinmaa); //Suomi 
```

Pidempiä perimisketjuja voidaan rakentaa korvaamalla olion prototyyppiolioita uudella oliolla seuraavasti. 

```
function Elain() {
  this.reviiri = "puisto"
  this.paino = 0;
  this.syo = function() {this.paino+10} {
}

function Lintu() {
  this.siipienVari = "";
  this.lauluAani = "titityy";
}

Lintu.prototype = new Elain()

function Peippo(nimi) {
  this.nimi = nimi;

Peippo.prototype = new Lintu()


var sirkku = new Peippo("Sirkku")


sirkku.nimi;          // Sirkku"
sirkku.lauluAani;     //"titityy"
sirkku.siipienVari;   // ""
sirkku.siipienVari = "musta";  //"musta"   
sirkku.paino;  // 0

sirkku.syo();  
sirkku.syo();
sirkku.syo();               
sirkku.paino;  // 30
sirkku.reviiri; // "puisto"
 
 ```
Tällöin muodostuu alla olevan mukainen perintäketju, missä alimpana luotu Peippo perii itselleen käyttöönsä  kaikkien ylempien olioden ominaisuuksia.

<img src="https://github.com/vsvala/JavaScript_ohjelmointitekniikka/blob/master/JSel%C3%A4in%20(1).png" >


## perintä Object.createn avulla 
JavaScriptin versioon 1.8.5 ja ECMAScriptin 5. editioon on lisätty funktio Object.create, jonka tarkoituksena on kloonata olio suoraan toisesta oliosta. Tämä ei kuitenkaan toimi aina ihan odotetulla tavalla ja saattaa aiheuttaa ongelmia. sen käytön suhteen kannattaakin olla varovainen.



http://ohtekjs.github.io/#olioliteraalitetc

