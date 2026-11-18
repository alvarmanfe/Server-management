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

- 

  


















## **LÄHTEET**
- https://westminsterresearch.westminster.ac.uk/download/4cc417566aa9af60fe3826d690719e390abdb7a3c8672f3d51b1eb4ca75e7624/1427236/karvinen-2023-configuration-management-of-distributed-systems.pdf
- https://www.redhat.com/en/topics/automation/understanding-ansible-vs-terraform-puppet-chef-and-salt
- https://www.redhat.com/en/blog/protect-systems-fail2ban
- https://github.com/fail2ban/fail2ban/blob/master/config/fail2ban.conf?utm_source=chatgpt.com
