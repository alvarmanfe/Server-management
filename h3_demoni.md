## **h3 - Demoni**

## **x) Tiivistelmä**
## **Karvinen 2026: Apache installed with Ansible - quick notes**

- Apache on demoni ja verkkopalvelin, jonka tehtävä on vastaanottaa HTTP- ja HTTPS-pyyntöjä selaimilta.
- Package - file - service:
  - **Package:** Apache asennetaan tavallisesti ```sudo apt-get install apache2```
  - **File:** asetustiedostojen muokkaaminen ```sudoedit /etc/apache2```
  - **Service:** uudellen käynnistys, jotta muutokset tulevat voimaan ```systemctl restart apache2```
- Apachea täytyy muistaa potkia. Aina kun sen asetustiedostoja muutetaan, se ei välttämättä huomaa muutoksia automaattisesti. Siksi se täytyy käynnistää uudelleeen, eli potkia (_restart_).

## **Ansible Community Documentation: Handlers: running operations on change**

- **Handlerit (Handlers):** ovat Ansiblessa tehtäviä, jotka suoritetaan vaan silloin, kun toinen tehtävä ilmoittaa muutoksesta, eli toisin sanoen, silloin kun palvelimella tapahtuu muutos. Esimerkiksi kun Apache asetustiedostoa muutetaan, niin se käynnistyy uudelleen, jotta uudet asetuukset tulevat käyttöön. Jos muutoksia ei tehdä niin Apachea ei tarvitse uudelleenkäynnistää.
- Tehtävän lopussa olevalla ```notify```lla, voidaan ilmoittaa handlerille toiminnon suorittamisesta. Tässä tapauksessa, jos tiedosto on muuttunut niin notify ilmoittaa handlerille, joka suorittaa uudelleenkäynnistyksen.
- Handlerit ovat apuna automaatiossa, jolla vältetään turhia palvelun uudellenkäynnistäytymisiä.

## **Apassi**


- Kirjaudun ensiksi omalle palvelimelle käyttäjällä _anseba_. Ennen kun jatkan tarkistan ```whoami``` komennolla kuka on tämänhetkinen käyttäjä.
<img width="1047" height="267" alt="Näyttökuva 2026-11-11 160951" src="https://github.com/user-attachments/assets/335f8f70-5da0-4ad9-b839-dae1cf2e6b4e" />

- Loin
<img width="684" height="549" alt="Näyttökuva 2026-11-11 164828" src="https://github.com/user-attachments/assets/16d0593e-bf8c-45e6-bc0d-c6ae8c318983" />

- Avataan yksi kerralla nämä tiedostot ja tehdään sinne tarvittavat muutokset Teron ohjeiden mukaisesti [Lue lähde: Apache installed with Ansible](https://terokarvinen.com/apache-ansible/).

  <img width="733" height="56" alt="Näyttökuva 2026-11-11 172334" src="https://github.com/user-attachments/assets/42f5862b-4a48-430d-935d-e0f0b51d0ebb" />

- ```tasks/main.yml```
  
  <img width="752" height="396" alt="Näyttökuva 2026-11-11 171757" src="https://github.com/user-attachments/assets/6e916f9f-3aed-4181-a983-9037493917c0" />

- ```handlers/main.yml```
  
  <img width="329" height="86" alt="Näyttökuva 2026-11-11 172033" src="https://github.com/user-attachments/assets/511230e4-9a50-41b7-8807-cf7ab61faacc" />

- ```files/example.com.conf```
  
  <img width="502" height="166" alt="Näyttökuva 2026-11-11 172245" src="https://github.com/user-attachments/assets/ace23067-6bff-4b78-b920-bbbf701e8d95" />

Tässä vaiheessa aloin pohtimaan eikös tehtävässä mainittu Apachen asennuksesta suoritettavaksi nimenomaan käsin eikä automatisoidusti. Lähdin siis tekemään tehtävää uudestaan omalla _alvar_ käyttäjälläni.

- Avasin siis uuden terminaali-ikkunan ja päivitin aluksi paketit ajamalla ```sudo apt update``` ja asensin apachen heti porään ```sudo apt-get install apache2```

<img width="794" height="261" alt="Näyttökuva 2026-11-11 180748" src="https://github.com/user-attachments/assets/8d16ee26-785b-4ade-9a07-3f4e93a8c4c8" />

  Apache näyttääkin olevan jo ennalta asennettu.

- Tarkistetaan Apachen status ```sudo systemctl status apache2```

<img width="797" height="271" alt="Näyttökuva 2026-11-11 181840" src="https://github.com/user-attachments/assets/6f284efc-136a-4893-a3d1-e228489d675a" />



## **LÄHTEET**

- Karvinen, T. 2026. Apache installed with Ansible – quick notes. Luettavissa: https://terokarvinen.com/apache-ansible/. Luettu: 11.11.2026.

- Ansible Community Documentation. N.d. Handlers: running operations on change. Luettavissa: https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html. Luettu: 11.11.2026.





  
