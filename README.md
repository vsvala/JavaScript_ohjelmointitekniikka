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
Olion luominen
  
Lähteet:  
  
https://fi.wikipedia.org/wiki/Sulkeuma_(ohjelmointi)

https://www.cs.helsinki.fi/u/wikla/OTjs/materiaalia/funktiot/
