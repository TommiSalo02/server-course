# h5 Loppuhuipennus

## Johdanto

Tehtävässä h5 tuli tehdä oma moduuli esitysvalmiiksi. Aloitin oman Wireguard projektin viime viikolla tehtävässä h4. Siinä osiossa sain kaiken toimimaan manuaalisesti, elikkä Wireguard yhteys ja Salt olivat testattu halutussa konfiguraatiossa. Seuraavaksi pyrin tekemään mahdollisimman paljon tästä asennuksesta automaattisesti Saltilla. Kolmas vaihe olisi automatisoida myös Saltin asennus, jolloin projektin voisi kloonata gitistä ja sen voisi saada pystyyn vain muutamalla komennolla. 

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

Viimeinen vaihe on Wireguardin lataaminen, konfigurointi ja käynnistäminen. Tämä voidaan automatisoida Saltin avulla. Aluksi tuli luoda uusi kansio `/srv/salt`, johon voin luoda Saltin tiedostot. Kokeilin ensin ajaa yksinkertaisen Wireguardin asennus `init.sls`-tiedoston `wireguard`-kansiosta, jotta näkisin, että homma toimii.

![image](https://github.com/user-attachments/assets/627ee475-211b-4da7-baed-110b0ce23926)

![image](https://github.com/user-attachments/assets/663c15e0-ecb2-4d4c-9fae-a3cb4c316ad5)

Molemmat palvelimet latasivat työkalun ja ovat idempotenssissa. Tästä oli hyvä jatkaa eteenpäin.

Seuraava osuus oli yksityisten ja julkisten avaimen luominen, sillä niitä tarvitsee konfiguroinnissa. Loin uuden kansion `keygen`, jossa `init.sls`-tiedosto luo uudet avaimet uuteen kansioon `/etc/wireguard/keys`.

```
# Create key directory
create-key-directory:
  file.directory:
    - name: /etc/wireguard/keys
    - user: root
    - group: root
    - mode: 700

# Generate private key
generate-private-key:
  cmd.run:
    - name: wg genkey | tee /etc/wireguard/keys/privatekey
    - creates: /etc/wireguard/keys/privatekey
    - require:
        - file: create-key-directory

# Generate public key
generate-public-key:
  cmd.run:
    - name: cat /etc/wireguard/keys/privatekey | wg pubkey > /etc/wireguard/keys/publickey
    - creates: /etc/wireguard/keys/publickey
    - require:
        - cmd: generate-private-key
```

Tätä varten piti käyttää `cmd.run`-toimintoa, mutta lisätyt vaatimukset tekevät koodista idempotentin siitä huolimatta.

![image](https://github.com/user-attachments/assets/058c020d-ed97-4405-ac5d-ccf20fead646)

Seuraavaksi tuli ajaa itse konfigurointi-tiedostot `client` ja `server` -palvelimille `master`-palvelimelta. Tein tätä varten `top.sls`-tiedoston joka ajaa kummallekin palvelimelle oman konfiguraationsa. Tämä ei ollut skaalautuva tapa, mutta se toimii väliaikaisesti.

![image](https://github.com/user-attachments/assets/04a2a6fd-c25f-4906-bbbe-869a53e76265)

```
[Interface]
PrivateKey = ePzWO9Lo+0wthHDAVBnv03Wz80ZmI3iJ2xIm6XZQomc=
Address = 10.0.0.2/24
SaveConfig = true

[Peer]
PublicKey = KYhT627CQnCsibVZnkf3MWQQvWGIYc1SRUrf/WY2eFM=
Endpoint = 192.168.12.101:51820
AllowedIPs = 10.0.0.0/24
```

```
PrivateKey = +JoRmz8hdzJnfczRv2OszVH6hnPGFBTa8C7WTSjS+W8=
Address = 10.0.0.1/24
ListenPort = 51820
SaveConfig = true

[Peer]
PublicKey = 3LWT2huMiLbgZ+LEmd11aZkGfcTQ9+l+tlDkHEsqOkY=
AllowedIPs = 10.0.0.2/32
```

Näistä konfigurointi-tiedostoista puuttuu aluksi vielä avaimet, joten lisäsin ne manuaalisesti. Avainten nouto palvelimilta konfiguraatioon oli projektin teknisesti haastavin osio.

### Lähteet
https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/linux-deb.html
