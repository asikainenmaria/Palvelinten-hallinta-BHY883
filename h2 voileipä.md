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
