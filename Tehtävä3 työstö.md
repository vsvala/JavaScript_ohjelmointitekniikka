
# 3. oliot, protoryypit ja periytyminen

Javascriptissä on olemassa kolmenlaisia olioita: funktio-olioita, niihin liittyviä prototyyppiolioita ja "tavallisia" olioita. Oliot perivät ominaisuuksia prototyyppiolioltaan. Vain funktiolla Funktion prototyyppi ja prototyyppiolio-olio ovat sama asia.

Prototyyppiperiytyminen perustuu Object ja Function olioihin(funktioihin), jotka pitävät sisällään joukon kenttiä, kielen peruskalustoa. Ne molemmat toimivat myös konstruktorifunktioina joiden avulla luodaan uusia olioita ja funktioita.

Kuten alla oleva kuva havainnollistaa kaikki oliot perivät Object-funktion prototyyppiolion kentät. Kaikki funktiot puolestaan perivät lisäksi Function-funktion prototyyppiolion kaikki kentät.

PÄIVITÄ KORJATTU KUVA
<img src="https://github.com/vsvala/JavaScript_ohjelmointitekniikka/blob/master/Untitled%20Diagram.png" >

### Prototyyppiperinnän käyttö copy-paste -koodin välttämiseksi
Perinnän avulla voidaan poistaa turhaa koodin kopioimista. Esimerkiksi jos oliot jakavat samoja  metodeita tai muuttujia voidaan ne siirtää perittäväksi ylemmältä prototyyppioliolta, jolloin päästään eroon turhasta koodin toistosta.

Tähän esimerkki

## a) ratkaistavan ohjelmointiongelman käsitteiden luonteva mallintaminen ja siten siis ongelman ratkaisijan ajattelun selkeyttäminen ja helpottaminen.

##  b) koodin turhan kopioimisen välttäminen, koodin uudelleenkäyttö.

Pyrkikää hahmottamaan ja löytämään, millaiset JavaScriptin ohjelmointitekniikat mahdollisimman hyvin palvelisivat näitä tavoitteita. Perusteluja tarvitaan!


