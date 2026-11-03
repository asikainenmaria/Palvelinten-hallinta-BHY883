x) Karvinen 2026: SSH public key - Login without password https://terokarvinen.com/ssh-public-key-login-without-password/
- SSH (Secure Shell) on johtava ratkaisu palvelimille kirjautumiseen turvallisesti.
- Monet ohjelmistot käyttävät SSH:ta taustalla, esim- Git, rsync ja Ansible.
- Julkiseen avaimeen perustuva tunnistautuminen on kätevää, koska ei tarvitse kirjoittaa
salasanaa oikein jokaisen git push- tai ansible-playbook -komennon yhteydessä.

- SSH:n asentaminen - 
-"sudo apt-get update"
-"sudo apt-get -y install ssh"
-Määritä SSH-palvelu käynnistymään automaattisesti tietokoneen käynnistyessä (enable) ja käynnistä se samalla heti (--now):
"sudo systemctl enable --now ssh".
  
- SSH-yhteyden testaaminen: 
"ssh localhost"
-Komennolla "w" näkee, että on kirjautunut sisään kahdesti, työpöydän ja SSH-yhteyden kautta.
-Poistuminen SSH-istunnosta: "remote$ exit"
-Voit kirjautua SSH-julkisella avaimella (Jos julkista avainta ei ole luotu, komento "ssh-keygen".
-muita komentoja: "head $HOME/.ssh/id_*.pub" , "ssh-copy-id localhost"
-Jatkossa SSH käyttää julkista avainta automaattisesti: "ssh localhost"

-Hyödyllisiä komentoja ongelmatilanteiden selvittämiseen: "ssh -v localhost", "sudo journalctl --follow", 
"sudo systemctl status ssh".

- Karvinen 2026: Hello Ansible https://terokarvinen.com/hello-ansible/

<img width="487" height="123" alt="Näyttökuva 2026-11-03 kello 14 21 12" src="https://github.com/user-attachments/assets/39c4a96d-15af-4d21-b522-c9afcdb24abc" />
<img width="636" height="178" alt="Näyttökuva 2026-11-03 kello 14 23 39" src="https://github.com/user-attachments/assets/5544d3d4-177b-4c52-9d4f-e177c009e8e4" />
<img width="636" height="156" alt="Näyttökuva 2026-11-03 kello 14 24 23" src="https://github.com/user-attachments/assets/49c59943-f547-43db-b1b8-9fc63d5b74a8" />
<img width="638" height="102" alt="Näyttökuva 2026-11-03 kello 14 25 22" src="https://github.com/user-attachments/assets/10c23463-a100-4322-87ba-d2b8e08916ac" />
<img width="633" height="440" alt="Näyttökuva 2026-11-03 kello 14 20 10" src="https://github.com/user-attachments/assets/9645e806-4d01-408e-a085-fc64557b75c8" />







  


a) https://github.com/asikainenmaria/Palvelinten-hallinta-BHY883/blob/6f19d99a718e5dba9f9c30fe1170e5af76a607dd/h0-oikeasti-netiss%C3%A4.md
b)
