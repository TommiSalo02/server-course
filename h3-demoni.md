# h3 Demoni

## Johdanto

Tehtävässä h3 tuli tutustua Apacheen ja SSH-porttikuunteluun. Lisäksi tuli valita aihe kurssin omalle moduulille. Valitsin itse x, sillä...

## Ennakkomateriaalit

Ennakkomateriaalin artikkeli käsitteli viime viikon raportissa (h2) tarkasteltuja `.sls`-konfigurointitiedostoja. Esimerkissä käytetään `pkg.installed`, `file.managed` ja `service.running`-tilafunktioita `sshd`-konfigurointitiedoston lataamiseksi/muokkaamiseksi/tarkastamiseksi.

Lisäksi katsoin läpi Saltin ohjeet tilafunktioihin liittyen.

### Lähteet
Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/. Luettu 18.11.2024

## Apache (Kohta A)

Latasin ensin Apachen manuaalisesti virtuaalikoneelleni. Tämä järjestyy komennoilla `sudo apt-get update` --> `sudo apt-get install apache2`. Korvasin seuraavaksi Apachen oletustiedoston sisällön `echo`-komennolla, käynnistin palvelun ja kokeilin `curl`-komennolla sen toimivan.

![image](https://github.com/user-attachments/assets/3552dd20-41d1-451c-93ab-0a8e06f6b541)

_Apache toimii? Apache toimii! Apache toimii._

Seuraavaksi käytin komentoa `sudo apt-get remove apache2` poistaakseni Apachen. Tämän jälkeen voin tehdä `init.sls`-tiedoston uuteen `apache`-kansioon, jolla voin ladata, konfiguroida ja käynnistää Apachen. Lisäsin samalla osion, joka käskee apachea pyörimään orjan ip-osoitteessa, jotta voisin tarkistaa sen herralla. Ajoin tilakomennon saltilla, ja käytin `curl`-komentoa tarkastaakseni lopputuloksen.

![image](https://github.com/user-attachments/assets/2f48a659-4c65-4ca5-adde-d147c9632bbd)

_Apache init.sls konfigurointi_

![image](https://github.com/user-attachments/assets/e0650203-d226-4cf1-ac3d-de145283da20)

_Idempotentti Apache_

![image](https://github.com/user-attachments/assets/7d60e4ab-fb76-4422-949b-53eb96df55f2)

_Orjan Apache herran koneelta_

Poistin seuraavaksi Apachen ja siiryyin seuraavaan tehtävään.

## SSH (Kohta B)

Lisäsin ensin SSH-portin manuaalisesti. Tämä järjestyi muokkaamalla konfigurointitiedostoa osoitteessa `/etc/ssh/sshd_config`. Konfigurointitiedostossa portti 22 (vagrant) on mainittu, mutta sen konfigurointi on jätetty kommentiksi. Tästä voisi päätellä, että se on oletuksena käytössä jo jonkun muun reitin kautta. Poistin kommentit ja lisäsin satunnaisen portin (tässä tapauksessa 2222) kokeilua varten.

![image](https://github.com/user-attachments/assets/1f70affb-e107-4cb6-9757-4764d467a2cc)

_SSH-konfigurointi_

Tarkastin seuraavaksi portin olevan auki `netcat`-työkalulla.

![image](https://github.com/user-attachments/assets/411809db-d8ce-4255-842c-2cbdcd9a1718)

Portti 22 ja 2222 ovat auki kuten määrittelin, kun taas hypoteettinen portti 2221 on kiinni.
