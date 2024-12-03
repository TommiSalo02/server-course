# h5 Loppuhuipennus

## Johdanto

Tehtävässä h5 tuli tehdä oma moduuli esitysvalmiiksi. Aloitin oman Wireguard projektin viime viikolla tehtävässä h4. Siinä osiossa sain kaiken toimimaan manuaalisesti, elikkä Wireguard yhteys ja Salt olivat testattu. Seuraavaksi pyrin tekemään mahdollisimman paljon tästä asennuksesta automaattisesti Saltilla. Kolmas vaihe olisi automatisoida myös Saltin asennus, jolloin projektin voisi kloonata gitistä ja sen voisi saada pystyyn vain muutamalla komennolla. 

## Github

Halusin käyttää Githubia projektissa alusta asti, jotta voisin lopussa tehdä sen helposti ladattavaksi sieltä. Loin tähän tarkoitukseen uuden `wireguard-project` -reposition, jonka kloonasin koneelleni. Tämän jälkeen siirsin tarvittavat tiedostot gitin kansioon.

![image](https://github.com/user-attachments/assets/cc7bc10c-8d2f-448e-b4e1-a7ab9079de6a)

![image](https://github.com/user-attachments/assets/503b8d8e-8b5e-44eb-b2ef-c62221925138)

Pystyin käyttämään `.gitignore`-tiedostoa välttääkseni laitekohtaisten tiedostojen (kuten .vagrant) päätymistä gittiin. Pystyin helposti lähettämään muutoksia esimerkiksi `Vagrantfile`-tiedostoon ja viemään esimerkiksi eri konfigurointi-tiedostoja gittiin.

## Salt

Aloin tekemään projektin toista vaihetta upo-uusilla vagrant-koneilla. Tässä osiossa tuli käyttää Salttia Wireguardin pystyttämiseen ja katsoa miten pystyn minimoimaan manuaalisen työn kolmatta vaihetta varten. Aluksi latasin ja yhdistin saltin `Client`, `Server` ja `Master` -palvelimilla tuttuun tapaan. 

![image](https://github.com/user-attachments/assets/a7e3e4e2-d5ae-458a-b8ad-6c3bdea65efc)

_Salt toiminnassa_

Saltin asennus on melko yksinkertainen prosessi, mutta vaatii useamman palvelun uudelleenkäynnistyksen ja tuoreella vagrant-koneella myös esimerkiksi `curl`-työkalun lataamisen. Tämä voi tehdä kolmosvaiheen automatisoinnista melko hankalaa, mutta luotto on vielä kova omiin taitoihin.

## Wireguard

Viimeinen vaihe on Wireguardin lataaminen, konfigurointi ja käynnistäminen. Tämä voidaan automatisoida Saltin avulla.

### Lähteet
https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html
