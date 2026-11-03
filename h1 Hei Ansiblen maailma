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


  


a) https://github.com/asikainenmaria/Palvelinten-hallinta-BHY883/blob/6f19d99a718e5dba9f9c30fe1170e5af76a607dd/h0-oikeasti-netiss%C3%A4.md
b)
