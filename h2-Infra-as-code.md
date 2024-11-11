# h2 Infra-as-code

## Johdanto

Tehtävässä h2 tuli asentaa Vagrant ja harjoitella sen sekä Saltin avulla kahden koneen herra-orja arkkitehtuuria. Vagrant ei ollut itselleni entuudestaan tuttu, joten aloitin tehtävän siihen tutustumalla ja asentamalla sen.

## Ennakkomateriaali

Karvisen artikkeli "Two Machine Virtual Network With Debian 11 Bullseye and Vagrant" auttoi tehtävän virtuaaliympäristön luomisessa. Artikkeli neuvoi miten luodaan kaksi virtuaalikonetta ja kokeillaan niiden yhteyttä Vagrantin avulla.

### Lähteet

Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant

Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux

Karvinen 2014: Hello Salt Infra-as-Code

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves

Salt contributors: Salt overview

## Vagrant & virtuaalikoneet (A-C)

Vagrantin kotisivuilta sain selville, että Vagrant on ohjelma, jolla voi luoda ja hallita virtuaalikoneita. Tämä helpottaa ja nopeuttaa prosessia suuresti verrattuna manuaaliseen vaihtoehtoon. 

Latasin ensin Vagrantin kannettavalleni. Valitsin Windows version `AMD64 2.4.2`, sillä kannettavani pyörii Windowsilla. Nopean SetUp-velhoilun ja koneen uudelleenkäynnistämisen jälkeen Vagrant oli asennettuna. 

Voin valmiiksi olettaa Windowsin aiheuttavan itkua ja hampaanpuremista tehtävän aikana, mutta Vagrantin pyörittäminen Linux-virtuaalikoneessa vaikuttaa vielä tuskaisemmalta.

![image](https://github.com/user-attachments/assets/fea407a8-5821-4e74-b70c-d5b9643ff882)

_Vagrant asennettu_



### Lähteet

Vagrant: Get Started. Luettavissa: https://developer.hashicorp.com/vagrant/tutorials/getting-started/getting-started-index.
