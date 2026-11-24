## x) 

4.12.1 Size and Complexity of Some DSLs

Konfiguraationhallinnan DSL-kielet (esim. Salt ja Puppet) voivat olla yllättävän suuria ja monimutkaisia.
Saltissa on noin 510 toimintoa (state functions) ja sen dokumentaatio on yli 20 000 riviä, eli laajuudeltaan väitöskirjan kokoinen.
Puppetissa on noin 113 toimintoa, ja lisäksi sillä on omia erityisiä rakenteita, kuten virtual resources.
DSL:t sisältävät usein omia ohjausrakenteita, jotka poikkeavat tavallisista ohjelmointikielistä.
Tutkimusten mukaan DSL-kielten hyötyjä on tutkittu melko vähän, vaikka niiden usein väitetään helpottavan ylläpitoa.

- Oma huomio: Jos DSL:n opetteluun kuluu paljon aikaa, onko sen hyöty aina suurempi kuin tavallisen ohjelmointikielen käyttö?

4.12.2 Use of DSL Functions in Case Configuration

Käytännön tuotantoympäristöissä käytetään vain pientä osaa DSL:n kaikista ominaisuuksista.
Yleisimmät Puppet-komennot ovat file, package, service ja exec.
Suurin osa järjestelmien konfiguroinnista perustuu malliin package > file > service.
Ohjausrakenteista yleisimpiä ovat if ja case.
Vaikka työkaluissa on satoja toimintoja, muutama perustoiminto kattaa valtaosan käyttötapauksista.

- Oma huomio: Miksi opetella satoja komentoja, jos käytännössä tarvitsee vain muutamia yleisimpiä?

4.12.3.1 Dependencies Between Main Functions
Konfiguraationhallinnan tärkeimmät rakennuspalikat ovat package, file, service, user, group ja exec.
Idempotenssi tarkoittaa, että muutoksia tehdään vain silloin, kun järjestelmän nykytila poikkeaa tavoitetilasta.
Perusfunktiot file ja exec muodostavat pohjan, joiden päälle muut toiminnot voidaan rakentaa.
Esimerkiksi palvelun asennus ja hallinta voidaan toteuttaa yhdistämällä package, file ja service.
Useimmat konfiguraatiot voidaan rakentaa pienestä määrästä yksinkertaisia perustoimintoja.

## a)

Asensin chronyn ja varmistin toiminnan komennoilla systemctl status chrony, chronyc tracking ja chronyc sources.

<img width="612" height="484" alt="Näyttökuva 2026-11-24 kello 12 37 47" src="https://github.com/user-attachments/assets/3ff1736a-4b6a-4489-a55a-c4ca1b046c3d" />


## b)

Automatisoin Chronyn asennuksen Ansiblella luomalla sille oman roolin. Rooli asentaa Chrony-paketin, kopioi asetustiedoston oikeaan sijaintiin sekä varmistaa, että palvelu on käynnissä.

<img width="1062" height="94" alt="image" src="https://github.com/user-attachments/assets/3c5a7664-46d7-4517-9d6f-2dab1e901992" />


Playbook suoritettiin komennolla:

Shell
ansible-playbook -i hosts.ini site.yml -K

Ansible suoritti tehtävät onnistuneesti ilman virheitä.



## c) 

- Loin oman asetustiedoston:

roles/chrony/files/chrony.conf

- ja määritin Ansible-roolin kopioimaan sen tiedostoon:

/etc/chrony/chrony.conf

- Muutin asetustiedostoa lisäämällä uuden asetusrivin ja ajoin playbookin uudelleen. Muutos siirtyi kohdejärjestelmään onnistuneesti, mikä varmistettiin tarkistamalla tiedoston sisältö:

cat /etc/chrony/chrony.conf

<img width="712" height="848" alt="image" src="https://github.com/user-attachments/assets/54f5bb2a-effe-48e7-a5fb-f7952b3a2aec" />

- <img width="1230" height="830" alt="image" src="https://github.com/user-attachments/assets/ccb11344-ba8e-4927-af27-3339f7793c8f" />


## d) 

- Poistin Chrony-palvelun komennolla "sudo apt purge -y chrony". Tämän jälkeen ajoin Ansible-playbookin uudelleen. Ansible asensi puuttuvan palvelun takaisin, palautti asetukset ja käynnisti palvelun. Tämä osoittaa, että määritelty tila korjaa poikkeamat automaattisesti.

  
<img width="1104" height="398" alt="image" src="https://github.com/user-attachments/assets/365ea6ee-8e7d-4748-abd4-cbd03a06c1d8" />



- Rikoin järjestelmän poistamalla Chrony-palvelun:

sudo apt purge -y chrony

- Tämän jälkeen palvelu ei ollut enää käytettävissä. Ajoin Ansible-playbookin uudelleen:

ansible-playbook -i hosts.ini site.yml -K

<img width="1262" height="858" alt="image" src="https://github.com/user-attachments/assets/0a25e65f-42f8-494c-a239-1a9c892923a3" />


- Ansible asensi puuttuvan paketin uudelleen, palautti asetukset ja käynnisti palvelun. Lopuksi tarkistin palvelun tilan komennolla:

systemctl status chrony

- Palvelu oli jälleen käynnissä (active (running)).

## e) 

- Todistin playbookin olevan idempotentti ajamalla sen useita kertoja peräkkäin:

ansible-playbook -i hosts.ini site.yml -K

- Viimeisellä ajokerralla Ansible raportoi:

PLAY RECAP

localhost : ok=5 changed=0 unreachable=0 failed=0

<img width="1218" height="106" alt="image" src="https://github.com/user-attachments/assets/365fcf35-a421-4478-bb97-7021d2f18cc9" />


## f) 

tehty 
