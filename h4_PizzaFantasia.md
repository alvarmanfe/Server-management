## **h4 - Pizza Fantasia**

## **x)** Karvinen 2023: Configuration Management of Distributed Systems over Unreliable and Hostile Networks (4.12.1, 4.12.2, 4.12.3.1)

- Salt ja Puppet ovat automaatio- ja konfiguraationhallintatyökaluja, joita käytetään palvelimien hallintaan, ohjelmistojen asentamiseen ja halutun tilan ylläpitämiseen. 
- DSL-kielet (Domain-Specific Language) voivat kasvaa hyvin monimutkaisiksi ja laajoiksi. Kummassakin on paljon toimintoja: Saltissa yli 500 ja Puppetissa yli 100.
- Saltissa ja Puppetissa on siis paljon valmiita toimintoja, mutta käytännössä suurin osa konfiguroinnista onnistuu muutamalla perustoiminnolla, kuten pakettien, tiedostojen ja palveluiden hallinnalla.
- Confteron ideana on tehdä konfiguroinnista yksinkertaisempaa. Pienempi ja selkeämpi kieli olisi helpompi oppia ja käyttää.
- Konfiguroinnissa tärkeää on idempotentti, eli se, että järjestelmä tekee muutoksia vain silloin, kun niille on tarvetta.
- Liian monimutkainen järjestelmä voi tehdä automatisoinnista vaikeampaa, vaikka sen tarkoituksena olisi helpottaa ylläpitäjän työtä.

Mielestäni konfiguroinnissa tärkein on tehdä asioista mahdollisimman selkeitä ja yksinkertaisia. Onko välttämätöntä ja järkevää opetella satoja tai tuhansia eri toimintoja, jos suurimman osan työstä voi tehdä muutamalla perustoiminnolla?

## **a) Räpylä**

- Päivitetään virtuaalikoneen käynnistettyä paketit komennolla ```sudo apt update```.
- Asennetaan omalle Debainille käsin _fail2ban_ demoni, joka suojaa palvelimia automatisoiduilta ja raan voiman hyökkäyksiltä.

<img width="1058" height="598" alt="Näyttökuva 2026-11-18 192447" src="https://github.com/user-attachments/assets/53e6b57d-19c2-40f3-8c49-3622c88504e0" />

- Testatamaan toimiiko palvelu tarkistamalla status ja ping. Saadaan vastaukseksi _enabled_ ja _pong_, eli palvelu on käynnissä ja se vastaa oikein.

- <img width="818" height="288" alt="Näyttökuva 2026-11-18 192929" src="https://github.com/user-attachments/assets/7a39f7bc-9a2a-4294-afc6-a429ac069539" />

## **b) Automaatti**

- Luodaan Ansibleen uudet roolit ja tiedostot:

 <img width="673" height="92" alt="Näyttökuva 2026-11-18 193942" src="https://github.com/user-attachments/assets/befeaea3-b60d-49eb-a797-1b414c289c3e" />

- Muokataan tiedostoa ```roles/fail2ban/tasks/main.yml``` seuraavasti:

  <img width="315" height="174" alt="Näyttökuva 2026-11-18 194641" src="https://github.com/user-attachments/assets/49c9b198-e241-449c-adbf-fe4b60eba743" />

  Ja sitten ```site.yml``` tiedostoa:

  <img width="276" height="152" alt="Näyttökuva 2026-11-18 194839" src="https://github.com/user-attachments/assets/fbfeeffc-790c-4cd3-949d-f155bec179fd" />

- Ajetaan Ansible ja tarkistetaan idempotenssi:

  
  <img width="1253" height="691" alt="Näyttökuva 2026-11-18 195134" src="https://github.com/user-attachments/assets/8028afdc-04de-4a61-8185-c21dca0c335e" />

  <img width="1250" height="59" alt="Näyttökuva 2026-11-18 195201" src="https://github.com/user-attachments/assets/3df4cfb8-31ff-4c87-ac38-bfe10dcfbc07" />

## **c) Asetus**

- Omassa Ansible projektihakemistossa luodaan uusi kansio ```micro roles/fail2ban/files/fail2ban.local```. Tämä tehdää koska tarkoituksena on muuttaa Fail2banin asetuksia niin, että Ansible pystyy hallitsemaan niitä keskitetysti master-koneelta. ```.local```-tiedostojen idea on, että voit tehdä omia muutoksia ilman, että alkuperäisiä asetustiedostoja tarvitsee muokata.
Lisätään sinne:

 <img width="239" height="63" alt="Näyttökuva 2026-11-18 205215" src="https://github.com/user-attachments/assets/89aebfea-069a-455a-bc9b-3c00c4a549a2" />

 - [Definition] määrittää Fail2banin yleiset palvelinasetukset.
 - loglevel määrittää lokituksen tarkkuuden.
 - DEBUG tarkoittaa yksityiskohtaista lokitusta.
- Muokataan seuraavaksi Ansiblen task tiedostoa ```main.yml```. Lisätään apt- ja service- jälkeen:

  <img width="556" height="308" alt="Näyttökuva 2026-11-18 211050" src="https://github.com/user-attachments/assets/fc563151-229f-45cc-8dc1-72d47d696195" />
 Tässä kopioidaan tiedosto Masterilta palvelimelle.

- Muokataan handlereitä ```micro roles/fail2ban/handlers/main.yml```:

  <img width="365" height="102" alt="Näyttökuva 2026-11-18 211505" src="https://github.com/user-attachments/assets/f8c16afd-d5f4-4290-a342-d3a7ee42d7ea" />

 **Muistutuksena** Handleri suoritetaan vain silloin, kun jokin toinen tehtävä ilmoittaa sen tarpeelliseksi. Eli jos ja kun tiedosto on muuttunut niin ```notify``` ilmoittaa tästä handlerille, joka käynnistää Fail2banin uudelleen.
 
- Ajetaan Ansible uudestaan ```ansible-palybook site.yml```
  Saadaan virheilmoitus:
  
  <img width="1246" height="178" alt="Näyttökuva 2026-11-18 212532" src="https://github.com/user-attachments/assets/c1b10065-b8cf-440b-ac25-3675d1b354c8" />
  
 Vika näyttäisi olevan joko handlers tai tasks tiedostossa. Tarkistetaan yksi kerrallaan. Vika löytyi yml syntaksissa! ```notify: Restart fail2ban``` oli sisennetty väärin, joten korjaan sen:

 <img width="472" height="159" alt="Näyttökuva 2026-11-18 212730" src="https://github.com/user-attachments/assets/7702aa67-bfce-463b-ab1a-f83840e00b64" />

 Ajetaan siis playbookki uudelleen ja tarkistetaan idempotenssi. Nyt toimii!

 <img width="1250" height="212" alt="Näyttökuva 2026-11-18 212709" src="https://github.com/user-attachments/assets/9eaa7fa4-14d6-4d13-8f30-9ee69fa98e85" />

 - Lopuksi tarkistan Fail2banin lokitustason komennolla ```sudo fail2ban-client get loglevel```. Sen pitäisi palauttaa meille ```DEBUG```, mutta se paluattaakin ```INFO```.

   <img width="630" height="35" alt="Näyttökuva 2026-11-18 213958" src="https://github.com/user-attachments/assets/974355bf-23ea-4fbd-b503-265fb9a2a9bc" />

   Tämä luultavasti johtuu siitä, että asetustiedosto oli jo kopioitu ennen kuin lisäsin notify-määrityksen tai koska se oli aluksi sisennetty väärin joten kopioitu ennen kun kävin muuttamassa sisennystä. Ansible ei silloin välttämättä havainnut muutosta, eikä käynnistänyt palvelua uudelleen automaattisesti.

   Potaksitaan siis demoni uudelleen käyntiin ```sudo systemctl restart fail2ban``` ja ajetaan uudelleen ```sudo fail2ban-client get loglevel```.
   Nyt näyttää toimivan:

   <img width="665" height="54" alt="Näyttökuva 2026-11-18 214053" src="https://github.com/user-attachments/assets/b5c30746-01a4-40bd-a634-374f2c153324" />

## **d) Paikka remonttiin**

Tämän tehtävän tarkoituksena meidän on rikkoa asetuksia ja tarkistaa onko automaatio oikeasti toimiva. 

- Valitsin fail2banin poistamisen palvelimelta. Ajoin ```sudo apt-get purge fail2ban``` poistaen ohjelman asennuksen asetustiedostoineen.
- Varmistin, että ohjelma on poistettu eikä se ole käytössä ```sudo fail2ban-client ping```. Nyt palveluun ei saada yhteyttä.

 <img width="1253" height="669" alt="Näyttökuva 2026-11-18 224346" src="https://github.com/user-attachments/assets/c90d0b8f-e139-4621-b240-63ca0367b098" />


- Sitten siirryin Ansible -hakemistoon ja ajoin playbookin, joka tarkastaa onko Fail2ban asennettu ja jos se puuttuu, se asentaa sen uudelleen. Sen jälkeen asetustiedosto menee tarkistukseen, ja jos se puuttuu niin Ansible kopioi sen uudelleen master-koneelta. Lopuksi asetustiedoston muuttuminen käynnistää handlerin, joka käynnistää Fail2banin uudelleen.
  
  <img width="1252" height="617" alt="Näyttökuva 2026-11-18 224445" src="https://github.com/user-attachments/assets/b5d99886-683e-46d9-8e74-37d013060904" />

  Kohta changed=1 tarkoittaa, että Ansible havaitsi järjestelmässä puutteen ja teki tarvittavan muutoksen, eli asensi fil2banin uudelleen.

- Tarkistetaan palvelun status uudelleen ```sudo systemctl status fail2ban``` ja näkyy että se on käynnissä.
- testataan vielä ping = pong ja ajamalla```sudo fail2ban-client get loglevel```, että DEBUG-asetus on edelleen käytössä.

  <img width="887" height="356" alt="Näyttökuva 2026-11-18 224506" src="https://github.com/user-attachments/assets/682650ed-a9ef-4e3c-852a-9749fccf6ed2" />

## **e) Idempotentti**

Jos ajetaan nyt vielä kerran Ansible niin näyttää tältä:

<img width="1249" height="50" alt="Näyttökuva 2026-11-18 224847" src="https://github.com/user-attachments/assets/05c439e8-81dc-460b-a0bf-a900cdecf6ed" />

changed näyttää nyt 0. Tämä koska Fail2ban on asennettu ja käynnissä, eli Ansible ei joudu tekemään muutoksia.


## **LÄHTEET**
- Karvinen, T. 2023. Configuration Management of Distributed Systems over Unreliable and Hostile Networks. Doctoral thesis. University of Westminster. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/Karvinen-2023-Configuration-Management-of-Distributed-Systems-over-Unreliable-and-Hostile-Networks.pdf. Luettu: 18.11.2026.
- Hess, K. 2020. Linux security: Protect your systems with fail2ban. Red Hat. Luettavissa: https://www.redhat.com/en/blog/protect-systems-fail2ban. Luettu: 18.11.2026.
- Red Hat. 2023. Understanding Ansible, Terraform, Puppet, Chef, and Salt. Luettavissa: https://www.redhat.com/en/topics/automation/understanding-ansible-vs-terraform-puppet-chef-and-salt. Luettu: 18.11.2026.
- Fail2ban. s.a. fail2ban.conf. GitHub. Luettavissa: https://github.com/fail2ban/fail2ban/blob/master/config/fail2ban.conf. Luettu: 18.11.2026.
- Fail2ban. s.a. jail.conf.5 – Fail2Ban Configuration. GitHub. Luettavissa: https://github.com/fail2ban/fail2ban/blob/master/man/jail.conf.5. Luettu: 18.11.2026.
- Ansible Community. s.a. Desired state and idempotency. Ansible Documentation. Luettavissa: https://docs.ansible.com/projects/ansible/latest/user_guide/playbooks_intro.html. Luettu: 18.11.2026.
