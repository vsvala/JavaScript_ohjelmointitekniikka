# JavaScript_ohjelmointitekniikka

## Sulkeuma ja sen käyttötavat

Funktio voi saada parametrikseen toisen funktion. Tällöin sulkeumassa funktion parametrin mukana voidaan välittää myös sen muuttujia. Kun funktion sisällä luodaan sisempi funktio, sen näkyvyysalueeseen kuuluvat myös ulomman funktion muuttujat. Eli kun parametrin saanut funktio suorittaa parametrina saamansa funktion, suoritetaan se parametrina annetun funktion määrittelykohdan nimiavaruudessa.

sidotut muuttujat
"Funktion sidotuiksi muuttujiksi kutsutaan funktion muodollisia parametreja sekä funktion sisällä määriteltyjä paikallisia muuttujia. Toisin sanoen muuttujia, joilla on merkitys vain funktion sisällä ja jotka suoritusaikana ovat olemassa vain funktion suorituksen ajan.
vapaat muuttujat
Funktion vapaiksi muuttujiksi kutsutaan sellaisia funktioon sisältymättömiä, mutta funktiossa viitattuja muuttujia, jotka funktiosta näkyvyyssääntöjen sallimana nähdään."(Nämä vielä suoraan lainausta luentomatskusta)

Nimensä "sulkeuma" (closure) saa siitä, kun funktio välitetään parametrina sen käyttämät vapaat muuttujat "suljetaan" mukaan funktion suoritusta varten.


### 1. Sulkeumaan suljetut vapaat muuttujat säilyvät sulkeuman suorituksen jälkeiseen aikaan.
### 2. Sulkeumaan suljetuttujen vapaiden muuttujien määritellyt funktio päättyy, mutta sulkeuma säilyy

function sulkeumaEsimerkki() {
  var a = "sul", b = "keuma";
  return function() { return a + b };
}
 
Kyseinen funktio palauttaa toisen funktion, joka näkee ulomman funkpalauttaa arvon "sulkeuma", vaikka ulkoisen funktion suoritus onkin päättynyt.


## Oliot ja niiden käyttäytyminen: Olioiden käytön hyviä (ja jos mahdollista turvallisia) ohjelmointityylejä ja -malleja.
Olion luominen
  
Lähteet:  
  
https://fi.wikipedia.org/wiki/Sulkeuma_(ohjelmointi)
https://www.cs.helsinki.fi/u/wikla/OTjs/materiaalia/funktiot/
