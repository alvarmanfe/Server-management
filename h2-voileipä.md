## **h2 - Voileipä**


## **x)** Karvinen 2026: Sudo without password
- Ansible tarvitsee pääkäyttäjän (root) oikeudet hallittavalla koneella. Yksi tapa mahdollistaa tämä on sallia sudo-komennon käyttö ilman salasanaa.
- Luo uusi käyttäjä. Käytä ainoastaan vahvoja salasanoja.
- Luo uusi sudoless-käyttäjäryhmä ja lisää siihen käyttäjät, joille halutaan antaa automaatioon tarvittavat oikeudet.
- Lisää sudoers-sääntö: %sudoless ALL=(ALL) NOPASSWD: ALL.
- Käytä /etc/sudoers.d/-hakemistoa ja visudo-komentoa välttääksesi määritysten syntaksivirheet.
- Uuden käyttäjäryhmän oikeudet tulevat voimaan kirjautumalla uudelleen sisään tai käynnistämällä kone uudelleen.
- Käytetään pääasiassa automaatiotyökalujen, kuten Ansible, kanssa.

## Munroe 2006 : Sandwich
<img width="457" height="381" alt="Näyttökuva 2026-11-04 170337" src="https://github.com/user-attachments/assets/728b08b8-a577-4bd1-97a6-40273273c5ab" />


Tämä hassunhauska sarjakuva kertoo ```sudo``` (_superuser do_) komennon tärkeydestä. Sarjakuvassa vasen ukkeli (_eli käyttäjä_) pyytää tekemään voileivän ensiksi ilman _sudo_-komentoa, jolloin toinen ukkeli (_eli kone_) ei suostu tekemään meille sämpylää. Tämän jälkeen käyttäjä pyytää suorittamaan saman _sudolla_ jolloin kone vihdoinkin suostuu. Tämä on tärkeä muistutus siitä, että ilman sudoa meillä ei ole riittäviä käyttäjäoikeuksia tiettyjen komentojen suorittamiseen. Sudon avulla tavallinen käyttäjä voi suorittaa komentoja pääkäyttäjän eli root-käyttäjän oikeuksilla.


## Karvinen 2026: Passwordless Sudo with Ansible
- Ansible-automaatio edellyttää oikeuksien korottamista ilman manuaalista salasanan syöttämistä.
- Salasanaton sudo mahdollistaa täysin automatisoidun palvelimien käyttöönoton ja määrityksen.
- SSH-yhteyden ja sudo-oikeuksien määrittäminen ovat automaation keskeisiä perusedellytyksiä.
- Tavoitteena on toistettavissa oleva ja yhdenmukainen infrastruktuurin käyttöönotto.

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

## **b)** Antero (Anseba)

Tarkistetaan ensiksi, miltä Ansible-hakemistoni näyttää:

<img width="623" height="227" alt="Näyttökuva 2026-11-05 154101" src="https://github.com/user-attachments/assets/c300d8c2-3230-412b-9ee6-3e5205b937a3" />

- Tarkistetaan oma ssh ```ls ~/.ssh/``` ja kopioidaan se.
- Lisäsin polkuun _/roles/anseba/tasks_ tiedoston _main.yml_, jota muokkasin mikrolla (```micro roles/anseba/tasks/main.yml```) Teron sivulla olevilla ohjeilla ja liitin oikeaan kenttäkohtaan oman ssh-avaimeni.

<img width="1190" height="385" alt="Näyttökuva 2026-11-05 153925" src="https://github.com/user-attachments/assets/a504781b-831c-4206-b355-5bfd021a33d1" />



- Muokkasin site.yml tiedostoa määrittelemällä ```become:true``` _hosts:in_ perään ja lisäsin roolin ```anseba```.

<img width="390" height="129" alt="Näyttökuva 2026-11-05 154455" src="https://github.com/user-attachments/assets/10d31d0e-020d-48f0-ba50-70f6b7519544" />

- Ajoin ```ansible-playbook site.yml```. Nyt valittaa, että sudo tarvitsee salasanaa.
- Sitten ```ansible-playbook site.yml -K``` -K on sama kuin ```--ask-become-password```, eli kysyy käyttäjäni sudo-salasanan.

<img width="1190" height="657" alt="Näyttökuva 2026-11-05 160128" src="https://github.com/user-attachments/assets/9b0cbab1-f303-4578-8dde-94d8476c06d5" />

- Avasin ```ansible.cgf``` tiedoston ja lisäsin sinne asetuksen ```remote_user = anseba```.

<img width="385" height="117" alt="Näyttökuva 2026-11-05 183309" src="https://github.com/user-attachments/assets/f46a7083-b746-4824-a0b5-1349b824b8aa" />

Nyt voidaan kirjautua koneelle Ansiblen ansiosta anseba käyttäjänä, vaikka ajettaisi komento omalla käyttäjällä. Myöskään ssh-kirjautumiseen ei tarvita enää salasanaa, koska julkinen avaimeni on lisätty anseba käyttäjälle. _Sudoless_ toimii, eikä vaadi salasanaa. Tämä onnistuu siksi, että anseba kuuluu ryhmään _sudoless_.
Koitetaan nyt ajaa pelkkä komento ```ansible-playbook site.yml``` , joka ei puolestaan vaadi enää salasanaa.

<img width="1096" height="486" alt="Näyttökuva 2026-11-05 184156" src="https://github.com/user-attachments/assets/13b18f0d-3cd8-4dd1-882d-79e6161c31d3" />

- Kokeillaan myös kirjautumista ilman salasanaa:

<img width="1049" height="169" alt="Näyttökuva 2026-11-05 170112" src="https://github.com/user-attachments/assets/0d644ac4-1f98-452b-a8b5-6a436d52d113" />

Kirjautuminen onnistuu ssh:lla ilman salasanaa ansiblella käyttäjällä anseba.

Tässä tehtävässä opettelin miten Ansiblella voidaan automatisoida ryhmä palvelimelle kirjautumista ilman käyttäjän salasanan syöttämistä ja pääkäyttäjän oikeuksia vaativien komentojen suorittamisen ilman sudoa.

## **c)**

Asennetaan paketit htop ja tree:

- Lisätään tiedostoon _roles/anseba/tasks/main.yml_ loppuun.

<img width="443" height="153" alt="Näyttökuva 2026-11-05 171730" src="https://github.com/user-attachments/assets/67338a29-b79e-4db3-86f1-04712c3242f7" />

- Sitten ajetaan idempotenssi ```ansible-playboook site.yml```
- Testataan vaikka yhtä näistä paketeista ajamalla ```htop```

<img width="1188" height="660" alt="htop" src="https://github.com/user-attachments/assets/9be27c95-6741-4af0-bff3-b4b874c1ba22" />

Toimii!

## **d)**


## **LÄHTEET**
- Karvinen, T. s.a. Sudo without password. Luettavissa: https://terokarvinen.com/passwordless-sudo/. Luettu: 4.11.2026.
- xkcd. s.a. Sandwich. Luettavissa: https://xkcd.com/149/. Luettu: 4.11.2026.
- Karvinen, T. s.a. Passwordless Sudo with Ansible. Luettavissa: https://terokarvinen.com/passwordless-sudo-with-ansible/. Luettu: 4.11.2026.
