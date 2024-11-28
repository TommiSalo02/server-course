# h4 Puolikas

## Johdanto

Tehtävässä h4 tuli tehdä ensimmäinen vedos kurssilla tehtävästä moduulista. Moduulin tulisi kattaa kursilla opittuja tekniikoita. Tätä varten valitsin luoda ympäristön, jossa `Wireguard`-sovelluksen avulla luodaan turvallinen yhteys palvelimeen, joka on muuten ulottumattomissa. Wireguardin konfigurointi tehdään kokonaan hyödyntämällä Saltin toimintoja.

![image](https://github.com/user-attachments/assets/9fce1332-ce2d-4c29-bb97-4a146721bff9)

_Alustava suunnitelma_

## Palvelimet osa 1.

Käytin palvelinten asentamiseen Vagranttia, sillä se on tehokas tapa luoda uusia palvelimia projektia varten ja se sopii hyvin kurssin `Infrastructure as code`-teemaan. Asensin ensin kahdet palvelimet, joista toinen on palvelin johon muodostetaan VPN yhteys ja toinen on palvelin, johon Wireguard konfiguroidaan.

## Wireguard manuaalisesti

## Palvelimet osa 2.

## Wireguard Saltilla

## Liitteet

Liite 1: Palvelimet osa 1. asennus

```
# -*- mode: ruby -*-
# vi: set ft=ruby :
# Copyright 2014-2023 Tero Karvinen http://TeroKarvinen.com

$minion = <<MINION
sudo apt-get update
sudo apt-get -qy install salt-minion
echo "master: 192.168.12.3">/etc/salt/minion
sudo service salt-minion restart
echo "See also: https://terokarvinen.com/2023/salt-vagrant/"
MINION

$master = <<MASTER
sudo apt-get update
sudo apt-get -qy install salt-master
echo "See also: https://terokarvinen.com/2023/salt-vagrant/"
MASTER

Vagrant.configure("2") do |config|
	config.vm.box = "debian/bullseye64"

	config.vm.define "t001" do |t001|
		t001.vm.provision :shell, inline: $minion
		t001.vm.network "private_network", ip: "192.168.12.100"
		t001.vm.hostname = "t001"
	end

	config.vm.define "t002" do |t002|
		t002.vm.provision :shell, inline: $minion
		t002.vm.network "private_network", ip: "192.168.12.102"
		t002.vm.hostname = "t002"
	end

	config.vm.define "tmaster", primary: true do |tmaster|
		tmaster.vm.provision :shell, inline: $master
		tmaster.vm.network "private_network", ip: "192.168.12.3"
		tmaster.vm.hostname = "tmaster"
	end
end
```
