
# 3. oliot, protoryypit ja periytyminen

Javascriptissä on olemassa kolmenlaisia olioita: funktio-olioita, niihin liittyviä prototyyppiolioita ja "tavallisia" olioita. Oliot perivät ominaisuuksia prototyyppiolioltaan. Vain funktiolla Funktion, prototyyppi ja prototyyppiolio-olio ovat sama asia.

Prototyyppiperiytyminen perustuu **Object ja Function** olioihin(funktioihin), jotka pitävät sisällään joukon kenttiä, kielen peruskalustoa. Ne molemmat toimivat myös konstruktorifunktioina joiden avulla luodaan uusia olioita ja funktioita.

Kuten alla oleva kuva havainnollistaa kaikki oliot perivät Object-funktion prototyyppiolion kentät. Kaikki funktiot puolestaan perivät lisäksi Function-funktion prototyyppiolion kentät. Konstruktorifunktioiden prototyyppiolioista muodostuu linkitettyjä perintä ketjuja.

<img src="https://github.com/vsvala/JavaScript_ohjelmointitekniikka/blob/master/Untitled%20Diagram.jpg" >

### Prototyyppiketju ja __proto__-kenttä

Jokaiselta oliolta löytyy yksi kenttä _proto_ "minun prototyyppini", jonka osoittaa oman prototyyppiketjun lähimpään prototyyppiolioon. Luokkametodilla Object.getPrototypeOf(olio) saa selvitettyä mihin prototyyppiolioon _proto_ kenttä viittaa. Toinen tapa selvittää asia a on Käsky  x.__proto__, mutta tämä ei kuitenkaan välttämättä toimi vanhoilla selaimilla, joten on varmempaa käyttää ensimmäistä tapaa.

JavaScriptin perintä perustuu _proto_ -kenttiin, joista muodostuu keskenään perintäketjuja. _proto_ kenttä viittaa aina perittävään prototyyppiolioon, jonka -proto kenttä puolestaan viittaa taas sen prototyyppiolioon. Perintä jatkuu prototyyppiketjua ylöspäin aina Function funktion prototyyppikenttään asti joka osoittaa null:ia. Normaalisti jokaisen olion prototyyppien ketju päättyy Object-funktion prototyyppiolioon.



"Kun olion x kenttään viitataan arvoa kysellen, ensin etsitään olion omista kentistä. Ellei löydy, tutkitaan olion Object.getPrototypeOf(x) kentät. Ellei niistäkään löydy haettua, tutkitaan olio Object.getPrototypeOf(Object.getPrototypeOf(x)), jne. Näin voidaan edetä aina Object.prototype-kentän osoittamaan olioon eli Object-funktion prototyyppiolioon saakka.
Siihen ketju päättyy: Object.getPrototypeOf(Object.prototype)===null. Jos kentän arvoa haettaessa päästään ketjun loppuun haettua kenttää löytämättä, palautetaan arvo undefined."Suoraa Lainausta muokkaa...

** Eli kuvan konstruktorifunktion F prototyyppiketju menisi seuraavasti.
F.__proto__===Function.prototype
F.__proto__.__proto__===Object.prototype
F.__proto__.__proto__.__proto__===null

Funktio "F perii yleiset funktio-ominaisuutensa Function-funktion prototyyppioliolta ja yleiset olio-ominaisuutensa Object-funktion prototyyppioliolta."



### Prototyyppiperinnän käyttö copy-paste -koodin välttämiseksi
Perinnän avulla voidaan poistaa turhaa koodin kopioimista. Esimerkiksi jos oliot jakavat samoja  metodeita tai muuttujia voidaan ne siirtää perittäväksi ylemmältä prototyyppioliolta, jolloin päästään eroon turhasta koodin toistosta.

Tähän esimerkki

## a) ratkaistavan ohjelmointiongelman käsitteiden luonteva mallintaminen ja siten siis ongelman ratkaisijan ajattelun selkeyttäminen ja helpottaminen.

##  b) koodin turhan kopioimisen välttäminen, koodin uudelleenkäyttö.

Pyrkikää hahmottamaan ja löytämään, millaiset JavaScriptin ohjelmointitekniikat mahdollisimman hyvin palvelisivat näitä tavoitteita. Perusteluja tarvitaan!




## perintä prototyypilltä...
## perintä Object.createn avulla (huom varovaisuus--> kaksjalkinen leijona!!!)
JavaScriptin versioon 1.8.5 ja ECMAScriptin 5. editioon on lisätty funktio Object.create, jonka tarkoituksena on  kloonata olio suoraan toisesta oliosta. Tämä ei kuitenkaan toimi aina odotetulla tavalla ja saattaa aiheuttaa ongelmia esim.....
esimerkki???
