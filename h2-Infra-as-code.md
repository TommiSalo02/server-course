# h2 Infra-as-code

## Johdanto

Tehtävässä h2 tuli asentaa Vagrant ja harjoitella sen sekä Saltin avulla kahden koneen herra-orja arkkitehtuuria. Vagrant ei ollut itselleni entuudestaan tuttu, joten aloitin tehtävän siihen tutustumalla ja asentamalla sen.

## Ennakkomateriaali

- Karvisen artikkeli "Two Machine Virtual Network With Debian 11 Bullseye and Vagrant" auttoi tehtävän virtuaaliympäristön luomisessa. Artikkeli neuvoi miten luodaan kaksi virtuaalikonetta ja kokeillaan niiden yhteyttä Vagrantin avulla.

- Karvisen artikkeli "Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux" on tuttu jo h1 tehtävän raportista. Artikkeli käsittelee Saltin asennusta ja toimintaa.

- Karvisen artikkeli "Hello Salt Infra-as-Code" syventyy Saltin käyttöön. Saltissa konfigurointitiedostoa kutsutaan nimellä "state" eli tila. Jos haluamme kirjoittaa "infraa koodina", voimme luoda tila-tiedoston (kansiossa `hello`, jonka Salt voi ottaa koneille käyttöön komennolla `state.apply hello`. Tämän avulla voimme saada idempotenttia, helposti seurattavaa, helposti käyttöönotettavaa ja helposti laajennettavaa konfigurointia palvelimillemme Saltin avulla.

  Seuraava asken on luoda `top.sls` tiedosto, joka määrittää sen, mitä tilaa kukin kone käyttää. Tämän johdosta emme tarvitse enää edes tiedostosijaintia komennossa `state apply`, vaan se konfiguroi kaikki automaattisesti `top.sls` tiedostoon nojaten.

- Karvisen artikkeli "Salt Vagrant - automatically provision one master and two slaves" antoi vielä täsmälliset komennot Salt tilatiedoston luomiseen ja käyttöönottoon.

- Artikkeli "Salt overview" antoi vielä tietoa `YAML` merkintäkielestä, jota Salt käyttää. YAML koostuu kolmesta eri elementistä: skaalarit / avain-arvo-parit (vihannes: herneet), listat (vihannekset: - herneet - porkkanat) ja sanakirjat (illallinen: alkupala: herneet pääruoka: - pihvi - ranut). YAML vaatii tarkkaa kirjoitusta/sisennystä, jotta se toimisi.

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

Tämän jälkeen aloin luomaan virtuaaliympäristöä Vagrantilla. Sovelsin tässä kohdassa Karvisen artikkelia "Two Machine Virtual Network With Debian 11 Bullseye and Vagrant". Osa komenoista tuli muuttaa Windows-formattiin.

Loin ensin uuden hakemiston `mkdir h2` ja hakeuduin sinne `cd h2`. Uuteen hakemistoon loin Notepadillä konfigurointi-tiedoston `Vagrantfile`, joka sisälsi artikkelin tarjoaman kofigurointitiedot. Konfigurointitiedot asentavat ja päivittävät kahdet virtuaalikoneet (`t001` ja `t002`) käyttövalmiiksi ja antavat näille IP-osoitteet `192.168.88.101` & `192.168.88.102` verkossa `private_network` Jouduin vielä muuttamaan konfiguraatiotiedoissa debianin version uudemmaksi, elikkä `bookworm64`.

![image](https://github.com/user-attachments/assets/7fc3c1a7-3b9e-4c66-a023-c78c3d93b89b)

_Vagrant havaitsee konfigurointitiedoston_

Konfiguroinnin jälkeen komento `vagrant up` asentaa virtuaalikoneet.

![image](https://github.com/user-attachments/assets/dc2af9a9-e88f-4ebe-81de-a19fd904c116)

_Virtuaalikoneet valmiina_

Kokeilin vielä ottamaan ssh yhteyden kumpaankin koneeseen ja tarkastamaan yhteydet.

![image](https://github.com/user-attachments/assets/411859b9-8dd7-4d28-842b-823d66a1f102)

![image](https://github.com/user-attachments/assets/003939e0-5aa2-4a1f-b324-a6fa7904be7b)

_Yhteyskokeilut_

Yhteyskokeilussä käy ilmi, että molemmat koneet saavat yhteyden toisiinsa sekä verkon ulkopuolelle. Koneilla on siis sisäverkko `192.168.88.0/24` ja NAT-verkko `10.0.2.0/24`.

### Lähteet

Vagrant: Get Started. Luettavissa: https://developer.hashicorp.com/vagrant/tutorials/getting-started/getting-started-index.
