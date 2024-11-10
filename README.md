# TP MITM SSH
## Objectif
Ce dépôt contient un fichier Vagrantfile permettant la création d'un réseau de 3 VMs . Ces VMs permettent le test d'une attaque "Man-in-the-middle" sur le SSH.
1. Cloner le répertoire :
```bash
git clone https://github.com/bouhenic/tpssh
cd tpssh
```
2. Créer et lancer les VM :
```bash
vagrant up
```
3. Connexion aux VMs :
Connexion à la VM "alice"
```bash
vagrant ssh alice -- -X
```
-- -X sert à utiliser X11 de la machine host pour lancer les applications graphiques.
Connexion à la VM "bob"
```bash
vagrant ssh bob -- -X
```
Connexion à la VM "eve"
```bash
vagrant ssh eve
```
