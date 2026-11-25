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

```git add --all``` Lisää kaikki muutokset valmisteltaviksi.
```git commit``` Tallentaa muutokset paikallisesti.
```git pull``` Hakee muutokset etäpalvelimelta.
```git push``` Lähettää muutokset etäpalvelimelle.
```&&``` Suorittaa seuraavan komennon, jos edellinen onnistuu.
```git status``` Näyttää projektin tilan.
```-m``` Lisää commitille viestin.
```git clone``` Kun halutaan kloonata olemassa oleva repositorio paikalliselle koneelle.
