# h3 Demoni

## Johdanto

Tehtävässä h3 tuli tutustua Saltin käyttöön Apachen ja OpenSSH:n parissa. Samalla tuli tuumia valmiiksi tulevan moduulin aihetta.

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

## SSH (Kohta B)

Lisäsin ensin SSH-portin manuaalisesti. Tämä järjestyi muokkaamalla konfigurointitiedostoa osoitteessa `/etc/ssh/sshd_config`. Konfigurointitiedostossa portti 22 (vagrant) on mainittu, mutta sen konfigurointi on jätetty kommentiksi. Tästä voisi päätellä, että se on oletuksena käytössä jo jonkun muun reitin kautta. Poistin kommentit ja lisäsin satunnaisen portin (tässä tapauksessa 2222) kokeilua varten.

![image](https://github.com/user-attachments/assets/1f70affb-e107-4cb6-9757-4764d467a2cc)

_SSH-konfigurointi_

Tarkastin seuraavaksi portin olevan auki `netcat`-työkalulla.

![image](https://github.com/user-attachments/assets/411809db-d8ce-4255-842c-2cbdcd9a1718)

Portti 22 ja 2222 ovat auki kuten määrittelin, kun taas hypoteettinen portti 2221 on kiinni.

Seuraavaksi tein saman hyödyntäen `init.sls`-tiedostoa Saltissa. Loin uuden kansion `saltssh`, johon lisäsin `init.sls`-tiedoston. Kopioin tähän tiedostoon ennakkomateriaalin artikkelissa mainitun konfiguraation.

![image](https://github.com/user-attachments/assets/fdb12fdf-85f5-479e-8ba9-7c8773009440)

_SaltSSH init.sls_

Tämä konfiguraatio tarkistaa, että OpenSSH on ladattu, synkronisoi Saltin root-kansiossa olevan `sshd_config`-tiedoston orjalle ja käynnistää `ssh`-palvelun uudestaan.

Kopion vielä aikaisemman `sshd-config`-tiedoston komennolla: `cp /etc/ssh/sshd_config /srv/salt/sshd_config` ja ajoin sen jälkeen tilan orjalle.

![image](https://github.com/user-attachments/assets/6451eec9-670c-4f39-9e2f-d66904147e05)

_Idempotentti saltssh_

Kokeilin lopputuloksia taas `netcat`-työkalulla. Vedin tässä vaiheessa verkon pois kannettavasta, vaikka se ei suoranaisesti olisi tarpeellista. 

![image](https://github.com/user-attachments/assets/557ed08c-ebfa-46d1-a0f4-3263199ccc43)

_Porttikokeilut herralta orjalle_

Porttiasetukset olivat muuttuneet halutulla tavalla Salttia hyödyntäen.

## Apache weppisivu (Kohta D)

Siirryin vielä luomaan Apache-sivun, joka vastaa tehtävän vaatimuksia (tiedostot kotihakemistossa, voi muokata ilman sudoa). Loin ensin käyttäjän "webuser", jonka kotihakemistossa Apache pyörii. Lisäsin tämän käyttäjän kotihakemistoon `public-html`-kansion, johon sisälsin `index.html`-tiedoston. Säädöin samalla käyttöoikeudet kohilleen.

![image](https://github.com/user-attachments/assets/db19908f-c7b6-4afd-8de2-1fc6a66b6caf)

_Tilannekatsaus_

Seuraavaksi suuntasin `VirtualHost`-tiedostoon ja konfiguroin sen `DocumentRoot`-osion omaksi `public-html`-hakemistokseni.

![image](https://github.com/user-attachments/assets/fd78af91-b5e7-488e-9cc1-334a8c031232)

_Apache toiminnassa._

Käytin taas `curl`-työkalua localhost-sivun tarkastelemiseksi. Sivusto oli muuttunut haluamaksemme ja pystyin muokata sitä myös ilman sudo-oikeuksia.



### Lähteet

Digital Ocean: How To Set Up Apache Virtual Hosts on Ubuntu 20.04. Luettavissa: https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-20-04. Luettu 23.11.2024

## Yleiset lähteet

Pohjana Tero Karvinen 2024: Palvelinten hallinta -kurssi, http://terokarvinen.com

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
