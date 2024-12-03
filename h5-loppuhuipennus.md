# h5 Loppuhuipennus

## Johdanto

Tehtävässä h5 tuli tehdä oma moduuli esitysvalmiiksi. Aloitin oman Wireguard projektin viime viikolla tehtävässä h4. Siinä osiossa sain kaiken toimimaan manuaalisesti, elikkä Wireguard yhteys ja Salt olivat testattu. Seuraavaksi pyrin tekemään mahdollisimman paljon tästä asennuksesta automaattisesti Saltilla. Kolmas vaihe olisi automatisoida myös Saltin asennus, jolloin projektin voisi kloonata gitistä ja sen voisi saada pystyyn vain muutamalla komennolla. 

## Github

Halusin käyttää Githubia projektissa alusta asti, jotta voisin lopussa tehdä sen helposti ladattavaksi sieltä. Loin tähän tarkoitukseen uuden `wireguard-project` -reposition, jonka kloonasin koneelleni. Tämän jälkeen siirsin tarvittavat tiedostot gitin kansioon.

![image](https://github.com/user-attachments/assets/cc7bc10c-8d2f-448e-b4e1-a7ab9079de6a)

![image](https://github.com/user-attachments/assets/503b8d8e-8b5e-44eb-b2ef-c62221925138)

Pystyin käyttämään `.gitignore`-tiedostoa välttääkseni laitekohtaisten tiedostojen (kuten .vagrant) päätymistä gittiin. Pystyin helposti lähettämään muutoksia esimerkiksi `Vagrantfile`-tiedostoon ja viemään esimerkiksi eri konfigurointi-tiedostoja gittiin.
