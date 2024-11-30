# h4 Puolikas

## Johdanto

Tehtävässä h4 tuli tehdä ensimmäinen vedos kurssilla tehtävästä moduulista. Moduulin tulisi kattaa kursilla opittuja tekniikoita. Tätä varten valitsin luoda ympäristön, jossa `Wireguard`-sovelluksen avulla luodaan turvallinen yhteys palvelimeen, joka on muuten ulottumattomissa. Wireguardin konfigurointi tehdään kokonaan hyödyntämällä Saltin toimintoja.

![image](https://github.com/user-attachments/assets/9fce1332-ce2d-4c29-bb97-4a146721bff9)

_Alustava suunnitelma_

## Palvelimet

Käytin palvelinten asentamiseen Vagranttia, sillä se on tehokas tapa luoda uusia palvelimia projektia varten ja se sopii hyvin kurssin `Infrastructure as code`-teemaan. Asensin ensin kahdet palvelimet, joista toinen on palvelin johon muodostetaan VPN yhteys ja toinen on palvelin, johon Wireguard konfiguroidaan.

Asensin palvelimet uuteen kansioon `wireguard-project`. Vagranttia varten loin konfigurointitiedoston `Vagrantfile`. Tiedoston luomisen jälkeen palvelimet voi luoda komennolla `vagrant up`.

![image](https://github.com/user-attachments/assets/eabce949-dd06-4898-bb92-629273c23fc9)

_Ensimmäset palvelimet_

![image](https://github.com/user-attachments/assets/2daef2eb-2277-473c-8355-abd4779d2a53)

_vagrant created_

### Lähteet

https://terokarvinen.com/2023/salt-vagrant/

## Wireguard manuaalisesti

Wireguardin asennukseen löytyi ohjeet sen omilta sivuilta. Aloitin lataamalla sen molemmille palvelimille komennolla `sudo apt-get install wireguard` Tämän jälkeen tein myös yhteyskokeilut virtuaalikoneiden välillä.

![image](https://github.com/user-attachments/assets/8f814c68-6544-4995-90cd-531b17906a6a)

_vagrant@server_

![image](https://github.com/user-attachments/assets/f2be1b05-c23c-4600-bfa7-bc3f031fde66)

_vagrant@client_

Seuraavaksi loin avaimet yhteyttä varten molemmilla koneilla.

![image](https://github.com/user-attachments/assets/fafaf1a1-28df-4cfd-bcf3-35b2964cd935)


### Lähteet

https://www.wireguard.com/quickstart/

## Wireguard Saltilla

Valmis moduuli vaatii vielä tämän lataamisen, konfiguroinnin ja ajamisen Saltin avulla. Suunnitelmissa oli tehdä näistä kolmesta omat `.sls`-tiedostot, jotka ajan yhdellä `.top`-tilalla. Jos moduuli osoittautuu Saltin osalta helpoksi, voin vielä lisätä monia ominaisuuksia, jotka tekevät VPN-yhteydestä vielä turvallisemman.

### Yleiset lähteet

Pohjana Tero Karvinen 2024: Palvelinten hallinta -kurssi, http://terokarvinen.com

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
