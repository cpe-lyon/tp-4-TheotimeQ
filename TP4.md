**Quere Theotime 3ICS**

# Table des matières

[ Exercice 1. Commandes de base](#Anch1)

[Exercice 2.](#Anch2)

[Exercice 3.](#Anch3)

[Exercice 4.](#Anch4)

[Exercice 5. aptitude](#Anch5)

[Exercice 6. Installation d’un paquet par PPA](#Anch6)

[Exercice 7. Installation d’un logiciel à partir du code source](#Anch7)

[Exercice 8. Création de dépôt personnalisé](#Anch8)

# Exercice 1. Commandes de base <a id='Anch1'></a>

## 1. Commencez par mettre à jour votre système avec les commandes vues dans le cours.

```console
User@localhost:~$ apt-get upgrade
```

## 2. Créez un alias “maj” de la ou des commande(s) de la question précédente. Où faut-il enregistrer cet alias pour qu’il ne soit pas perdu au prochain redémarrage ?

Il faut mettre la commande d'allias dans .bashrc

```console
alias maj='apt-get upgrade'
```

## 3. Utilisez le fichier /var/log/dpkg.log pour obtenir les 5 derniers paquets installés sur votre machine.

```console
User@localhost:~$ grep installed /var/log/dpkg.log | tail -n5 | cut -d' ' -f5 | cut -d: -f1
```

## 4. Listez les derniers paquets qui ont été installés explicitement avec la commande apt install

```console
User@localhost:~$ grep "apt install" /var/log/apt/history.log | cut -d ' ' -f4
```

## 5. Utilisez les commandes dpkg et apt pour compter de deux manières différentes le nombre de total de paquets installés sur la machine (ne pas hésiter à consulter le manuel !). Comment explique-t-on la (petite) différence de comptage ? Pourquoi ne peut-on pas utiliser directement le fichier dpkg.log ?

Avec dpkg , on compte le nombre de ligne contenant ii
```console
User@localhost:~$ dpkg -l | grep "ii" | wc -l
1512
```

On trouve 1512 paquet 

Avec apt , on a une commande pour avoir directement la liste des paquets installé. On a juste à compter les lignes avec wc.

```console
User@localhost:~$ apt list --installed | wc -l
1513
```

On compte un paquet en lps parce que :

## 6. Combien de paquets sont disponibles en téléchargement sur les dépôts Ubuntu ?

```console
User@localhost:~$ apt list | wc -l
74175
```

Il y as 74175

## 7. A quoi servent les paquets glances, tldr et hollywood ? Installez-les et testez-les.

Glances est une application pour voir les ressources utilisé.
Tldr est une alternative au man 
Hollywood permet de creer une fenettre en mode "hacking"

## 8. Quels paquets proposent de jouer au sudoku ? ! N’installez pas le paquet gnome-sudoku ou ksud

ksudoku permet de jouer au sudoku .

```console
User@localhost:~$ sudo apt install ksudoku
```

# Exercice 2. <a id='Anch2'></a>

## A partir de quel paquet est installée la commande ls ? 

On peut taper : 
```console
User@localhost:~$ dpkg -S ls | grep "/ls$"
coreutils: /bin/ls
klibc-utils: /usr/lib/klibc/bin/ls
```

On trouve que ls est installé depuis coreutils et klibc-utils.

## Comment obtenir cette information en une seule commande, pour n’importe quel programme ? 

Avec la commande `dpkg -S ls | grep "/ls$"`

## Utilisez la réponse à cette question pour écrire un script appelé origine-commande (sans l’extension .sh) prenant en argument le nom d’une commande, et indiquant quel paquet l’a installée.

```bash
#!/bin/bash 

echo $(dpkg -S $1 | grep "/$1$") 2> /dev/null | cut -d " " -f1 | tr ":" "\n"
```

# Exercice 3. <a id='Anch3'></a>

Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package
spécifié dans cette commande.

```bash
dpkg -l | grep "^ksudoku/" && echo "INSTALLE" || echo "NON INSTALLE"
```

# Exercice 4. <a id='Anch4'></a>

Lister les programmes livrés avec coreutils. En particulier, on remarque que l’un deux se nomme

```console
User@localhost:~$ dpkg -S ls | grep "/ls$"
coreutils: /bin/ls
klibc-utils: /usr/lib/klibc/bin/ls
```

# Exercice 5. <a id='Anch5'></a>

Installez les paquets emacs et lynx à l’aide de la version graphique d’aptitude (et prenez deux minutes
pour vous renseigner et tester ces paquets).

- Emacs est un éditeur de texte 
- Lynx est un client World Wide Web 

# Exercice 6. <a id='Anch6'></a>

Certains logiciels ne figurent pas dans les dépôts officiels. C’est le cas par exemple de la version ”officielle”
de Java depuis qu’elle est développée par Oracle. Dans ces cas, on peut parfois se tourner vers un ”dépôt
personnel” ou PPA.
1. Installer la version Oracle de Java (avec l’ajout des PPA)
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update
sudo apt install oracle-java15-installer
2. Vérifiez qu’un nouveau fichier a été créé dans /etc/apt/sources.list.d. Que contient-il ?

Ce fichier contient les reference vers les logiciels APT

```bash
deb http://ppa.launchpad.net/linuxuprising/java/ubuntu focal main
#deb-src http://ppa.launchpad.net/linuxuprising/java/ubuntu focal main
```

# Exercice 7. <a id='Anch7'></a>

```console
User@localhost:~ git clone https://gitlab.com/jallbrit/cbonsai
User@localhost:~ sudo apt install libncursesw5-dev
User@localhost:~ sudo apt install make
```

![](/TP4_IMG/TP4-IMG-4.png)

Une fois l'installation realisé et le checkinstall verifié on peut executer cbonsai n'importe ou.

# Exercice 8. Création de dépôt personnalisé <a id='Anch8'></a>

## Création d’un paquet Debian avec dpkg-deb

1. Dans le dossier scripts créé lors du TP 2, créez un sous-dossier origine-commande où vous créerez un sous-dossier DEBIAN, ainsi que l’arborescence usr/local/bin où vous placerez le script écrit à l’exercice 2

Pour creer l'arborescence correcte , on tape : 
```console
User@localhost:~/Desktop/Package_Perso$ mkdir origin-commande
User@localhost:~/Desktop/Package_Perso$ mkdir origin-commande/DEBIAN
User@localhost:~/Desktop/Package_Perso$ mkdir origin-commande/usr
User@localhost:~/Desktop/Package_Perso$ mkdir origin-commande/usr/local
User@localhost:~/Desktop/Package_Perso$ mkdir origin-commande/usr/local/bin
User@localhost:~/Desktop/Package_Perso$ touch origin-commande/usr/local/bin/script.sh
User@localhost:~/Desktop/Package_Perso$ nano origin-commande/usr/local/bin/script.sh 
User@localhost:~/Desktop/Package_Perso$ bash origin-commande/usr/local/bin/script.sh
```
2. Dans le dossier DEBIAN, créez un fichier control avec les champs suivants :
Package: origine-commande #nom du paquet
Version: 0.1 #numéro de version
Maintainer: Foo Bar #votre nom
Architecture: all #les architectures cibles de notre paquet (i386, amd64...)
Description: Cherche l'origine d'une commande
Section: utils #notre programme est un utilitaire
Priority: optional #ce n'est pas un paquet indispendable

On creer un fichier control avec les bons champs.

3. Revenez dans le dossier parent de origine-commande (normalement, c’est votre $HOME) et tapez la
commande suivante pour construire le paquet :

```console
User@localhost:~/Desktop/Package_Perso$ dpkg-deb --build origine-commande
dpkg-deb: building package 'origine-commande' in 'origine-commande.deb'.
```

Le pacquet est crée !

## Création du dépôt personnel avec reprepro

On creer un dossier repo-cpe

```console
User@localhost:~/Desktop/Package_Perso$ mkdir ~/repo-cpe
```

On ajoute conf et packages

```console
User@localhost:~/Desktop/Package_Perso$ cd ~/repo-cpe
User@localhost:~/Desktop/Package_Perso$ mkdir ~/conf
User@localhost:~/Desktop/Package_Perso$ mkdir ~/packages
```

On creer le fichier distribution :

```bash
Origin: Un nom, une URL, ou tout texte expliquant la provenance du dépôt
Label: Nom du dépôt
// Suite: stable
Codename: focal #!! A MODIFIER selon la distribution cible !!
Architectures: i386 amd64 #(architectures cibles)
Components: universe #(correspond à notre cas)
Description: Une description du dépôt
```

On genere l'arboresence du depot : 
```console
User@localhost:~/repo-cpe$ reprepro -b . export
```

Cela creer tout les dossiers necessaires :
![](/TP4_IMG/TP4-IMG-1.png)

On poursuit la procedure comme expliqué dans le TP4
