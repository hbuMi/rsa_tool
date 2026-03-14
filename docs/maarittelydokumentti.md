# Määrittelydokumentti

Opinto-ohjelma: Tietojenkäsittelytieteen kandidaattiohjelma (TKT) 

Tässä projektissa implementoidaan RSA-algoritmi osana Algoritmit ja tekoäly harjoitustyö -kurssia. Projekti toteutetaan hyödyntäen Pythonia, joka on toistaiseksi ainut ohjelmointikieli, jota osaan vertaisarvioida. Projektin käyttöliittymä ja dokumentointi toteutetaan suomeksi. Valitsin aiheen mielenkiinnosta tietoturvaa kohtaan.

Tavoitteena on luoda ohjelma, joka käyttäjän syötteen mukaan: 
  1. Luo RSA-salauksessa käytettävän avainparin (julkinen ja yksityinen avain) 
  2. Salaa käyttäjän syötteen julkisella avaimella 
  3. Purkaa salatun syötteen alkuperäiseen muotoonsa yksityisellä avaimella 

## Avainparin luominen 

Projektin keskiössä on avainparien luominen ja alkulukujen generointi, joissa käytetään useita eri algoritmeja. 
  - Julkisen avaimen luomisessa generoidaan kaksi suurta alkulukua p ja q. Näiden generointiin käytetään Sieve of Eratosthenes- ja Miller–Rabin primality test -algoritmeja. Sieve of Eratosthenes -algoritmilla muodostetaan lista pienistä alkuluvuista, jota hyödynnetään seulana tarkastamaan onko testattava luku jaollinen jollakin niistä. Mikäli testattava luku ei ole jaollinen millään listan pienistä alkuluvuista, käytetään Miller–Rabin primality test -algoritmia arvioimaan, onko testattava luku todennäköinen alkuluku. 
  - Kun kaksi suurta alkulukua on generoitu, RSA-avaimet muodostetaan: 
    1. Lasketaan n = p x q 
    2. Lasketaan φ(n)=(p−1)(q−1) 
    3. Valitaan julkinen eksponentti e, jolle pätee: - 1 < e < N - on suhteellinen alkuluku 1 < e < N φ(n):n kanssa 
    4. Lasketaan yksityinen eksponentti d, siten että - d = e^(-1) mod φ(n) - yksityinen eksponentti d generoidaan käyttäen Extended euclidean -algoritmia. 
    5. Saadaan julkiseksi avainpariksi (e, n) ja yksityiseksi avainpariksi (d, n) 

## Syötteen salaus ja purkaminen 

Syötteen salauksessa ja purkamisessa käytetään Pythonin valmista modulaarista potenssifunktiota. Salauksessa käyttäjän syöte korotetaan julkisen avaimen eksponenttiin modulo n. Vastaavasti purkamisessa syöte korotetaan yksityisen avaimen eksponenttiin modulo n. 

## Aika- ja tilavaativuudet

Aika- ja tilavaativuuksia ohjelmalle ei voida määrittää tarkasti, sillä aika- ja tilavaativuudet riippuvat satunnaisista tekijöistä. Suurin osa ohjelman ajasta ja tilasta kuluu alkulukujen etsimiseen avainparia generoidessa, koska useita satunnaisia lukuja täytyy testata ennen kuin kaksi sopivaa alkulukua löytyy.

## Lähteet: 
https://fi.wikipedia.org/wiki/RSA
https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes
https://en.wikipedia.org/wiki/Miller%E2%80%93Rabin_primality_test
https://en.wikipedia.org/wiki/Extended_Euclidean_algorithm
