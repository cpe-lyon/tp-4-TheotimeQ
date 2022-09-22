**Quere Theotime 3ICS**

# Table des matières

[ Exercice 1. Commandes de base](#Anch1)

[Exercice 2.](#Anch2)

[Exercice 3.](#Anch3)

# Exercice 1. Commandes de base<a id='Anch1'></a>

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
User@localhost:~$ cat /etc/group
```

## 4. Listez les derniers paquets qui ont été installés explicitement avec la commande apt install

```console
User@localhost:~$ cat /etc/group
```

## 5. Utilisez les commandes dpkg et apt pour compter de deux manières différentes le nombre de total de paquets installés sur la machine (ne pas hésiter à consulter le manuel !). Comment explique-t-on la (petite) différence de comptage ? Pourquoi ne peut-on pas utiliser directement le fichier dpkg.log ?

```console
User@localhost:~$ cat /etc/group
```

## 6. Combien de paquets sont disponibles en téléchargement sur les dépôts Ubuntu ?

```console
User@localhost:~$ cat /etc/group
```

## 7. A quoi servent les paquets glances, tldr et hollywood ? Installez-les et testez-les.

```console
User@localhost:~$ cat /etc/group
```

## 8. Quels paquets proposent de jouer au sudoku ? ! N’installez pas le paquet gnome-sudoku ou ksud

```console
User@localhost:~$ cat /etc/group
```








## 1. Utilisez la commande groupadd pour créer deux groupes dev et infra

```console
User@localhost:~$ sudo groupadd dev
User@localhost:~$ sudo groupadd infra
```

```console
User@localhost:~$ cat /etc/group
```

![](/TP2_IMG/TP3_1.png)
