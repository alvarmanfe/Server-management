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

## **a) Apassi**

- Avasin siis uuden terminaali-ikkunan ja päivitin aluksi paketit ajamalla ```sudo apt update``` ja asensin apachen heti porään ```sudo apt-get install apache2```

  <img width="794" height="261" alt="Näyttökuva 2026-11-11 180748" src="https://github.com/user-attachments/assets/8d16ee26-785b-4ade-9a07-3f4e93a8c4c8" />

  Apache näyttääkin olevan jo ennalta asennettu.

- Tarkistetaan Apachen status ```sudo systemctl status apache2```

  <img width="797" height="271" alt="Näyttökuva 2026-11-11 181840" src="https://github.com/user-attachments/assets/6f284efc-136a-4893-a3d1-e228489d675a" />

- Avaan Apachen asetustiedostot komennolla:
```sudoedit /etc/apache2/sites-available/sona2k.example.com.conf```

- Lisään tarvittavat muutokset jotka osoittaavat _public_ kansioon jossa index.html sivuni löytyy

  <img width="606" height="232" alt="Näyttökuva 2026-11-12 065406" src="https://github.com/user-attachments/assets/a9c2bf62-b7f2-4d4c-a952-7edcc2651447" />

- Lopuksi otan käyttöön asetustiedoston ja pyydän Apachea lataamaan asetukset uudelleen ```sudo systemctl reload apache2```

  <img width="805" height="79" alt="Näyttökuva 2026-11-12 070116" src="https://github.com/user-attachments/assets/70bfdab0-461c-4b3d-ac44-086500d17f15" />


  <img width="585" height="111" alt="Näyttökuva 2026-11-12 071134" src="https://github.com/user-attachments/assets/61830570-20aa-4ee4-a42b-94bea9ac6dcd" />
  <img width="342" height="56" alt="Näyttökuva 2026-11-12 071043" src="https://github.com/user-attachments/assets/2814e895-6936-4f42-9869-305bb96e1957" />

```index.html``` omistaja on alvar ja sen oikeudet ovat rw-, eli käyttäjä alvar voi muokata tiedostoa ilman root- tai sudo-oikeuksia.

- Nyt palvelimeni etusivulla näkyy index.html kirjoittama koodini.

  <img width="587" height="153" alt="Näyttökuva 2026-11-12 070923" src="https://github.com/user-attachments/assets/523b6952-df3f-4c40-9408-cf1a0c629f70" />

## **b) Moottorix**

Tässä tehtävässä asennetaan nginx:

- Teron vinkkeissä "Kaksi demonia ei voi kuunnella samaa porttia". Eli ennen nginx asennusta kytketään Apache pois päältä. Sen jölkeen voidaankin heti asentaa nginx.
  <img width="1131" height="332" alt="Näyttökuva 2026-11-12 073316" src="https://github.com/user-attachments/assets/adbe4686-9f5e-44df-8c14-c8867839e11f" />






## **LÄHTEET**

- Karvinen, T. 2026. Apache installed with Ansible – quick notes. Luettavissa: https://terokarvinen.com/apache-ansible/. Luettu: 11.11.2026.

- Ansible Community Documentation. N.d. Handlers: running operations on change. Luettavissa: https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html. Luettu: 11.11.2026.





  
