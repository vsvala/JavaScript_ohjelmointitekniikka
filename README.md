# JavaScript_ohjelmointitekniikka: hajoitustyö 2018
  Virva Svala ja Noora Virolainen



1. [Suosituksia hyviksi JavaScript-ohjelmointikäytännöiksi](#1)
2. [Tyyppiturvallisuuden tavoittelua](#2)
3. [Funktionaalinen vai Imperatiivinen ohjelmonti](#3)
4. [Sulkeumat ja sen käyttötavat](#4)
5. [Oliot ja niiden käyttäytyminen](#5)
6. [Protoryypit ja periytyminen](#6)
7. [Suunnittelumalleja](#7)

# 1 
# Suosituksia hyviksi JavaScript-ohjelmointikäytännöiksi 

JavaScript ohjelmointitekniikan kurssin tehtävänä oli laatija yhtenäinen ohjeisto hyvään JavaScript-ohjelmointiin. Alla olevasta koostamastamme dokumentista löytyy keräämiämme kielen keskeisiä piirteitä ja käsitteiden selvenyksiä sekä suosituksia hyviksi JavaScript-ohjelmointikäytännöiksi.

# 2
# Tyyppiturvallisuuden tavoittelua	

JavaScript on dynaamisesti tyypitetty:muuttujilla, muodollisilla parametreilla ja funktioilla ei ole tyyppiä, mutta arvoilla on. Dynaamisessa tyypistyksessä tyyppi voi muuttua ajon aikana, kun taas staattisessa tyypit ovat tiedossa jo käännösvaiheessa. Dynaaminen tyypitys luo kieleen joustavuutta, muttei kuitenkaan välttämättä aina ole staattista tyypitystä parempi ratkaisu. Staattisen tyyppijärjestelmän avulla useat virheet havaitaan jo käännösaikana, kun taas dynaamisesti tyypitetyssä kielessä vasta ajon aikana, mikä ainakin aloittelevan JavaScript koodaajan kannalta ei ole niin mukavaa.
    
Ohjelmointikielen tyyppijärjestelmä sanelee, kuinka ohjelmointikieli luokittelee arvot ja muuttujat tyyppeihin, kuinka se käsittelee näitä tyyppejä ja miten ne  toimivat keskenään. Tyypit siis  määrittelevät, millä tavoin se voi toimia muiden muuttujien tai arvojen kanssa. Tyyppitarkastuksessa varmistutaan siitä, että tyypit toimivat näiden rajoitusten mukaan, eli tarkastetaan osa ohjelman semantiikasta.

Javascriptin tietotyypit ovat **merkkijono (string), luku (number), totuusarvo (boolean), taulukko (array), objekti (object), olematon (null) ja määrittelemätön (undefined).**

Jos muuttujalle ei anna arvoa heti luontihetkellä, saa se automaattisesti arvokseen undefined. Kyseessä on ihan oikea arvo, jota voi tutkia ja vertailla. Mietimme olisiko joissain tapauksissa parempi korvata undefined esim. arvolla null, jolloin arvo saa kentän tyyppiä object. Jos ei ole erityistä tarvetta on mielestämme ihan ok ja aikaa sästävää, että kaikille tyypeille ei tarvitse antaa erikseen itse arvoa. Tämä on yksi JavaScript kielen ominaisuus, jota mielestämme kannattaa mahdollisuuksien mukaan hyödyntää ohjelmoimisessa.

Jos on tarpeen selvittää onko muuttujan arvo undefined vai null, voitaisiin se tehdä seuraavalla tavalla:

```
var a;
var b = null;
typeof a === undefined // true;
a === undefined // true;
b === null // true;
```

Tyyppien tarkistamisen tarve kasvaa esimerkiksi käsiteltäessä käyttäjän syöttämiä arvoja. Javascript ei itsestään huomauta väärien tyyppien käytöstä, joten kaikki tarkistukset jäävät  ohjelmoijan vastuulle. JavaScript kielessä on joukko arvon tyypin tutkimisen välineitä, Tässä laatimamme ehdotuslista kirjastofunktioista, joilla arvojen tyyppejä voitaisiin tarkastaa.

Type of operaattori kertoo sille operandina annettavan muuttujan tyypin ja sitä voidaan käyttää yleisesti erilaisten tyyppien tarkastukseen.  Se ei kuitenkaan ole kaikissa tapauksissa tarkin tapa  erotella tyyppejä, sillä se ei osaa esimerkiksi erottaa erityyppisiä objekteja. Se määrittelee esim. että null on objekti ja NaN on numero.

```
<p>typeof "Ville";                 // string</p> 
<p>typeof 4;                      // number</p>
<p>typeof "4";                    // string</p>
<p>typeof NaN;                    // number</p>
<p>typeof null;                   // object </p>

```
## Kokonaisluvut ja numeeriset arvot

<p>JavaScript kielessä ei ole Java kielestä poiketen erillistä kokonaislukutyyppiä, vaan numeerinen lukuarvo number, joka voi sisältää sekä kokonaislukuja että liukulukuja.  Käsittääksemme kokonaislukujen tarkistaminen ei aina ole välttämätöntä , koska­  tarvittaessa likuluvun saa muutettua kokonaisluksi helposti esimerkiksi Math.floor-funktiolla. Jos kuitenkin tarkastusta on tarpeellista tehdä esim, halutessamme käyttäjältä tarkan kokonasilukusyötteen, voitaisiin se tehdä esimerksi seuraavilla tarkastusfunktioilla. </p>
<p>Javassa olevat operaatiot parseInt ja parseFloat toimivat tarkastajina niissä tapauksissa joissa syöte alkaa numeroilla, jolloin siiitä erotetaan numero-osa ja muut jätetään huomiotta. Mutta tämä ei toimi esim, jos syöte alkaa vaikkapa kirjaimella jota seuraa numero. Tällöin tarvimme toista tarkastustapaa. </p>
<p>Helpoin tapa tarkistaa onko luku kokonaisluku on tarkastella onko sillä desimaaliosaa, eli onko sen jakojäännös nollasta eroava numerolla yksi jaettaessa. Ennen tätä tarkastelua täystyisi kuitenkin varmistaa että syöte on numeerinen. Tämä  ei kuitenkaan ole kaikissa tapauksissa toimivin esimerkiksi  mikäli syöte on luotu konstruktoria käyttäen: JavaScript tekee automaattisen tyyppimuunnoksen jakojäännösoperaattorin yhteydessä </p>

<p>Tarkastusfunktio numerolle <p>
	
<div class="highlight"><pre><span class="kd">function</span> <span class="nx">isNumber</span><span class="p">(</span><span class="nx">value</span><span class="p">)</span> <span class="p">{</span>
    <span class="k">return</span> <span class="k">typeof</span> <span class="nx">value</span> <span class="o">===</span> <span class="s1">'number'</span>
<span class="p">}</span></pre></div>
<br>
<p>Tarkastusfunktio kokonaisluvulle palauttaa truen jos annettu luku kokonaisloko </p>
<div class="highlight"><pre><span class="kd">function</span> <span class="nx">isInteger</span><span class="p">(</span><span class="nx">value</span><span class="p">)</span> <span class="p">{</span>
    <span class="k">return</span> <span class="nx">value</span> <span class="o">===</span> <span class="nb">Math</span><span class="p">.</span><span class="nx">floor</span><span class="p">(</span><span class="nx">value</span><span class="p">)</span>
<span class="p">}</span>
</pre></div>

Kolmanneksi vaihtoehdoksi numeeristen tyyppien tarkastamiseen löysimme Javascriptistä löytyvän valmiin sisäänrakennetun tarkastusfunktion.

```
<p>Number.isInteger(3);         //true</p>

<p>Number.isInteger(0.1);       //false </p>

<p>Number.isFinite(Infinity);   //false </p>
<p>Number.isFinite(0);          //true </p>

<p>Number.isNaN(NaN);           //true </p>
<p><pNumber.isNaN(3);             //false</p>

```

JavaScriptin valmis typeOf funktio toimii tarkastuksissa tiettyyn pisteesee, se ei ole kaikissa tapauksissa riittävä.
Alla määritelty muuttuja a on Number olio ja se käyttäytyy oikein laskutoimituksissa, mutta sen tyyppi ei ole numero. Jotta tämä saadaan määriteltyä oikein täytyy viitata hierarkiassa ylöspäin Object function prototyyppi olion toString:iin. Tällöin niin Number-olio kuin numero yksikin tunnistetaan numeroiksi, kun taas merkkijono ”1” saa tyypikseen String:

```
var a = new Number(4)
write(typeof a == 'number')                                           // false
write(typeof 2 == 'number')                                           // true
write(typeof "2" == 'number')                                         // false
write(a + 1)                                                          // 4
write(a % 1)                                                          // 0
write(1 + "1")                                                        // 11
write(Object.prototype.toString.call(a) == '[object Number]')         // true
write(Object.prototype.toString.call(1) == '[object Number]')         // true
write(Object.prototype.toString.call("1") == '[object Number]')       // false
```

<p>Liukuluvun tarkastukseen toimii seuraava tarkastusfunktio, joka tarkastaa ettei luvun desimaaliosa ole nolla:</p>

```
<p>function isDouble (value) {</p> 
<p> return typeof value === "number" && !isNaN(value) && value !== Math.floor(n)}</p>
```

## Merkkijonot
<p>Merkkijonojen tarkastukseen kävisi seuraava tarkastusfunktio:</p>

```
function isString(value){</p>
<p>return typeof value ==='string'</p>
```

Java Scriptissä ei ole yhtämerkkiä vastaavaa tietotyyppiä char kuten Javassa. Jos tarvii selvittää onko esim. annettu merkki yhden kirjaimen mittainen, siihen kävisi seuraava tarkastusfunktio: 

```
function isChar(i) {
return isString(i) && i.length == 1;}
```

## Totuusarvot
<p>Totuusarvoja voitaisiin tarkestella esim. seuraavalla tarkastusfunktiolla:</p>

```
<p>function isBoolean(value){ </p>
return typeof value==='boolean';} </p>
```


## Taulukot
<p>Seuraava funktio toimii tarkastusfunktiona taulukolle. Kutsuttaessa eri arvoilla se palauttaa true tai false.</p>

```
<p>function isArray(value) {</p>
<p>    return value instanceof Array;}</p>
<p>isArray(2)   //false</p>
<p>isArray([2,1]) //true </p>
```

# 3
# Funktionaalinen vai imperatiivinen ohjelmointi

## Imperatiivinen ohjelmointi
<p>Imperatiivisessa ohjelmoinnissa ongelmanratkaisu kuvataan vaihevaiheelta etenevin komennoin järjestyksessä. Komennot muuttavat suorituksen tilaa ja muuttavat muuttujien arvoja. Tyypillistä imoeratiiviselle ohjelmointityylille on muokattavat tietorakenteet, sekä ehtolausekkeet, toistolauseet sekä poikkeukset. Imperatiiviselle olioohjelmoinnille tyypillisesti asioita kuvataan olioina ja toimintoja olioihin liittyvinä metodeina. Java kieleen alkuun tottuneelle imperatiivinen ohejlointikieli voi tuntua helppolukuismmalta.</p>

## Funktionaalinen ohjelmointi
<p>Funktionaalinen ohjelmointiparadigma perustuu matemaattisten funktioiden käyttöön, tarkemmin lambdakalkyyliin. Olennaista funktionaaliselle ohjelmointiyylille on, että ohjelmissa ei ole tilaa. Funktiot laaditaan niin, että ne eivät muutaolemassa olevia muuttujia. Funktionaalisesssa ohjelmoinnissa ei käytetä sijoituslauseita tai silmukoita, eikä muuttujien arvoja ei vaihdeta kun ne on kerran asetettu. Tämän vuoksi funktionaalinen tyylis soveltuukin hyvin matemaattisiin tarkoituksiin. Suuria arvoja käsitellään usein rekursion avulla. Funktiolla ei ole sivuvaikutuksia, joten sen arvot pysyvät samoina aina samoilla parametreilla. Funktionaalisen ohjelmointityylin yksi etu onkin siinä, että funktiot ovat luotettavia. Ne tekevät aina täsmälleen samoin ja aina täysin loogisesti.  Ne voi myös helpommin  pilkkoa pienimpiin osasiinsa, jossa ne on helppo testata kun ei tarvitse huomioida tilamuutoksia.  Myös rinnakkaisuuden toteutus on helpompaa. Funktionaalisen ohjelmoinnin tllattomuus voi kuitenkin myös aiheuttaa päänvaivaa esimerkiksi websovellukissa, joissa komponentti tarvitsisi tilaa. Tällaisessa tilanteessa voikin olla järkevämpää turvautua hyödyntämään luokkasyntakseja.</p>
<p>Funktionaalisen ohjelmoinnin yhtenä etuna voidaan nähdä sen matemaattisuuden jolloin ohjelmien oikeiksi todistaminen  on helppompaa. Myös koska sivuvaikutuksia ei ole, on funktioiden suoritusjärjestys vapaata ja kääntäjä voi optimoida samanlaisia funktiokutsuja yhdeksi. Funktioiden käsittelylle on myös parmmat tuet ja  JavaScriptissä  voidaankin käyttää nk. Korkeamman asteen funktioita: funktioita voidaankin käyttää parametreina ja funktiot voivat kutsua ja palauttaa funktioita.  Funktionaalista tyyliä käytettäessä ohjelmointikieli on monesti yksinkertaisempaa suunnitella ja toteuttaa ja koodin määrä usein lyhenee. </p>
<p>Seuraavassa esimekki  JavaScriptin yksinkertaisemman korkeamman asteen taulukonkäsittely MAP funktion käytöstä verrattuna saman asian tekevään toistolausekkeella toetutettuun metodiin, joka on huomattavasti pidempi.</p>

```
<p>var animals=[{name: ’Fill’, species:’rabbit’}, {name:’Caro’, Species: ‘dog’}, {name:’Val’, Species: ‘dog’}]</p>
<br>
<p>var names=animals.map(animal) =>animal.name)</p>
<br>
<p>var names =[];</p>
<p>for (var I =0; i &lt; animals.length; i++){ </p>
<p>names.push(animal[i].name)} </p>
```

<p>Toinen esimerkki  kuinka helposti taulukon arvoja pystytään tuplaamaan MAP funktion  avulla.</p>

```
<p>var array1 = [1, 4, 9, 16]; </p>
<p>const map1 = array1.map(x => x * 2);</p>
<p>console.log(map1);   // expected output: Array [2, 8, 18, 32]</p>
```

<p>Mielestämme JavaScriptin kaksiparadigmaisuudessa ei pitäisi ottaa liian jyrkkää kantaa puoleen tai toiseen, vaan järkevintä olisi hyödyntää molempien paradigmojen ohjelmointityyliä sen mukaan mikä olisi kulloiseenkin ohjelmointiprojektiin sopivinta. Olisikin hyvä  opetella molempia tyylejä, jotta oppisi valitsemaan tilanteeseen sopivimman. Imperatiivisen Java kielen äidinkilenään oppineelle funktionaalisen tyylin uusiin ajatusmalleihin tutustuminen tuottaa varmastikin aluksi päänvaivaa. Uskomme kuitenkin, että siihen tutustuminen ja käytön oppiminen on vaivan arvoista.</p>



# 4
# Sulkeumat ja sen käyttötavat

## Näkyvyysalue 
<p>Näkyvyysalueen(scope) perusteella meillä on kahdenlaisia muuttujia: paikalliset(local) ja globaalit(global). Näkyvyysalue määrittelee, missä ja milloin muuttuja on olemasssa ja sen arvo on saatavilla. Totutusta Java kielen lohkoajattelusta poiketen Javascript kielssä funktio muodostaa oman näkyvyysalueensa(scope). Tällöin funktion muodolliset parametrit, paikalliset muuttujat ja paikalliset funktiot näkyvät ja ovat käytettävissä vain ko.funktion sisällä. Funktion näkyvyyaluetta kutsutaan toisinaan myös viittausympäristöksi tai nimiavaruudeksi. JavaScript kieli ei ole Javan tavoin "litteä", sillä funktiot voivat myös muodostaa useita sisäkkäisiä näkyyysalueita/miniavaruuksia. Perusideana JavaScriptin sisäkkäisillä näkyvyysalueilla on se, että "sisältä näkee ulos, mutta ulkoa ei näe sisään". Sulkeuma poikkeaa näkyvyysalueen normaalista määrittelystä, sillä siinä funktio suoritetaan oman näkvyysalueen sijasta sulkeuman määrittelyn funktion näkyvyysalueessa.</p>

## Sulkeuma

<p>JavaScriptissä funktio voi saada parametrikseen toisen funktion. Tällöin sulkeumassa funktion parametrin mukana voidaan välittää myös sen muuttujia. Jos funktion sisällä luodaan sisempi funktio, sen näkyvyysalueeseen kuuluvat myös ulomman funktion muuttujat. Eli esimerkiksi  kun parametrin saanut funktio suorittaa parametrina saamansa funktion, suoritetaan se parametrina annetun funktion näkyvyysalueessa.

</p>
<p><b>Sidotut muuttujat</b>  ovat funktion muodollisia parametreja sekä funktion sisällä määriteltyjä paikallisia muuttujia. Näillä funktioilla on merkitys vain funktion sisällä ne ovat olemassa vain funktion suorituksen ajan.

</p><p><b>Vapaat muuttujat</b> ovat funktion ulkopuolella olevia, mutta funktiossa viitattuja muuttujia, jotka funktiosta näkyvyyssääntöjen:"sisältä näkee ulos", sallimana nähdään.

</p><p>Nimensä "sulkeuma" (closure) saa siitä, kun funktio välitetään parametrina sen käyttämät vapaat muuttujat "suljetaan" mukaan funktion suoritusta varten.</p>

<h2>1. Sulkeumaan suljetut vapaat muuttujat säilyvät sulkeuman suorituksen jälkeiseen aikaan.</h2>

```
<p>var tulo =(function () {</p>
<p> var eka = 0;<p>
<p>var toka = 0;</p>
<p>return function() {</p>
<p>eka += 1;</p>
<p>toka +=1;</p>
<p>return eka * toka }  }) ();</p>
<p> </p>
<p>console.log(tulo()); //1 </p>
<p>console.log(tulo()); //4 </p>
<p>console.log(tulo()); //9 </p>
<p>console.log(tulo()); //16 </p>
```

<h2>2. Sulkeumaan suljetuttujen vapaiden muuttujien määritellyt funktio päättyy, mutta sulkeuma säilyy</h2>

```
<p>function kerro(nimi) {</p>
<p>    var tervehdys = 'Hei ';<p/> 
<p>    var sanoma = function(viesti) { </p>
<p>      console.log(tervehdys + nimi + ', ' + viesti); </p>
<p>    }; </p>
<p>    return sanoma;</p>
<p>}</p>
<p>tulosta = kerro('Noora');</p> 
<p>tulosta('kohta syömään!');</p>  
<p>//Hei Noora, kohta syömään!</p>
```

<p>Normaalisti olemme tottuneet siihen että paikallinen muuttuja ja sen arvo säilyvät vain tämän funktion elinajan. Tästä poiketen ylläoleva funktio palauttaa toisen funktion, joka näkee ulomman funktion muuttujat a ja b ja palautta arvon "sulkeuma", vaikka ulkoisen funktion suoritus onkin jo päättynyt </p>


# 5
# Oliot ja niiden käyttäytyminen 

## Olion luominen
<p>Olion voidaan ajatella olevan jonkin asian yleinen käsite tai esimerkiksi kokoelma tietoja. OLio sisältää ominaisuuksia eli atribuutteja jotka tallennetaan muuttujiin sekä metodeja, joilla käsitellään olion sisältämää tietoa. Olioiden voidaan ajatella olevan functioiden ilmentymiä jotka luodaan sanalla -New- . Olit voi käsitää myös avain- arvopareina, joita käytetään Hashmappien tavoin.</p
	
<p><b>Yksinkertainen aaltosuluilla luotu olio:</b><p/>

```
let noora = {nimi: "Noora", ika: 35};
```
<p>tai määritellään ominaisuudet jälkeenpäin:</p>

```
let virva = {};
virva.nimi = "Virva";
virva.ika = 18;
```
<p><b>Object Olion avulla:</b></p>

```
let noora = new Object();
noora.nimi = "Noora";
noora.ika = 35;
```
Se millä tavalla oliota lähdetään luomaan, riippu aina käyttötarkoituksesta. Yllä esitetyt tavat ovat nopeita ja nidien avulla voi luoda yksittäisiä ns kertakäyttöoliota joilla ei ole yhteisiä ominaisuuksia. Jos kuitenkin tarvitaan useampia samantyyppisiä oliota on se kätevää tehdä konstruktorifunktion avulla. 


<p><b>Konstruktorifunktio</b><p/>
  
  ```
function Henkilo(nimi, ika) {
  this.nimi = nimi;
  this.ika = ika;
}
noora = new Henkilo("Noora", 35);
var tokahenkilo = new Henkilo("Virva", 15);

console.log(noora.ika) //35
console.log(tokahenkilo.nimi) //Virva
```

<p>Konstruktorifunktion prototyyppiolioon voidaan liittää ominaisuuksia, jotka kaikki kyseisellä funktiolla konstruoidut oliot jakavat keskenään.Jos konstruktorin avulla olioita tehtaillessa olioilla on samoja funktioita, olisikin parempi ohjelmointityyli liittää yhteiset ominaisuudet prototyyppiolioon kaikkien perittäväksi, jotta vältytään koodin toisteisuudelta. </p>

```
<p>Henkilo.prototype.tuplaaIka = function() {return this.ika * 2} 
console.log(noora.tuplaaIka()); //70</p>

```
<p><b>tai vielä Object.create-funktion avulla:</b></p>

```
var Henkilo = {
  nimi : "",
  ika : "",
  }
 
 noora = Object.create(Henkilo);
  noora.nimi = "Noora";
  noora.ika = 35;
```

<p>Object.create tavan etuna on, että functiolle annettava prototyyppi voidaan valita vapaasti. Eri tyyppisiä olioita voidaan luoda dynaamisesti samassa functiossa sillä parametrina voi antaa minkä tahansa tyyppisen olion.</p>

<p><b>Olioden luonti JavaScriptin "luokka" eli class-määrittelyn avulla.</b></p>
<p>ECMAScript 6 esitteli class-rakenteen luokkien ja olioiden luomiseen.Pohjimmiltaan sen rakenne on sama kuin kostruktorilla luodulla oliolla. Class luokan olion luokkametodit vastaavat konstruktorilla luodun olion funktio-olion metodeita ja ilmentymämetodit funktio-olion prototyyppiolion metodeja. JavaScriptin luokkametodit eivät kuitenkaan vastaa luokkapohjaisten oliokielten luokkametodia. Luokkiin ei myöskään voida (toistaiseksi?) ohjelmoida tietokenttiä.</p>

```
var Henkilo = {
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

```
<h3>Olion metodit</h3>

Javasta poiketen olion kentiksi voi antaa myös metodeja, jotka määritellään vastaavalla tavalla kuin funktio. Metodissa viitataan olion muuttujiin this-osoittimen avulla this.yearnow, this.syntymavuosi. Eli metodin ika-muuttujiin sijoitetaan arvo olion yearnow ja syntymavuosi-muuttujista.Metodiin viitataan/sitä kutsutaan syntaksilla olio.metodi().

```
var Henkilo = {
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

```
<h3>Olioden dynaamisuudesta:</h3>

Javascritissa olion kentät ovat julkisia eli niihin voidaan dynaamisesti lisätä ja niistä voidaan poistaa kenttiä ja muuttaa arvoja olion luonnin jälkeen. 
Tämän piirteen kanssa tulee olla huolellinen, ettei tule uutta arvoa sijoittaessa vahingossa lisänneeksi ylimääräistä kenttää(jos esim. vahingossa kirjoittaa kentän nimen väärin). Huom! Oleellinen ero arvoa sijoittaessa ja haetaessa on siis se, että  jos sijoittaessa  kenttää ei ole, se lisätään, huolimatta siitä löytyykö sitä "ylemmästä oliosta". Haettaessa puolestaan  kuljetaan prototyyppiketjua 
pitkin kysymään "ylemmältä" oliolta löytyykö kenttä sieltä. Jos ei löydy palautetaan undefined.

<p><b>Olion kenttiin viittaaminen ja läpikäynti</b></p>
Olion kenttänimenä voi käyttää melkein mitä tahansa: tunnus, merkkijono (jopa tyhjä), luku eli  kaikki sellaiset kielen arvot" jotka voi muuttaa merkkijonoksi. Olion kentän tietoihin tietoihin pääsee käsiksi syntaksilla olio.ominaisuus tai vaihtoehtoisesti tietoihin voidaan osoittaa indeksin avulla hakasulkunotaatiolla, jolloin ominaisuuksien arvoja voidaan asettaa dynaamisesti.

```	
 var elain = {nimi: 'Miuku'}
	elain.nimi ; //Miuku
	elain[‘nimi’]:  //Miuku

```

Koska olioden kentät on assosiaatiotaulukoita, olioiden numeroituvia kenttiä voidaan käydä läpi taulukon tavoin for kentta in olio rakenteella. Tällöin mukana tulostuu myös perityt kentät.

```
Object.prototype.lintu = "Peippo";
var elain = {kissa: "Miuku"};
for(var i in elain) {
console.log(i); // tulostaa sekä lintu että kissa }

```
Jos halutaan selvittää pelkästään olion omat kentät yksi tapa on käyttää  Object.prototype-olion hasOwnProperty-metodia. Seuraavassa metodissa tulostuu vain kissa
	
```
Object.prototype.lintu = "Peippo";
var elain = {kissa: "Miuku"};
for(var i in elain) {
if (elain.hasOwnProperty(i)) {
console.log(i); // tulostaa vain kissa }
```
Samaan tyyliin saataisiin seuraavilla selville olion numeroimattomien kenttien kentttämimet käyttämällä funktiota: Object.getOwnPropertyNames(o) 

```
var sekaolio = {eka:1, toka:2, kolmas:3, nelkkku: function(x) {this.toka+=x}};
write(Object.getOwnPropertyNames(sekaolio)); // eka,toka,kolmas,nelkku

```
<p><b>Olion poisto</b></p>
<p>Ainut hyvä tapa olion ominaisuuden poistoon on käyttää delete-operaattoria. Ominaisuuden asettaminen joko arvoon undefined tai null poistaa vain siihen liittyneen arvon muttei itse avainta, kuten seuraavasta esimerkistä käy ilmi.</p>


```
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
```

<p>Ohjelma tulostaa m1 undefined ja m2 null. vain m3 on poistettu Huomaa myös, että oliolion prototyyppiolion kentän tai metodin poisto poistaa kentät kaikilta sen perineiltä olioilta.</p>

<p><b>olion getterit ja setterit</p></b>

<p>JavaScriptistä löytyy valmis kirjastofunktio  Object.defineProperties gettereiden ja settereiden luontiin, mutta niitä voi myös ohjelmoida "käsin"  </p>

# 6
# Protoryypit ja periytyminen

Javascriptissä on olemassa kolmenlaisia olioita: funktio-olioita, niihin liittyviä prototyyppiolioita ja "tavallisia" olioita. Oliot perivät ominaisuuksia prototyyppiolioltaan. Vain funktiolla Funktion, prototyyppi ja prototyyppiolio-olio ovat sama asia.

Prototyyppiperiytyminen perustuu **Object ja Function** olioihin(funktioihin), jotka pitävät sisällään joukon kenttiä, kielen peruskalustoa. Ne molemmat toimivat myös konstruktorifunktioina joiden avulla luodaan uusia olioita ja funktioita.

Kuten alla oleva kuva havainnollistaa kaikki oliot perivät **Object-funktion prototyyppiolion** kentät. Kaikki funktiot puolestaan perivät lisäksi **Function-funktion prototyyppiolion** kentät. 

<img src="https://github.com/vsvala/JavaScript_ohjelmointitekniikka/blob/master/Untitled%20Diagram.jpg" >

### __ proto__-kenttä ja prototyyppiketju

Jokaiselta oliolta löytyy yksi kenttä **__proto__** "minun prototyyppini", jonka osoittaa oman prototyyppiketjun lähimpään prototyyppiolioon.Konstruktorifunktioiden prototyyppiolioista muodostuu linkitettyjä perintäketjuja.

JavaScriptin perintä perustuu siis ´__proto__´ -kenttiin joka viittaa aina perittävään prototyyppiolioon, jonka´__proto__´  -kenttä puolestaan viittaa taas sen prototyyppiolioon. Perintä jatkuu näin muodostuvaa **prototyyppiketjua** ylöspäin aina Function funktion prototyyppikenttään asti, jonka __proto__-kenttä osoittaa null:ia. Normaalisti jokaisen olion prototyyppien ketju päättyykin Object-funktion prototyyppiolioon, jollei sitä erikseen katkaista. 

Luokkametodilla Object.getPrototypeOf(olio) saa selvitettyä mihin prototyyppiolioon __proto__ kenttä viittaa. Toinen tapa selvittää asia a on Käsky  x.__proto__, mutta tämä ei kuitenkaan välttämättä toimi vanhoilla selaimilla, joten on varmempaa käyttää ensimmäistä tapaa.

"Kun olion x kenttään viitataan arvoa hakien, haetaan ensin olion omista kentistä. Jos ei löydy, tutkitaan olion Object.getPrototypeOf(x) kentät. Jos niistäkään ei löydy haettua arvoa, etsitään Object.getPrototypeOf(Object.getPrototypeOf(x)), jne. Näin edetään Object.prototype-kentän osoittamaan olioon eli Object-funktion prototyyppiolioon saakka, mihin ketju päättyy: Object.getPrototypeOf(Object.prototype)===null. Tällöin palautetaan arvo undefined.

### Prototyyppiperinnän käyttö copy-paste -koodin välttämiseksi
Perinnän avulla voidaan poistaa turhaa koodin kopioimista. Konstruktorifunktion prototyyppiolioon voidaan liittää ominaisuuksia, jotka kaikki kyseisellä funktiolla konstruoidut oliot jakavat keskenään.Jos konstruktorin avulla olioita tehtaillessa olioilla on samoja funktioita tai ominaisuuksia, olisikin parempi ohjelmointityyli liittää yhteiset ominaisuudet prototyyppiolioon kaikkien perittäväksi, jotta vältytään koodin toisteisuudelta. Esimerkissä noora ja virva perivät molemmat asuinmaakseen Suomen.

```
function Henkilo(nimi, ika) { this.nimi = nimi; this.ika = ika; }

noora = new Henkilo("Noora", 35);
virva = new Henkilo("Virva", 5);

Henkilo.prototype.opiskelupaikka = "Helsingin yliopisto"
Henkilo.prototype.asuinmaa = "Suomi"

console.log(noora.opiskelupaikka); //Helsingin yliopisto
console.log(virva.opiskelupaikka); //Helsingin yliopisto
console.log(virva.asuinmaa); //Suomi 
console.log(noora.asuinmaa); //Suomi 
```

Pidempiä perimisketjuja voidaan rakentaa korvaamalla olion prototyyppiolioita uudella oliolla seuraavasti. 
Funktioiden prototyyppiolioihin voidaan liittää kenttien lisäksi myös aksessorimetodeita, kuten esimerkissä Eläinmelle on lisätty syö aksessorimetodi. Kun peritty aksessori asettaa arvon perittyyn kenttään niin this viittaa silloin perineeseen olioon. Jos arvoa asettaessa perinyt olio ei sisällä perittyä kenttää se luodaan, haettaessa puolestaan etsittäisiin ketjusta.

```
function Elain() {
  this.reviiri = "puisto"
  this.paino = 0;
}
Elain.prototype.asetaPaino =function (maara) {this.paino=maara}
Elain.prototype.syo = function (maara) {this.paino+=maara}

function Lintu() {
  this.siipienVari = "";
  this.lauluAani = "titityy";
}

Lintu.prototype = new Elain()

function Peippo(nimi) {
  this.nimi = nimi;
}
Peippo.prototype = new Lintu()


var sirkku = new Peippo("Sirkku")


sirkku.nimi;          // Sirkku"
sirkku.lauluAani;     //"titityy"
sirkku.siipienVari;   // ""
sirkku.siipienVari = "musta";  //"musta"   
sirkku.asetaPaino(10);  // 0

sirkku.syo(5);  
sirkku.syo(5);              
sirkku.paino;  // 20
sirkku.reviiri; // "puisto"
 
 ```
Tällöin muodostuu alla olevan mukainen perintäketju, missä alimpana luotu Peippo perii itselleen käyttöönsä kaikkien ylempien olioden ominaisuudet ja funktiot. Arvoa sijoitettaessa ei edetä pitkin prototyyppiketjua. Vain arvoa kysyttäessä etsitään tarvittaessa ketjusta.

<img src="https://github.com/vsvala/JavaScript_ohjelmointitekniikka/blob/master/JS3ejpg%20(1).jpg">

Syntynyt ketsu siis  alhaalta lähdettäsessä:

sirkun _proto_ --> Peippo.prototype
Peippo.prototype. -proto_ --> Lintu.prototype
Lintu.prototype._proto_ --> Elain.prototype
Elain.prototype._proto_ --> Object.prototype
Object.prototype.-proto_ -->null

## perintä Object.createn avulla 
JavaScriptin versioon 1.8.5 ja ECMAScriptin 5. editioon on lisätty funktio Object.create, jonka tarkoituksena on kloonata olio suoraan toisesta oliosta. Tämä ei kuitenkaan toimi aina ihan odotetulla tavalla ja saattaa aiheuttaa ongelmia. sen käyttöä emme välttämättä suosittele tai ainakin kannattaa olla sen käytön suhteen varovainen.


# 7
# Suunnittelumalleja

JavaScript-ohjelmalle on tyypillistä suoritusaikainen dynaamisuus eli se että läshes kaikkea voi vauhdissa muuttaa. Tämän seurauksena kielelle on mahdollista kehittää ja onkin kehitetty hyvin erilaisia ohjelmointityylejä ja -tapoja. Verkosta löytyykin paljon erilaisia eri "gurujen" kehittelemiä JavaScript-ohjelmoinnin rakennehahmoja eli suunnittelumalleja ("design pattern") esimerkiksi Ben Cherryn [JavaScript Module Pattern: In-Depth](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html) ja [Addy Osmanin](Learning JavaScript Design Patterns). Alla luennoilla esitelty hivenen muokattu esimerkki Addy Omanin suunnittelumallista Module pattern.

```
var testModule = (function () {
 
  var counter = 0;
 
  return {
 
    incrementCounter: function () {
      return counter++;
    },
 
    resetCounter: function () {
      console.log( "counter value prior to reset: " + counter );
      counter = 0;
    }
  };
 
})();
 
// Käyttö:
 
// Increment our counter
testModule.incrementCounter();
 
// Check the counter value and reset
// Outputs: counter value prior to reset: 1
testModule.resetCounter();


```


## Lähteet:

  <li>https://github.com/zHarrowed/Javascript-ohjelmointitekniikka/wiki/Viikko-2</li>
  <li>https://fi.wikipedia.org/wiki/Tyyppijärjestelmä</li>
  <li>https://fi.wikipedia.org/wiki/JavaScript</li>
  <li>http://www.mit.jyu.fi/opiskelu/seminaarit/ohjelmistotekniikka/funktion/  </li>
 <li> https://fi.wikipedia.org/wiki/Funktionaalinen_ohjelmointi</li>
 <li>https://fi.wikipedia.org/wiki/Imperatiivinen_ohjelmointi</li>
 <li>https://plus.cs.hut.fi/o1/2017/k07/osa05/  </li>
 <li>https://fullstackopen.github.io/osa1/  </li>
 <li>Map -part 2 of Functional Programming in JAvaScript https://www.youtube.com/watch?v=bCqtb-Z5YGQ&list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84&index=2 </li>
 
  <li>https://www.cs.helsinki.fi/u/wikla/OTjs/materiaalia/funktiot/</li>
  <li>https://www.cs.helsinki.fi/u/wikla/OTjs/materiaalia/oliot/</li>
  <li>https://fi.wikipedia.org/wiki/Sulkeuma_(ohjelmointi)</li>
  <li>https://bonsaiden.github.io/JavaScript-Garden/fi/#function.closures</li>
  <li>http://www.mit.jyu.fi/opiskelu/seminaarit/ohjelmistotekniikka/funktion/  </li>
 <li> https://books.google.fi/books?id=DWs-DwAAQBAJ&pg=PA73&lpg=PA73&dq=JavaScript+sulkeuma&source=bl&ots=C5OQuDEQxF&sig=_aMEunKdE_Vhvc8forJOkYlDFWc&hl=fi&sa=X&ved=2ahUKEwi33bzI_t7eAhULiCwKHQl6CEUQ6AEwBnoECAUQAQ#v=onepage&q=JavaScript%20sulkeuma&f=false</li>

 <li>http://ohtekjs.github.io/#olioliteraalitetc</li>




