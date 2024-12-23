# h1 Viisikko
Tehtävässä h1 oli tarkoituksena kokeilla Salt-ohjelmaa Linuxissa. Olin asentanut etukäteen Debian 12-Bookworm:in virtuaalikoneeseen, joten en avannut sen latausprosessia tässä.

## Tiivistykset
Ennen tehtävän aloittamista kävin läpi annetut materiaalit ja tiivistin niistä ydinkohdat;

1. Run Salt Command Locally

   -Saltia kannattaa kokeilla aluksi paikallisesti (Master ja Minion samalla koneella).
   
   -Saltissa on viisi erityisen tärkeää komentoa; pkg, file, service, user ja cmd.
   
2. Salt Quickstart

   -Salt on hyödyllinen, sillä sen avulla voidaan hallita lukuisia koneita niiden sijainnista huolimatta.
   
   -Saltissa pääsee alkuun lataamalla sen, konfaamalla minionin ja hyväksymällä minionin avaimen masterilla.

3. Raportin kirjoittaminen
   
   -Raportointi on hyvä niin muiden kuin itsensäkin kannalta. Se toimii hyvin myös muistiinpanoina omaa toimintaa varten.

   -Raportin tulisi olla täsmällinen, jotta vianselvitys olisi mahdollisimman helppoa.

   -Lähteet, tekstin selkeys ja raportin rakenne tulisi olla hallussa.

## Salt:in asennus ja testaus
Aloitin tämän jälkeen Saltin asentamisen ja testaamisen. Ohjeissa huomioitiin, että Salt edellyttää uuden pakettivaraston asentamista, joten tein tämän ohjeiden mukaisesti.

![image](https://github.com/user-attachments/assets/24c5fd91-47ac-4c17-922c-d0eb746bc513)

*Uuden pakettivaraston asennus*

Seuraavaksi asensin herran ja orjan virtuaalikoneelleni komennolla "sudo apt-get -y install salt-minion salt-master". Tämän jälkeen innostuksissaan herpaannuin katsomaan heti miten localhost herra-orja yhteys toimii. 

Komennolla "sudo nano /etc/salt/minion" pääsemme muokkaamaan "master" kohdan kommentista koodiksi ja korvaamaan sen kohteella "localhost". Nyt tarvitsin enää nopean "systemctl restart" minionille ja sitten "systemctl start" molemmille osapuolille. 

Viimeisessä vaiheesssa komento "sudo salt key -A" hyväksyi vielä minionin avaimen. Nopea yhteyskokeilu todisti yhteyden toimivan.

![image](https://github.com/user-attachments/assets/723a9c32-77f2-4e51-bff1-410515dc6828)

*Yhteyskokeilu*

Nyt kun tehtävän viimeinen kohta oli tehty, pystyin palata olennaiseen eli Saltin tilafunktioiden ja idempotentin testaamiseen. 

Käytin ensimmäiseksi "pkg.installed" tilafunktiota "tree" työkalun lataamiseksi minionille. Demonstroin samalla idempotenssin, sillä saman komennon suorittaminen uudestaan ei tee mitään.

![image](https://github.com/user-attachments/assets/020de379-5f1c-4f6e-b33e-582c89f0da3c)

*pkg.install komento*

![image](https://github.com/user-attachments/assets/70bd741d-ee02-4323-8123-a74e1c5a7ba8)

*Idempotenssi demonstraatio*

Kokeilin seuraavaksi "file" komennolla tiedoston luomista ja muokkaamista.

![image](https://github.com/user-attachments/assets/d9377b77-d634-4d81-958a-1eb38159034f)

*Tiedoston luominen*

![image](https://github.com/user-attachments/assets/f221922b-eefe-4241-b8c2-e578917ded5f)

*Tiedoston sisällön muokkaaminen*

![image](https://github.com/user-attachments/assets/d75d80d2-7ab8-4654-a5b6-d1c5012a103d)

*Luodun tiedoston lukeminen*

Tämän jälken kokeilin "service" tilafunktiota. En ollut vielä asentanut esim. Apache2:sta, joten ajoin ylös ja alas sen sijaan "cups" tulostusohjelman. Ylös ajaessa sain taas demonstroitua idempotenssia, sillä valmiiksi päällä olevan ohjelman ylösajo ei tuota muutoksia.

![image](https://github.com/user-attachments/assets/883b5f2f-26a3-42ce-9001-ff0a348690c5)

*Idempotenssi demostraatio 2 / cups ylösajo*

![image](https://github.com/user-attachments/assets/8102627e-b200-4600-881f-7d6714d23f72)

*Cups alasajo*

Tein ja poistin myös käyttäjän "user" tilafunktiolla.

![image](https://github.com/user-attachments/assets/27d03688-c015-4d6e-a49c-1dc8f14bd38f)

*Käyttäjä luotu*

![image](https://github.com/user-attachments/assets/ebd588c8-861f-4f6f-9ab2-a29d70e3230f)

*Käyttäjä poistettu*

Lopuksi demonstroin "cmd" tilafunktiota. Tämä tulisi suorittaa aikaisemmilla tilafunktioilla silloin kuin mahdollista (esimerkiksi tässä kohtaa "user"), sillä cmd ei varmista itsessään idempotenssia. "creates=" osio takaa tässä osassa idempotenssin.

![image](https://github.com/user-attachments/assets/24d5c165-aa9c-4e2f-a014-f58d28e2e9be)

*Luodaan testitiedosto cmdillä*

![image](https://github.com/user-attachments/assets/c1feb89b-aaa5-46e3-b018-b0e7a240ac98)

*Tiedosto luotu*

## Lähteet

Karvinen, Tero 2021. Run Salt Command Locally. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu 28.10.2024

Karvinen, Tero 2018. Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux. Luettavissa: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/. Luettu 28.10.2024

Karvinen, Tero 2006. Raportin kirjoittaminen. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu 28.10.2024

Pohjana Tero Karvinen 2024: Palvelinten hallinta -kurssi, http://terokarvinen.com

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html
