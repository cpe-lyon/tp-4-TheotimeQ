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


# Exercice 2. <a id='Anch1'></a>

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

echo $(dpkg -S ls | grep "/ls$" 2> /dev/null | cut -d " " -f1 | tr ":" "\n")
```



![](/TP2_IMG/TP3_1.png)
