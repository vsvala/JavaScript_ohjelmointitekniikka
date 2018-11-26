
# 3. oliot, protoryypit ja periytyminen

Javascriptissä on olemassa kolmenlaisia olioita: funktio-olioita, niihin liittyviä prototyyppiolioita ja "tavallisia" olioita. Oliot perivät ominaisuuksia prototyyppiolioltaan. Vain funktiolla Funktion prototyyppi ja prototyyppiolio-olio ovat sama asia.

Prototyyppiperiytyminen perustuu **Object ja Function** olioihin(funktioihin), jotka pitävät sisällään joukon kenttiä, kielen peruskalustoa. Ne molemmat toimivat myös konstruktorifunktioina joiden avulla luodaan uusia olioita ja funktioita.

Kuten alla oleva kuva havainnollistaa kaikki oliot perivät Object-funktion prototyyppiolion kentät. Kaikki funktiot puolestaan perivät lisäksi Function-funktion prototyyppiolion kaikki kentät.

PÄIVITÄ KORJATTU KUVA
<img src="https://github.com/vsvala/JavaScript_ohjelmointitekniikka/blob/master/Untitled%20Diagram.png" >

### Prototyyppiketju ja __proto__-kenttä

Jokaisella oliolla on yksi kenttä "minun prototyyppini", joka osoittaa kyseisen olion prototyyppiolioon.Tämän linkin olion prototyyppiin, saa "luokkametodilla" Object.getPrototypeOf:(olio). Jokaisella oliolla on myös kenttä _proto_ joka osoittaa oman prototyyppiketjun lähimpään prototyyppiin.Käsky x.__proto__ ei kuitenkaan välttämättä toimi vanhoilla selaimilla, joten prototyypin selvittämiseen on varmempaa käyttää ensimmäistä.   ???tarkasta menikö tämä juttu nyt oikein...

"Kun olion x kenttään viitataan arvoa kysellen, ensin etsitään olion omista kentistä. Ellei löydy, tutkitaan olion Object.getPrototypeOf(x) kentät. Ellei niistäkään löydy haettua, tutkitaan olio Object.getPrototypeOf(Object.getPrototypeOf(x)), jne. Näin voidaan edetä aina Object.prototype-kentän osoittamaan olioon eli Object-funktion prototyyppiolioon saakka.
Siihen ketju päättyy: Object.getPrototypeOf(Object.prototype)===null. Jos kentän arvoa haettaessa päästään ketjun loppuun haettua kenttää löytämättä, palautetaan arvo undefined."Suoraa Lainausta muokkaa...


"Jokaisella oliolla on kenttä oman prototyyppiketjun lähimpään prototyyppiin. Kentän nimi on __proto__ (kaksi alaviivaa alussa ja lopussa)."Suoraa Lainausta muokkaa...

### Prototyyppiperinnän käyttö copy-paste -koodin välttämiseksi
Perinnän avulla voidaan poistaa turhaa koodin kopioimista. Esimerkiksi jos oliot jakavat samoja  metodeita tai muuttujia voidaan ne siirtää perittäväksi ylemmältä prototyyppioliolta, jolloin päästään eroon turhasta koodin toistosta.

Tähän esimerkki

## a) ratkaistavan ohjelmointiongelman käsitteiden luonteva mallintaminen ja siten siis ongelman ratkaisijan ajattelun selkeyttäminen ja helpottaminen.

##  b) koodin turhan kopioimisen välttäminen, koodin uudelleenkäyttö.

Pyrkikää hahmottamaan ja löytämään, millaiset JavaScriptin ohjelmointitekniikat mahdollisimman hyvin palvelisivat näitä tavoitteita. Perusteluja tarvitaan!


