## x)

Karvinen 2026: https://terokarvinen.com/apache-ansible/

-  Ansiblella voidaan asentaa Apache2-verkkopalvelin automaattisesti ilman manuaalista asennusta.
- Apache käyttää package-file-service-mallia, jossa ensin asennetaan paketti, sitten määritetään asetustiedostot ja lopuksi käynnistetään palvelu.
- Ansible-rooli sisältää tehtävät (tasks), asetustiedostot (files) ja palvelun uudelleenkäynnistyksen hoitavat käsittelijät (handlers).
- Apache tarjoaa verkkosivun osoitteessa http://localhost, ja sivuston sisältöä voidaan muokata tavallisena käyttäjänä ilman root- tai sudo-oikeuksia.
- Asetustiedostojen muutokset aktivoidaan notify- ja handler-toimintojen avulla, jotka käynnistävät Apache-palvelun uudelleen.

Huomio: Sivuston tiedostojen muokkaaminen onnistuu ilman pääkäyttäjän oikeuksia, mutta Apachen asennus ja palvelimen asetusten muuttaminen vaativat edelleen pääkäyttäjän oikeudet.

Ansible Community Documentation: https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html

- Ansible Handlerit ovat tehtäviä, jotka suoritetaan vain silloin, kun jokin toinen tehtävä ilmoittaa muutoksesta notify-komennolla.
- Niitä käytetään esimerkiksi palveluiden uudelleenkäynnistämiseen silloin, kun niiden asetustiedostoja on muutettu.
- Handler suoritetaan oletuksena vasta playbookin tehtävien valmistuttua, eikä samaa handleria suoriteta useita kertoja saman suoritusvaiheen aikana.
- Yksi tehtävä voi ilmoittaa usealle handlerille, ja handlerit suoritetaan siinä järjestyksessä, jossa ne on määritelty.
- listen-toiminnolla voidaan yhdistää useita handlereita saman ilmoituksen alle.
- meta: flush_handlers -komennolla voidaan pakottaa ilmoitetut handlerit suoritettaviksi jo ennen kaikkien tehtävien valmistumista.
- Handlereissa voidaan käyttää muuttujia esimerkiksi määrittämään, mikä palvelu käynnistetään uudelleen.
  
Huomio: Handlereiden avulla vältetään turhat palveluiden uudelleenkäynnistykset, mikä tekee Ansible-ajosta tehokkaamman ja vähentää tarpeettomia käyttökatkoja.

ansible-doc service on terminaalissa käytettävä komento, jolla voidaan lukea Ansible-palvelumoduulin ohjeita suoraan komentoriviltä.
- Service-moduulilla hallitaan etäkoneiden palveluita, kuten Apachen käynnistämistä ja pysäyttämistä.
- enabled: Määrittää, käynnistyykö palvelu automaattisesti tietokoneen käynnistyessä (yes tai no).
- name: Määrittää hallittavan palvelun nimen, esimerkiksi apache2.
- state: Määrittää palvelun halutun tilan:
  - started = käynnissä
  - stopped = pysäytetty
  - restarted = käynnistetään uudelleen
  - reloaded = ladataan asetukset uudelleen.

huomio: enabled ja state tarkoittavat eri asioita: enabled määrittää automaattisen käynnistymisen tietokoneen käynnistyessä, kun taas state määrittää palvelun tämänhetkisen tilan.

## y)  

It Will Never Be the Year of the Linux Desktop: https://news.ycombinator.com/item?id=48323920&utm_source=chatgpt.com

- Artikkeli käsittelee sitä, miksi Linux ei ole saavuttanut yhtä suurta suosiota työpöytäkäyttöjärjestelmänä kuin Windows.
- Yksi keskeinen syy on yritysten tarve hallita tietokoneita ja käyttäjiä keskitetysti. Windowsissa tämä onnistuu esimerkiksi Active Directoryn ja Group Policyn avulla.
- Keskitetyn hallinnan avulla ylläpitäjä voi helposti lisätä ja poistaa käyttäjiä, hallita tietokoneita sekä määrittää yhteisiä asetuksia.
- Linuxissa vastaava hallinta vaatii usein useiden eri työkalujen yhdistämistä. Esimerkiksi Ansiblella voidaan automatisoida tietokoneiden asetuksia ja ohjelmistojen asennuksia.
- Keskustelussa mainitaan myös LDAP ja FreeIPA, joita voidaan käyttää käyttäjien ja käyttöoikeuksien hallintaan.
- Mielenkiintoinen huomio on, että Linuxin hallinta voi olla jopa Windowsia tehokkaampaa suurissa ympäristöissä, kun automatisointi ja komentorivityökalut ovat kunnossa.
- Toisaalta Linuxin eri jakelut ja työkalut tekevät keskitetystä hallinnasta joskus hajanaisempaa.
  

## a)

<img width="1094" height="476" alt="image" src="https://github.com/user-attachments/assets/6a14a7aa-083a-481e-b280-6664c2bee88a" />

<img width="1132" height="548" alt="image" src="https://github.com/user-attachments/assets/54923e7a-2c55-4b84-b059-c1a65791dcf1" />

<img width="1582" height="1016" alt="image" src="https://github.com/user-attachments/assets/5a079a47-972d-4f41-b442-19c11deeab5d" />

<img width="1176" height="940" alt="image" src="https://github.com/user-attachments/assets/0bc9e6f3-62fb-4b32-9591-7e1078b64cf3" />

<img width="1898" height="312" alt="image" src="https://github.com/user-attachments/assets/be265acd-37b0-4b72-b064-7f5cec32f7bc" />

<img width="1238" height="692" alt="image" src="https://github.com/user-attachments/assets/e420a17b-57ec-4fcb-b907-212f50cd2230" />



## b)

Sammutin Apachen: 

<img width="869" height="190" alt="Näyttökuva 2026-11-17 kello 11 34 28" src="https://github.com/user-attachments/assets/8bc5f3b3-ef56-4ddd-9ab8-6f9d5ebec57b" />

Nginx asennus: 

<img width="596" height="210" alt="Näyttökuva 2026-11-17 kello 11 37 06" src="https://github.com/user-attachments/assets/040937a6-2487-46ab-beaf-173a7c982c24" />

<img width="650" height="84" alt="Näyttökuva 2026-11-17 kello 11 37 41" src="https://github.com/user-attachments/assets/47f2dade-b80f-4214-9bc6-f0116610fd09" />

<img width="494" height="205" alt="Näyttökuva 2026-11-17 kello 11 47 15" src="https://github.com/user-attachments/assets/fb17b6b8-2a3a-4619-9a8a-d6e0e6989e53" />

Muokkasin tekstiä normi käyttäjänä, muutokset näkyy heti verkkosivulla ilman Nginxin uudelleenkäynnistystä.:

<img width="545" height="176" alt="Näyttökuva 2026-11-17 kello 11 49 00" src="https://github.com/user-attachments/assets/d8e0f8f6-ba04-45a7-8abb-2e9ed777351d" />


## c) 

- Loin projektihakemiston: mkdir ~/ansible-nginx
  
 <img width="441" height="43" alt="Näyttökuva 2026-11-17 kello 11 58 44" src="https://github.com/user-attachments/assets/a7649374-39d5-4999-9774-d67ca0333e6a" />

- inventaariotiedosto:

 <img width="336" height="79" alt="Näyttökuva 2026-11-17 kello 12 01 27" src="https://github.com/user-attachments/assets/08903f60-f707-403d-9213-c55295c22180" />


- Nginxin asennus ja palvelun käynnissäolon varmistaminen automatisoitu playbookilla.

<img width="1034" height="517" alt="Näyttökuva 2026-11-17 kello 12 08 06" src="https://github.com/user-attachments/assets/d5cc1bb3-f5db-4aa0-a0ab-9efa56eb0b9d" />
