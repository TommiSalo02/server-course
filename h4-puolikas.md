# h4 Puolikas

## Johdanto

Tehtävässä h4 tuli tehdä ensimmäinen vedos kurssilla tehtävästä moduulista. Moduulin tulisi kattaa kursilla opittuja tekniikoita. Tätä varten valitsin luoda ympäristön, jossa `Wireguard`-sovelluksen avulla luodaan turvallinen yhteys palvelimeen, joka on muuten ulottumattomissa. Wireguardin konfigurointi tehdään kokonaan hyödyntämällä Saltin toimintoja.

![image](https://github.com/user-attachments/assets/9fce1332-ce2d-4c29-bb97-4a146721bff9)

_Alustava suunnitelma_

## Palvelimet osa 1.

Käytin palvelinten asentamiseen Vagranttia, sillä se on tehokas tapa luoda uusia palvelimia projektia varten ja se sopii hyvin kurssin `Infrastructure as code`-teemaan. Asensin ensin kahdet palvelimet, joista toinen on palvelin johon muodostetaan VPN yhteys ja toinen on palvelin, johon Wireguard konfiguroidaan.

Asensin palvelimet uuteen kansioon `wireguard-project`. Vagranttia varten loin konfigurointitiedoston `Vagrantfile`. Tiedoston luomisen jälkeen palvelimet voi luoda komennolla `vagrant up`.

![image](https://github.com/user-attachments/assets/eabce949-dd06-4898-bb92-629273c23fc9)

_Ensimmäset palvelimet_

![image](https://github.com/user-attachments/assets/42969de1-8994-4839-86ab-a3613e220279)

_vagrant up_

Palvelinten luomisen jälkeen asensin `Wireguard`-sovelluksen

### Lähteet

https://terokarvinen.com/2023/salt-vagrant/

## Wireguard manuaalisesti

Wireguardin asennukseen löytyi ohjeet sen omilta sivuilta. 

### Lähteet

https://www.wireguard.com/quickstart/

## Palvelimet osa 2.

## Wireguard Saltilla
