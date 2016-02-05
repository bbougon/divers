#Installer un container debian 7 (sur une debian 8)
L'installation d'un container diffère d'un container à un autre. 
Il faut savoir qu'il n'y a pas de container ubuntu embarqué avec LXC pour debian. 
La documentation suivante est la seule qui a fonctionné sur mon système (http://blog.roxing.net/lxc-debian-jessie).

## Pré-requis

````
apt-get install bridge-utils
````

## Installation du container debian 7 (wheezy) 
la commande ci-dessous installe un container debian 7 wheezy et récupère le mot de passe généré lors
de l'installation dans le fichier password.txt
 ````
sudo lxc-create -t debian -n $CONTAINER  -P $CONTAINERS_PATH -- --release wheezy 2>/dev/null | sed '$!d' | sed "s/^[^']*'//;s/'.*$//" > password.txt
```

## Configuration de l'interface réseau du container

```
lxc.network.type = veth                     # on veut du virtual ethernet
lxc.network.name = veth0                    # le nom que va porter notre interface
lxc.network.veth.pair = veth0
lxc.network.flags = up
lxc.network.link = br0                      # on se lie à l'interface br0 (comme bridge) déclarée sur l'hôte
lxc.network.hwaddr = 00:FF:AA:00:00:01      # une valeur comme une autre d'adresse MAC
lxc.network.ipv4 = 192.168.10.1/24          # adresse IP de réseau local
lxc.network.ipv4.gateway = 10.33.2.246      # adresse IP de l'hôte
````

## Configuration du réseau de l'hôte

### Autoriser l'ip forwarding 
````
vi /etc/sysctl.conf 
net.ipv4.ip_forward=1
```

Recharger la configuration 

````
sysctl -p
```

## Configuration de l'interface réseau de l'hôte 

````
auto br0
iface br0 inet static
    bridge_ports none 
    bridge_fd 0
    bridge_maxwait 0
    address 192.168.10.254      # adresse statique du bridge
    netmask 255.255.255.0
````

### Activer le partage de connexion 

````
iptables -t nat -F POSTROUTING
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

## Démarrer le container (en tant que daemon)

````
sudo lxc-start -n $CONTAINER -P $CONTAINERS_PATH -d
```

## Vérifier l'état du container

````
sudo lxc-ls -f -P sudo lxc-ls -f -P
````

retourne un tableau :
NAME  STATE    IPV4          IPV6  AUTOSTART  
--------------------------------------------
nfc   RUNNING  192.168.10.1  -     NO

## Se connecter au container

```
sudo lxc-console -n $CONTAINER -P kmDarQlO
````

## Arrêter le container

````
sudo lxc-stop -n $CONTAINER -P $CONTAINERS_PATH
```

