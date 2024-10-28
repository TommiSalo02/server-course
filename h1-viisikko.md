# h1 Viisikko
Tällä kertaa tehtävässä h1 oli tarkoituksena kokeilla Salt-ohjelmaa Linuxissa. Olin asentanut etukäteen Debian 12-Bookworm:in virtuaalikoneeseen, joten en avannut sitä prosessia tässä.

## Tiivistykset
Ennen tehtävän aloittamista kävin läpi annetut materiaalit ja tiivistän niiden ydinkohdat tähän;

1. Run Salt Command Locally

   -Salt:tia kannattaa kokeilla aluksi paikallisesti (Master ja Minion samalla koneella)
   
2. Salt Quickstart

   -Salt on hyödyllinen, sillä sen avulla voin hallita lukuisia koneita niiden sijainnista huolimatta.

3. Raportin kirjoittaminen
   -Raportointi on hyvä niin muiden kuin itsensäkin kannalta. Se toimii myös muistiinpanoina omaa toimintaa varten.

   -Raportin tulisi olla täsmällinen, jotta vianselvitys olisi mahdollisimman helppoa.

   -Lähteet, tekstin selkeys ja raportin rakenne tulisi olla hallussa.

## Salt:in asennus ja testaus
Aloitin tämän jälkeen Salt:in asentamisen ja testaamisen. Ohjeissa huomioitiin, että Salt edellyttää uuden pakettivaraston asentamista, joten tein tämän ohjeiden mukaisesti.

![image](https://github.com/user-attachments/assets/24c5fd91-47ac-4c17-922c-d0eb746bc513)
*Uuden pakettivaraston asennus*

Seuraavaksi asensin herran ja orjan virtuaalikoneelleni komennolla "sudo apt-get -y install salt-minion TAI salt-master". Tämän jälkeen on tärkeää innostuksissaan herpaantua kokonaan tehtävän ohjeista ja katsoa miten herra-orja localhost yhteys toimii. 

Komennolla "sudo nano /etc/salt/minion" pääsemme muokkaamaan "master" kohdan kommentista koodiksi ja korvaamaan sen kohteella "localhost". Nyt tarvitsin enää nopean "systemctl restart" minion:ille ja sitten "systemctl start" molemmille osapuolille. 

Viimeisessä vaiheesssa komento "sudo salt key -A" hyväksyi vielä minion:in avaimen. Nopea yhteyskokeilu todisti yhteyden toimivan.

![image](https://github.com/user-attachments/assets/723a9c32-77f2-4e51-bff1-410515dc6828)
*Yhteyskokeilu*

Nyt kun tehtävän viimeinen kohta oli tehty, pystyin palata olennaiseen eli Saltin tilafunktioiden ja idempotentin testaamiseen. Käytin ensimmäiseksi "pkg.installed" tila funktiota "tree" työkalun lataamiseksi minionille. Demonstroin samalla idempotenssin, sillä saman komennon suorittaminen uudestaan ei tee mitään.

![image](https://github.com/user-attachments/assets/020de379-5f1c-4f6e-b33e-582c89f0da3c)
*pkg.install komento*

![image](https://github.com/user-attachments/assets/70bd741d-ee02-4323-8123-a74e1c5a7ba8)
*idempotenssi demonstraatio*

Kokeilin seuraavaksi "file" komennolla tiedoston luomista ja muokkaamista.

![image](https://github.com/user-attachments/assets/d9377b77-d634-4d81-958a-1eb38159034f)

![image](https://github.com/user-attachments/assets/f221922b-eefe-4241-b8c2-e578917ded5f)

![image](https://github.com/user-attachments/assets/d75d80d2-7ab8-4654-a5b6-d1c5012a103d)

Service

![image](https://github.com/user-attachments/assets/883b5f2f-26a3-42ce-9001-ff0a348690c5)
idempotenssi / cups

![image](https://github.com/user-attachments/assets/8102627e-b200-4600-881f-7d6714d23f72)
cups 2

luodaan ja poistetaan tommi 2

![image](https://github.com/user-attachments/assets/27d03688-c015-4d6e-a49c-1dc8f14bd38f)

![image](https://github.com/user-attachments/assets/ebd588c8-861f-4f6f-9ab2-a29d70e3230f)

cmd höpötystä

![image](https://github.com/user-attachments/assets/24d5c165-aa9c-4e2f-a014-f58d28e2e9be)
![image](https://github.com/user-attachments/assets/c1feb89b-aaa5-46e3-b018-b0e7a240ac98)



## Tiivistelmä

## Lähteet
