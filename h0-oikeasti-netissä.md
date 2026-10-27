# h0 Oikeasti netissä

x) lue ja tiivistä

- Artikkelissa "Teoriasta käytäntöön pilvipalvelimen avulla (h4)" käsiteltiin virtuaalipalvelimen vuokraamista UpCloudista ja serverin pystytystä, virtuaalipalvelimen asennusta sekä konfigurointia. (Huomio: suositaan suomalaista palveluntarjoajaa UpCloud)
- Virtuaalipalvelimeen saa yhteyden SSH-yhteydellä. (Huomiona: etäyhteyden saa luotua komennolla ssh root@195.12.12.12, eli root + @ + virtuaalipalvelimen IP-osoite)
- Artikkelissa kerrotaan sudo-käyttäjän luomisesta ja palomuurin aktivoimisesta virtuaalipalvelimeen. (Huomio: apt-get update ja sitten apt-get install ufw. Kun palomuuri on asennettu siihen täytyy tehdä reikä / avata portti ennen aktivointia. Komennolla ufw allow 22/tcp päästetään portin 22 liikenne läpi. Aktivoidaan palomuuri komennolla ufw enable.)

  Partanen 2025: Harjoitus 5: Nimekäs a) Nimi
  
- Julkisen domain nimen hankkiminen Namecheapin avulla:
- Etsittiin halvin mahdollinen domain
- Kassalta lisäksi domain privacy suojaus päälle ilmaiseksi
- Rekisteröinti, nimen ja osoitteen lisääminen, kortin tiedot
- Laitetaan osoite osoittamaan omaan virtuaalipalvelimeen (Huomio: "Namecheapin Domain List näkymästä valitaan (nimi).space ja Advanced DNS.
- HOST RECORDS osiossa nähdään että siinä on turha CNAME tietue. Poistan sen ja lisään oman A Record kohdan, joka osoittaa virtuaalipalvelimelle.
- Host kohtaan laitetaan www, joka tarkoittaa www.(nimi).space osoitetta. @ host taas tarkoittaa pelkkää domain osoitetta, tässä tapauksessa (nimi).space.
- TTL ajaksi laitan 5 minuuttia, jotta muutokset näkyvät nopeasti.")

a) Asenna Debian 13 paikallisesti virtuaalikoneeseen - Tein virtuaalipalvelimen käyttäen Debian GNU/Linux 13 (Trixie)
b) Olen vuokrannut virtuaalipalvelimen UpCloudista
c) Loin sudokäyttäjän nimellä maria. Kirjauduin virtuaalipalvelimelle SSH-yhteydellä root-käyttäjänä. Tämän jälkeen loin itselleni tavallisen käyttäjän komennolla:
- adduser oma_nimi
- Lisäsin käyttäjän sudo-ryhmään komennolla:
- usermod -aG sudo oma_nimi
- Tarkistin käyttäjän kirjautumisen ja sudo-oikeudet komennoilla whoami ja sudo whoami. Jälkimmäinen tulosti root, joten sudo-oikeudet toimivat. kai :')

Asensin palomuurin:
-sudo apt update
-sudo apt install ufw
Sallin SSH-yhteydet ennen käyttöönottoa:
-sudo ufw allow OpenSSH
Otin palomuurin käyttöön ja tarkistin sen tilan:
-sudo ufw enable
-sudo ufw status

d) Asensin Apachen:
-sudo apt update
-sudo apt install apache2
Sallin HTTP-liikenteen palomuurissa:
-sudo ufw allow 80/tcp
Testasin:
-sudo systemctl status apache2
-sudo systemctl enable apache2
<img width="1154" height="728" alt="image" src="https://github.com/user-attachments/assets/14cbb876-0a1b-4102-8e51-3f96e032427a" />


Testasin web-palvelinta selaimesa avaamalla osoitteen http://87.58.151.93.
Kun sivu näkyi selaimessa, pystyin varmistamaan, että palvelin vastasi verkkopyyntöihin.

<img width="2560" height="1664" alt="image" src="https://github.com/user-attachments/assets/26772f27-cee8-4664-9b4a-2e0381440c50" />



