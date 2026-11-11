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




  
