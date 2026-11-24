x) 

## 4.12.1 Size and Complexity of Some DSLs

Konfiguraationhallinnan DSL-kielet (esim. Salt ja Puppet) voivat olla yllättävän suuria ja monimutkaisia.
Saltissa on noin 510 toimintoa (state functions) ja sen dokumentaatio on yli 20 000 riviä, eli laajuudeltaan väitöskirjan kokoinen.
Puppetissa on noin 113 toimintoa, ja lisäksi sillä on omia erityisiä rakenteita, kuten virtual resources.
DSL:t sisältävät usein omia ohjausrakenteita, jotka poikkeavat tavallisista ohjelmointikielistä.
Tutkimusten mukaan DSL-kielten hyötyjä on tutkittu melko vähän, vaikka niiden usein väitetään helpottavan ylläpitoa.

- Oma huomio: Jos DSL:n opetteluun kuluu paljon aikaa, onko sen hyöty aina suurempi kuin tavallisen ohjelmointikielen käyttö?

## 4.12.2 Use of DSL Functions in Case Configuration

Käytännön tuotantoympäristöissä käytetään vain pientä osaa DSL:n kaikista ominaisuuksista.
Yleisimmät Puppet-komennot ovat file, package, service ja exec.
Suurin osa järjestelmien konfiguroinnista perustuu malliin package > file > service.
Ohjausrakenteista yleisimpiä ovat if ja case.
Vaikka työkaluissa on satoja toimintoja, muutama perustoiminto kattaa valtaosan käyttötapauksista.

- Oma huomio: Miksi opetella satoja komentoja, jos käytännössä tarvitsee vain muutamia yleisimpiä?

## 4.12.3.1 Dependencies Between Main Functions
Konfiguraationhallinnan tärkeimmät rakennuspalikat ovat package, file, service, user, group ja exec.
Idempotenssi tarkoittaa, että muutoksia tehdään vain silloin, kun järjestelmän nykytila poikkeaa tavoitetilasta.
Perusfunktiot file ja exec muodostavat pohjan, joiden päälle muut toiminnot voidaan rakentaa.
Esimerkiksi palvelun asennus ja hallinta voidaan toteuttaa yhdistämällä package, file ja service.
Useimmat konfiguraatiot voidaan rakentaa pienestä määrästä yksinkertaisia perustoimintoja.

- Oma kysymys: Voisiko hyvin suunniteltu pieni perustoimintojen joukko korvata suuren määrän monimutkaisia DSL-rakenteita?

a) 

b)

c)

d)

e)

f) tehty 
