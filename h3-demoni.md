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

Seuraavaksi käytin komentoa `sudo apt-get remove apache2` poistaakseni Apachen. Tämän jälkeen voin tehdä `.sls`-tiedoston, jolla voin ladata, konfiguroida ja käynnistää Apachen.
