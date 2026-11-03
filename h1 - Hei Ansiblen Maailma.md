## **h1 - Hei Ansiblen maailma**

_Päivitetty 3.11.2026_

## x) **Karvinen 2026: SSH public key - Login without password**
- SSH on johtava ratkaisu palvelimille kirjautumiseen turvallisesti.
- SSH on monien taustalla käyttämä työkalu (git, ansible...).
- SSH-avain helpottaa kirjautumista (salasanaa ei tarvitse syöttää joka kerta) ja parantaa palvelimen tietoturvaa.
- SSH on helppo käyttää. Alussa se asennetaan vain kuten muutkin ohjelmat.

## **Karvinen 2026: Hello Ansible**
- Ansiblella voimme hallita useita koneita helposti ja samanaikaisesti.
- Ansible toimii SSH:n kautta. Vaatimuksena ovat SSH-daemoni ja Python asennettuna.
- Auttaa uusien koneiden nopeassa konfiguroinnissa.

## **a) Paikallista**
Katso h0-tehtävät:

https://github.com/alvarmanfe/Server-management/blob/main/h0.md

**TAI**... jos haluat tarkistella enemmän asennuksesta hyppää taas Linux Palvelimet kurssin h1 raporttiin, klikkamalla alla olevasta linkistä:

https://github.com/alvarmanfe/Linux-servers/blob/main/h1.md

##  **b) Sshecrets**

Kun kirjauduin virtuaalikoneelleni ja avasin terminaalin, päivitin ensin järjestelmän ajamalla:
```
sudo apt-get update
```
Sitten otin SSH:n käyttöön:
```
sudo systemctl enable
```
Asennusta ei tarvinnut tehdä tällä kertaa, koska tein sen jo aiemmin Linux-kurssilla. Lopuksi kokeilin, toimiiko se, potkaisemalla daemonia:
```
ssh localhost
```

![Sieppaa](https://github.com/user-attachments/assets/24bb8957-e13d-4faa-9e54-4444ecc79c8e)

Still rocking!

## **c) Pubkey**
Automatisoin SSH-kirjautumisen julkisella avaimella, joka minulla oli jo valmiina. Ajoin siis vain:

```
ssh-copy-id localhost
ssh localhost
```
![Sieppaa1](https://github.com/user-attachments/assets/5941d106-84ff-4d3a-99c2-41e1de4bcd8d)

## **d) Hei Ansible**

Ihan aluksi testataan SSH:n toimivuus ilman Ansiblea.
```
ssh localhost
```
kerta toimii niin kirjaudutaan nyt saman tien ulos ```exit```

Sudolla päivitetään paketit:
```
sudo apt update
```
ja asennetaan Ansible ja tarkastetaan sen versio ajamalla ```ansible --version```

![Sieppaa2](https://github.com/user-attachments/assets/d5736e17-8467-4c5c-aa59-3a703d0104b2)

Luodaan ansible projekti. Tässä vaiheessa minulla oli jo valmiina Ansible directory joten minun ei tarvitse luoda uutta directoria. Kirjoitetaan lista hosteista jota tullaan ohjaamaan. Luodaan hosts.ini ja lisätään siihen localhosti. Testataan Ansible SSH:n yli, joka näyttää toimivan. Tein yml tiedoston jonka sisään rooliksi annoin "hello". Loin myös hakemistorakenteen ```roles/hello/tasks```. Roolin sisään luotiin main.yml-tiedosto, joka sisältää varsinaisen tehtävän. Tehtävänä oli kopioida teksti tiedostoon /tmp/hello-ansible. Tämä tehtiin Ansible-moduulilla copy, joka määriteltiin seuraavasti:
```
- copy:
    dest: /tmp/hello-ansible
    content: "Hei maailma Ansiblella!\n"
```
Ajettiin playbooki uudestan komennolla 
```
ansible-playbook site.yml
```
Ansible suoritti roolin onnistuneesti ja loi tiedoston kohdekoneelle.

Lopuksi varmistettiin lopputulos SSH-yhteyden yli komennolla:
```
ssh localhost 'cat /tmp/hello-ansible'
```
Tämä tulosti:
```
Hei maailma Ansiblella!
```
Ansible onnistuneesti suoritti infrastruktuurin hallinnan SSH:n yli ja loi halutun lopputilan kohdekoneelle.

![Sieppaa3](https://github.com/user-attachments/assets/bd5b482c-0f3f-47fc-bfe7-eb292b2c8b26)

Lopullinen rakenne:

![Sieppaa4](https://github.com/user-attachments/assets/fd81b225-7c57-4e35-aadb-4a15b9fdf361)

## **LÄHTEET**
- Karvinen, T. 2026. Verkkosivu. SSH public key - Login without password. Luettavissa: https://terokarvinen.com/ssh-public-key-login-without-password/. Luettu: 02.04.2026.
- Karvinen, T. 2026. Verkkosivu. Hello Ansible. Luettavissa: https://terokarvinen.com/hello-ansible/. Luettu 02.04.2026.
- Karvinen, T. 2026. Verkkosivu. Palvelinten hallinta. Luettavissa: https://terokarvinen.com/palvelinten-hallinta/. Luettu: 02.04.2026.
- Manfe, A. 2026. h0 - Oikeasti netissä. Server-management. GitHub. Luettavissa: https://github.com/alvarmanfe/Server-management/blob/main/h0.md. Luettu: 30.10.2026.
- Manfe, A. 2026b. h1 - Oma Linux. Linux-servers. GitHub. Luettavissa: https://github.com/alvarmanfe/Linux-servers/blob/main/h1.md. Luettu: 30.10.2026.
