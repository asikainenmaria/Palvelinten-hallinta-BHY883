# x) Karvinen 2026: SSH public key - Login without password https://terokarvinen.com/ssh-public-key-login-without-password/
- SSH (Secure Shell) on johtava ratkaisu palvelimille kirjautumiseen turvallisesti.
- Monet ohjelmistot käyttävät SSH:ta taustalla, esim- Git, rsync ja Ansible.
- Julkiseen avaimeen perustuva tunnistautuminen on kätevää, koska ei tarvitse kirjoittaa
salasanaa oikein jokaisen git push- tai ansible-playbook -komennon yhteydessä.

# - SSH:n asentaminen - 
- "sudo apt-get update"
- "sudo apt-get -y install ssh"
- Määritä SSH-palvelu käynnistymään automaattisesti tietokoneen käynnistyessä (enable) ja käynnistä se samalla heti (--now):
"sudo systemctl enable --now ssh".
  
- SSH-yhteyden testaaminen: 
"ssh localhost"
- Komennolla "w" näkee, että on kirjautunut sisään kahdesti, työpöydän ja SSH-yhteyden kautta.
- Poistuminen SSH-istunnosta: "remote$ exit"
- Voit kirjautua SSH-julkisella avaimella (Jos julkista avainta ei ole luotu, komento "ssh-keygen".
- muita komentoja: "head $HOME/.ssh/id_*.pub" , "ssh-copy-id localhost"
- Jatkossa SSH käyttää julkista avainta automaattisesti: "ssh localhost"

- Hyödyllisiä komentoja ongelmatilanteiden selvittämiseen: "ssh -v localhost", "sudo journalctl --follow", 
"sudo systemctl status ssh".

# Karvinen 2026: Hello Ansible https://terokarvinen.com/hello-ansible/

- Asenna Ansible = "sudo apt-get update", "sudo apt-get install ansible micro bash-completion tree"
- Testaa SSH "ssh localhost"
- Luo Ansible-kansio = "cd", "mkdir ansible", "cd ansible"
- Luo hosts.ini = "micro hosts.ini", kirjoita tiedostoon "localhost [all:vars]
ansible_python_interpreter=/usr/bin/python3"
- Tallenna Control + S ja sulje Control + Q.
- Testataan ansible = "ansible all -a 'uptime' -i hosts.ini", jos saat tulokseksi koneesi käyttöajan, testi onnistui.
- Luo ansible.cfg = "micro ansible.cfg" ja kirjoita "[defaults]
inventory = hosts.ini
display_args_to_stdout = true",
- tallenna ja sulje.
- Luo site.yml = "micro site.yml", ja kirjoita "- hosts: all
  roles:
    - hello"
- Luo Hello-rooli = mkdir -p roles/hello/tasks/
- Avaa tiedosto micro roles/hello/tasks/main.yml
- Kirjoita "- copy:
    dest: /tmp/hello-ansible
    content: "See you at TeroKarvinen.com!\n""
- Suorita Ansible = ansible-playbook site.yml, jos kaikki toimii, näet esim.
"localhost : ok=2 changed=1 unreachable=0 failed=0"
- Tarkista luotu tiedosto, oikea tulos on "See you at TeroKarvinen.com!"
- <img width="766" height="314" alt="image" src="https://github.com/user-attachments/assets/2f04d408-c782-4fd5-979b-f6eaed71a37f" />



a) https://github.com/asikainenmaria/Palvelinten-hallinta-BHY883/blob/6f19d99a718e5dba9f9c30fe1170e5af76a607dd/h0-oikeasti-netiss%C3%A4.md

# b)

Asensin SSH:n ja määritin sen niin, että se avautuu automaattisesti tietokoneen käynnistyessä.
-"sudo apt-get update"
-"sudo apt-get -y install ssh"
-"sudo systemctl enable --now ssh"
Testasin SSH-yhteyttä komennolla "ssh localhost".

<img width="636" height="178" alt="Näyttökuva 2026-11-03 kello 14 23 39" src="https://github.com/user-attachments/assets/5544d3d4-177b-4c52-9d4f-e177c009e8e4" />
<img width="636" height="156" alt="Näyttökuva 2026-11-03 kello 14 24 23" src="https://github.com/user-attachments/assets/49c59943-f547-43db-b1b8-9fc63d5b74a8" />
<img width="638" height="102" alt="Näyttökuva 2026-11-03 kello 14 25 22" src="https://github.com/user-attachments/assets/10c23463-a100-4322-87ba-d2b8e08916ac" />
<img width="633" height="440" alt="Näyttökuva 2026-11-03 kello 14 20 10" src="https://github.com/user-attachments/assets/9645e806-4d01-408e-a085-fc64557b75c8" />

# c)
Automatisoin public keyn käytön SSH localhostilla, niin en ei tarvitse käyttää salasanaa jatkossa. "ssh-copy-id localhost"
<img width="1140" height="334" alt="image" src="https://github.com/user-attachments/assets/4496b5ae-e08f-49d4-bbbc-19c34ea7b853" />

# d) 
- Tein tehtävän Tero Karvisen ohjeiden mukaan https://terokarvinen.com/hello-ansible/
- Asensin Ansiblen ja loin sinne kansioita ja käyttäjiä.
- En liittänyt tähän mukaan kaikkia kuvia ja vaiheita koska niitä oli niin paljon, mutta kohdassa x) tiivistin työvaiheet.
- 
<img width="1146" height="336" alt="image" src="https://github.com/user-attachments/assets/4af9d215-dde2-4455-97b3-e7ef19c96b72" />

<img width="848" height="214" alt="image" src="https://github.com/user-attachments/assets/32c80ed0-e642-4d4f-8699-432603d01a2e" />

<img width="1148" height="272" alt="image" src="https://github.com/user-attachments/assets/50ea0811-bca9-4ba8-9382-db91743ac144" />

<img width="1110" height="402" alt="image" src="https://github.com/user-attachments/assets/846b696e-6d8d-432e-9b46-d5f59d07ec4b" />

<img width="1122" height="330" alt="image" src="https://github.com/user-attachments/assets/ecf268d6-7560-4201-8bf9-8e9f901cba24" />

<img width="1144" height="452" alt="image" src="https://github.com/user-attachments/assets/e1246f00-0cd0-4056-bbb3-dcb33e2828b2" />

<img width="1018" height="98" alt="image" src="https://github.com/user-attachments/assets/41520062-79cb-48b1-9cd6-c87bb3c0c302" />

<img width="1126" height="512" alt="image" src="https://github.com/user-attachments/assets/5c2ea4c4-4110-4b70-ae33-36030c3527fa" />












