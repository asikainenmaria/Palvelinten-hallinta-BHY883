x)
## Karvinen 2026: Sudo without password https://terokarvinen.com/passwordless-sudo/
- Ansible tarvitsee kohdekoneella (slave) pääkäyttäjän eli root-oikeudet.
- Tämä voidaan toteuttaa sallimalla sudo-komentojen suorittaminen ilman salasanan kysymistä.
- Luodaan uusi käyttäjä: Luodaan käyttäjä nimeltä (nimi), jolle annetaan tarvittavat oikeudet.
- Luodaan käyttäjäryhmä: Luodaan ryhmä nimeltä sudoless ja lisätään käyttäjä (nimi) tähän ryhmään.
- Varmistetaan sudo-oikeuksien palautus: Avataan erillinen pääkäyttäjän istunto (sudo -i), jotta mahdolliset virheet sudo-asetuksissa voidaan korjata.
- Määritetään salasanaton sudo: Muokataan sudoers-asetuksia komennolla visudo. Lisätään sääntö, joka sallii sudoless-ryhmän jäsenille kaikkien komentojen suorittamisen ilman salasanaa.
- Huomio! Testataan asetukset: Tarkistetaan, että käyttäjä pystyy suorittamaan sudo-komentoja ilman salasanan kysymistä.

1. Luodaan käyttäjä
sudo adduser antero
2. Luodaan ryhmä
sudo groupadd sudoless
3. Lisätään käyttäjä ryhmään
sudo adduser antero sudoless
4. Avataan root-istunto varmuuden vuoksi
sudo -i
5. Muokataan sudoers-tiedostoa (toisessa terminaalissa)
sudo visudo -f /etc/sudoers.d/sudoless
6. Lisätään tiedostoon seuraava rivi:
%sudoless ALL = (ALL) NOPASSWD: ALL
7. Tarkistetaan sudoers-asetukset
sudo visudo -c
8. Testataan käyttäjän oikeudet
sudo -l -U antero
9. Testataan salasanaton sudo
sudo -iu antero
sudo -n whoami

## Karvinen 2026: Passwordless Sudo with Ansible https://terokarvinen.com/passwordless-sudo-with-ansible/

Salasanaton sudo Ansiblella

Salasanattoman sudo-oikeuden luominen Ansiblella:

Ansible-rooli tekee automaattisesti kolme asiaa:
1. Luo käyttäjän antero ja ryhmän sudoless.
2. Lisää käyttäjän ryhmiin sudoless, sudo ja adm sekä asettaa SSH-avaimen kirjautumista varten.
3. Luo sudoers-tiedoston, joka sallii sudoless-ryhmälle salasanattoman sudon.

- Ansible luo käyttäjän ja tarvittavat ryhmät.
- SSH-avain lisätään käyttäjälle.
- Sudoers-sääntö luodaan automaattisesti.
- Käyttäjä voi suorittaa sudo-komentoja ilman salasanan kysymistä.

- Huomio! Testaa asetukset ensin manuaalisesti ja automatisoi vasta sen jälkeen.
Tätä kutsutaan periaatteeksi Manual before auto.

a) 

- Tein Ansiblella sudoless-nimisen käyttäjäryhmän ja määritin sille oikeuden käyttää sudoa ilman salasanan kysymistä.

- Loin määrityksen tiedostoon /etc/sudoers.d/sudoless. Tiedostossa on seuraava määritys:
%sudoless ALL = (ALL) NOPASSWD: ALL

- Tämä tarkoittaa, että kaikki sudoless-ryhmään kuuluvat käyttäjät voivat suorittaa komentoja pääkäyttäjän oikeuksilla ilman salasanan kirjoittamista.

- Lisäksi määritin SSH-avaimen, jotta Ansible pystyy kirjautumaan palvelimelle automaattisesti ilman salasanan kysymistä.

- Testasin toiminnan komennolla:
sudo -n whoami

Tulokseksi tuli root, joten salasanaton sudo toimii.

b) 

-Loin Ansiblella käyttäjän nimeltä antero.

- Lisäsin käyttäjän ryhmiin sudoless, sudo ja adm. Määritin käyttäjälle myös kotihakemiston ja Bash-komentotulkin.

- Lisäsin käyttäjälle SSH-julkisen avaimen Ansible-moduulilla ansible.posix.authorized_key.

- Tämän ansiosta Ansible pystyy kirjautumaan palvelimelle SSH:n avulla ilman salasanan kirjoittamista.

- Testasin yhteyden ja varmistin, että käyttäjä pystyy myös käyttämään sudoa ilman salasanaa.

<img width="1080" height="430" alt="image" src="https://github.com/user-attachments/assets/ebe93f35-38bc-4e22-9524-784337b05976" />

c) 
- Käytin tähän Ansible-moduulia ansible.builtin.apt.
- tree näyttää hakemistojen ja tiedostojen rakenteen puumaisessa muodossa.
- curl on komentorivityökalu, jolla voidaan hakea tietoa verkkopalvelimilta.
-Käytin määrityksessä asetusta state: present, joka varmistaa, että paketit ovat asennettuina.

-Lisäksi käytin asetusta update_cache: true, joka päivittää pakettivarastojen tiedot ennen asennusta.

<img width="1232" height="920" alt="image" src="https://github.com/user-attachments/assets/c74bd808-fab6-4192-82bd-c05a702bd5b0" />


d) 
- Loin Ansiblella tiedoston /home/antero/harjoitus.txt.
- Tiedostoon kirjoitettiin useampi tekstirivi. Määritin tiedostolle myös omistajan, omistavan ryhmän ja käyttöoikeudet.

- Käytin seuraavia määrityksiä:
- owner: antero
- group: antero
- mode: '0640'

-Tiedoston omistajaksi määritettiin antero ja omistavaksi ryhmäksi antero.
- Käyttöoikeuksien oktaaliluku on 0640, jonka symbolinen muoto on:
-rw-r-----

- Oikeuksien merkitys:
- Omistaja (rw-): saa lukea ja muokata tiedostoa.
- Ryhmä (r--): saa lukea tiedostoa, mutta ei muokata sitä.
- Muut käyttäjät (---): eivät saa lukea tai muokata tiedostoa.
- Tarkistin tiedoston oikeudet komennolla:
sudo ls -l /home/antero/harjoitus.txt

<img width="1266" height="374" alt="image" src="https://github.com/user-attachments/assets/6d60ed2f-3e76-476d-88ce-017cef13c9b8" />


e) 

- käytin ansible.builtin.group-moduulia sudoless-ryhmän luomiseen. (tein tämän kohdan kokonaan tekoälyn avulla https://chatgpt.com/)

- name: Create sudoless group
  ansible.builtin.group:
    name: sudoless
    state: present

- name määrittää ryhmän nimen ja state: present varmistaa, että ryhmä on olemassa.
