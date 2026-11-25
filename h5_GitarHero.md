## **h5 - Gitar Hero**

## **x) Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git?**

- Git on hajautettu versionhallintajärjestelmä, jonka avulla voi seurata tiedostojen muutoksia, tallentaa projektin eri versioita ja palata tarvittaessa aikaisempaan versioon.
- Monet vanhemmat versionhallintajärjestelmät tallentavat tiedostojen väliset muutokset. Git puolestaan tallentaa projektista tilannekuvia (snapshot).
- Kun tallentaa muutokset commit-komennolla, Git tallentaa viittauksen projektin senhetkiseen tilaan. Jos jokin tiedosto ei ole muuttunut, Git voi käyttää aiemmin tallennettua versiota sen sijaan, että se tallentaisi tiedoston uudelleen.
- Suurin osa Gitin toiminnoista tapahtuu paikallisesti. 
- Gitillä voi tarkastella projektin aikaisempia versioita, vertailla tiedostojen muutoksia, tallentaa muutoksia paikallisesti, työskennellä ilman internetyhteyttä.
- Gitissä kun tallentaa muutokset commit-komennolla, niiden menettäminen on vaikeaa. Tämä tekee siitä myös oivallisen työkalun ohjelmistokehitykseen.

Mielestäni Git on mahtava työkalu, sillä se on turvallinen, koska muutokset tallennetaan paikallisesti ja kätevä siitä, että sitä voi käyttää ilman internet-yhteyttä.
Olen itse käyttänyt jonkun verran Git:iä Linux-ympäristössä. Koulukursseilla enemmän GitHub:ia. Tykkään silti ajaa git-komennot usein paikallisesti puskemalla lopputulokset GitHubiin (esimerkiksi ohjelmointikursseilla).

Git komennot ranslaisin viivoin:

- ```git add --all``` Lisää kaikki muutokset valmisteltaviksi.
- ```git commit``` Tallentaa muutokset paikallisesti.
- ```git pull``` Hakee muutokset etäpalvelimelta.
- ```git push``` Lähettää muutokset etäpalvelimelle.
- ```&&``` Suorittaa seuraavan komennon, jos edellinen onnistuu.
- ```git status``` Näyttää projektin tilan.
- ```-m``` Lisää commitille viestin.
- ```git clone``` Kun halutaan kloonata olemassa oleva repositorio paikalliselle koneelle.

## **a) Online**

Tässä tehtävässä loin GitHubiin uuden repositorion. Githubiin kirjauduttua klikataan kohdasta ```+``` oikeasta yläkulmasta ja valitaan _New Repository_. 

<img width="507" height="337" alt="Näyttökuva 2026-11-25 170421" src="https://github.com/user-attachments/assets/eb2e024a-e6ac-43cc-9f39-1559b4f16688" />

Annoin repositorion nimeksi ja kuvaukseksi _sunshine_ niinkun tehtävänannossa käsketty. Myös README-tiedosto lisätty asetuksista ja _GNU General Public License 3.0_ linsenssit.

<img width="940" height="860" alt="Näyttökuva 2026-11-25 170521" src="https://github.com/user-attachments/assets/b2d90aed-cd98-4720-a576-fe9b0e797f27" />

Kerran ollaan luotu repo niin näkymä näyttää seuraavalta:

<img width="1259" height="647" alt="Näyttökuva 2026-11-25 170611" src="https://github.com/user-attachments/assets/a6a96f08-f348-4ecc-827d-33568d017227" />

## **b) Dolly**

- Kirjauduin omalle Debianille ja loin aluksi h5-tehtäväkansion dokumentteihin, jonne kloonasin oman sunshine Repositoryn, joka oli luotu aiemmin GitHubissa.

  <img width="1175" height="301" alt="Näyttökuva 2026-11-25 172201" src="https://github.com/user-attachments/assets/2e758825-b06d-4a11-948b-90ddc510cbbc" />

- Seuraavaksi tarkistin menikö kloonaus läpi. Se meni läpi, sillä nyt näkyy _sunshine_ repositorio kansiossani. Seuraavaksi avasin repositorioni ja loin tekstitiedoston _dolly.txt_ jonne kirjoitin _Hei Dolly!_

  <img width="307" height="80" alt="Näyttökuva 2026-11-25 171838" src="https://github.com/user-attachments/assets/7f5355e0-5bb5-4d5d-89b4-a11983b3bf6c" />

- Tämän jälkeen muutokset piti puskea palvelimelle. Tarkistin ihan ensiksi muutokset ```git status``` komennolla ja sieltä tuli heti viestiksi, että _dolly.txt_ tiedostoa ollaan muutettu. Sitten ajetaan ```git add dolly.txt``` , jolla lisästään kaikki muutokset ja ```git commit -m``` ja perään suluissa viesti, jonka tarkoituksena on helpoittaa muistamaan mitä ollaan tässä commitissa tehty jos täytyisi tarkistaa jälkikäteen.

  <img width="1033" height="571" alt="Näyttökuva 2026-11-25 173458" src="https://github.com/user-attachments/assets/e58f5bbb-e643-41fe-a066-a446cbd41750" />

- Lopuksi yritin puskea ```git push```. Tällä komennolla paikalliseen repositorioon tehdyt commitit lähetetään etärepositorioon. Näin muutokset saadaan tallennettua myös GitHubiin. Muutosten siirtäminen kuuluisi onnistua, kun ne on ensin lisätty ```git add``` -komennolla ja tallennettu ```git commit``` -komennolla.

  <img width="954" height="98" alt="Näyttökuva 2026-11-25 173944" src="https://github.com/user-attachments/assets/895618ee-7577-4327-85e1-fd87897bb697" />

  Tässä kohdassa meni joku pieleen autentikoinnissa. Muistelin että tunnilla oltiin näytetty jotain asetuksia, jotka täytyy tehdä GitHubissa jotta tämä toimisi. Päätin siis etsiä tietoa myös eri lähtesitä ja löysin apua tähän GitHubin sivuilta. Löytämieni tietojen mukaan GitHub ei enää hyväksy tavallista GitHub-tilin salasanaa git push -komennon tunnistautumiseen.

- Tein asetuksiin muutoksia GitHubin puolella _SSH and GPG keys_ kohdassa ja lisäsin sinne oman ssh avaimeni jonka kävin kopioimassa virtuaalikoneeltani. Tämän jälkeen GitHub tunnistaa koneeni SSH-avaimen avulla, eikä minun tarvitse käyttää GitHub-salasanaa ```git push``` -komennossa.

  




## **LÄHTEET** 

- https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
- https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github?utm_source=chatgpt.com






