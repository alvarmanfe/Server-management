## **h5 - Gitar Hero**
_Aloitus 25.11.2026 klo 13:00_

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
  Tämän jälkeen olikin luvassa pientä odottelua sillä GitHubissa on ilmennyt pieniä ongelmia, eikä minulla toiminut lainkaan git komennot sekä ssh-avaimen lisääminen asetuksiin.
  
  <img width="991" height="707" alt="Näyttökuva 2026-11-25 182134" src="https://github.com/user-attachments/assets/f2d58a30-b84a-4fdf-a0bc-ddae498876bc" />

  Pitkän temppuilun jälkeen alkoi taas toimia. Jatkoin siis tehtäviä myöhemmin iltapäivällä. Sain nyt liitettyä virtuaalikoneen ssh-avaimen asetuksiin.

  <img width="1003" height="252" alt="Näyttökuva 2026-11-25 182157" src="https://github.com/user-attachments/assets/258e768c-a435-4ba2-a301-607a2c6bcd8c" />

- Käynnistin tässä vaiheessa uuden Terminaalin ja tarkistin, että _dolly.txt_ tekstitiedostoni löytyy repokansiosta ja kaikki näyttäisi olevan commitattu. Viimeiseksi ajoin ```git push``` uudestaan ja nyt vihdoin toimii.
  Muutokset on viety nyt onnistuneesti etärepositoriionkin.

  <img width="1217" height="558" alt="Näyttökuva 2026-11-25 183940" src="https://github.com/user-attachments/assets/9e142575-4822-4115-8136-f478e136bbc5" />

  <img width="493" height="205" alt="Näyttökuva 2026-11-25 184011" src="https://github.com/user-attachments/assets/ed47279f-0bdc-4467-ade4-1026dafd3af5" /

  Omaa pohdintaa:
  - Tämän tehtävän aikana huomatiin Gitin tärkeys. GitHub-palvelukatkosta huolimatta sain tehtyä kaikki muutokset paikallisesti, sillä GitHubissa luoma repositorioni oli jo kloonattu omalle koneelle. Etärepositoriossa näkymisen edellytyksenä oli kuitenkin GitHub-sivuston korrektin toimiminen.
  - Myös commit viestit, kuten repon nimet ja kuvaus, kannattaa aina muistaa kirjoittaa englanniksi.

## **c) Doh!**

- Tein muutoksia äskeiseen tekstitiedostoon vaihtamalla sen sisältöä näin:

  <img width="277" height="44" alt="Näyttökuva 2026-11-25 185235" src="https://github.com/user-attachments/assets/60d1c916-0121-4bf1-bc2f-df09c5a62dbd" />

- En ajanut _commit_ komentoa vaan tarkistin statuksen ja muutokset:

  <img width="723" height="339" alt="Näyttökuva 2026-11-25 185753" src="https://github.com/user-attachments/assets/dbe4e249-7ee9-45e1-86ff-cff1089ad5b8" />
  
  Tässä näkyy miten tiedoston tekstiä on muutettu.
  
- Tuhoan muutokset komennolla ```git reset --hard```, jonka jälkeen tarkistan uusiksi statuksen ja tekstitiedostoni, joka on palautunut viimeisimmän commitin mukaiseen tilaan.

  <img width="596" height="171" alt="Näyttökuva 2026-11-25 190129" src="https://github.com/user-attachments/assets/d014516b-ab28-48c1-9320-a377b367e9e2" />

## **d) Tukki**

- Tässä tehtävässä tarkistin lokit komennolla ```git log```. Komento näytti Gitin versionhistorian eli aikaisemmin tallennetut commitit, tunnisteet, tekijän, tallennusaika ja commit-viestit.

  <img width="912" height="226" alt="Näyttökuva 2026-11-25 190811" src="https://github.com/user-attachments/assets/87105aa6-1d99-4dab-94b2-3711e5f08ceb" />

- Sen jälkeen ```git log -p``` nähdäkseni, myös mitä muutoksia olin tehnyt Ansiblessa ja niitä koskevat tiedot, commitien lisäksi.
  
  <img width="943" height="639" alt="Näyttökuva 2026-11-25 191057" src="https://github.com/user-attachments/assets/ceb2d4b7-1b5c-4d99-bd19-2506fa7ec7d4" />
  
  <img width="1146" height="700" alt="Näyttökuva 2026-11-25 191146" src="https://github.com/user-attachments/assets/a7cbf0ff-af74-490e-919b-4ad4311ecf2b" />

## **e) Gitanbile**

- Suuntasin aluksi Ansible juurikansioon ja alustin siellä Gitin ```git init```. Tarkistataan status. Lisätään kaikki tiedostot ```git add .```

  <img width="865" height="575" alt="Näyttökuva 2026-11-25 192646" src="https://github.com/user-attachments/assets/75e08e31-ba59-4bba-aa9b-fca853372a60" />

- Sen jälkeen tallennan commitilla ja lisään kuten aina viestin perään. Nyt kaikki tiedostot on tallennettu.

  <img width="753" height="474" alt="Näyttökuva 2026-11-25 192727" src="https://github.com/user-attachments/assets/664a31d3-45b3-4795-a0a1-687790bddc86" />

- Lisäsin uuden tehtävän NGINX-rooliin (```micro roles/nginx/tasks/main.yml```):

  <img width="637" height="339" alt="Näyttökuva 2026-11-25 194932" src="https://github.com/user-attachments/assets/bf86f61b-590f-479d-b708-33ee8aa45af1" />

  - name on tehtävän kuvaus.
  - ansible.builtin.copy luo tai kopioi tiedoston.
  - content määrittää tiedoston sisällön.
  - dest kertoo tiedoston sijainnin palvelimella.
  - owner, group ja mode määrittävät omistajan, ryhmän ja käyttöoikeudet.

  ja ajoin lopuksi Ansiblen:

  <img width="1249" height="66" alt="Näyttökuva 2026-11-25 195040" src="https://github.com/user-attachments/assets/57474a60-fa89-4bf1-8977-89c0e2271350" />

  <img width="1230" height="273" alt="Näyttökuva 2026-11-25 195120" src="https://github.com/user-attachments/assets/2cba4d3d-b913-4d12-b09d-bdc91ec596d9" />

Ansible-playbookin ajamisen jälkeen käytin Git-komentoja tallentaakseni tekemäni muutoksen versionhallintaan varmistaakseni että Ansiblella tehty muutos oli tallennettu Gitissä ja että sen voi jälkikäteen nähdä versionhistoriasta.

```git status``` tarkistin, mitkä tiedostot olivat muuttuneet tai vielä tallentamatta Gitiin.
```git diff``` tarkistin, mitä muutoksia tiedostoihin oli tehty.
```git add .``` – lisäsin muuttuneen YML-tiedoston seuraavaan commitiin.
```git commit``` – tallensin muutoksen Gitin versiohistoriaan kuvaavalla viestillä.
```git log``` – tarkistin, että commit tallentui ja näkyi projektin historiassa.

  <img width="879" height="458" alt="Näyttökuva 2026-11-25 195834" src="https://github.com/user-attachments/assets/7958cf58-1e81-42d7-b85b-d2fcc2435940" />'

  <img width="1032" height="549" alt="Näyttökuva 2026-11-25 195901" src="https://github.com/user-attachments/assets/e7c6305e-b56c-4a6d-b73a-6f0a2588eed4" />

## **f)**

Olen löytänyt parin ryhmäprojektiin ja ollaan sovittu Teamsin välityksellä seuraavista askelista.



## **LÄHTEET** 

- Git. s.a. What is Git? Luettavissa: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F. Luettu: 25.11.2026.

- GitHub Docs. s.a. About authentication to GitHub. Luettavissa: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github. Luettu: 25.11.2026.

- GitHub. s.a. sunshine: GitHub repository. Luettavissa: https://github.com/alvarmanfe/sunshine.






