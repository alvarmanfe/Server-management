## **h2 - Voileipä**


## **x)** Karvinen 2026: Sudo without password
- Ansible needs root on the slave. One way is to allow 'sudo' without password.
- Create a new user. Use only strong passwords.
- Add to a new *sudoless* group and add users needing automation privileges, without using .
- Add sudoers rule ```%sudoless ALL=(ALL) NOPASSWD: ALL.```
- Use /etc/sudoers.d/ and visudo to avoid syntax errors.
- New group rights update after a restart or a new login.
- Used mainly for automation tools like Ansible.

## Karvinen 2026: Passwordless Sudo with Ansible
- Ansible automation requires privilege escalation without manual passwords.
- Passwordless sudo enables fully automated provisioning.
- SSH + sudo configuration are core prerequisites.
- Focus on repeatable infrastructure setup.

## **a)** Sudoless
Tässä tehtävässä: 
- Ensimmäiseksi loin sudolla uuden käyttäjän, jonka nimesin "anseba" ja johon loin myös vahvan salasanan.
- Sitten loin uuden *sudoless* ryhmän ja lisäsin juuri luomani käyttäjän ryhmään.
  ```
  sudo adduser anseba sudoless
  ```
  ![Sieppaa](https://github.com/user-attachments/assets/f41ac65a-d388-475f-9cd8-be44eab78e57)
  
- Avattiin uusi terminaali johon kirjauduttiin omalla sudo käyttäjällä ja ajettiin komento ```sudo -i```. Tämä toimii pelasturenkaana siltä varalta, että jos sudo menee rikki voidaan korjata se rootin avulla.
![Sieppaa1](https://github.com/user-attachments/assets/0035c7cb-9d69-4991-bd1a-3f8e75f289f7)
Siksi jätetään tämä ikkuna hetkeksi auki ja jatketaan työskentelyä edellisessä ikkunassa, jossa puolestaan avataan sudoers turvallisesti (tämä edellyttää aina visudo:n käyttöä). Lisätään rivi: ```%sudoless ALL=(ALL) NOPASSWD: ALL``` -> tallenna ja sulje.
  %sudoless -> kokee ryhmää
  ALL       -> kaikki koneet
  (ALL)     -> voi vaihtua mihin käyttäjään tahansa
  NOPASSWD  -> ei kysy salasanaa
  ALL       -> kaikki komennot on sallittu

  Nyt sudon pitäisi olla salasanaton.

  Tarkistetaan vielä kirjautumalla uudestaan uudelle käyttäjälle ```anseba@localhost```.
  Tyhjennetään sudon muistama aiempi kirjautuminen komennolla ```sudo -k``` jotta voidaan     
  testata onko käyttäjä nyt oikeasti salasanaton.
  Ajetaan testi ansebana: ```sudo echo "See you at TeroKarvinen.com"``` ja tuloksena saadaan *See you at TeroKarvinen.com*. Harjoitus onnistui sillä salasanaa ei kysytty.
  
  ![Sieppaa2](https://github.com/user-attachments/assets/7d989ba1-0a96-4d46-a889-dad331305f95)

## **b)** Antero



