# Script-Nmap Guide de référence Nmap

Nmap (Network Mapper) est un outil de cartographie de réseaux qui analyse les paquets IP pour identifier les périphériques connectés, leurs services et systèmes d'exploitation. Utilisé par les administrateurs réseau, il permet de réaliser des scans de ports, de détecter des hôtes actifs et d'obtenir des informations détaillées sur les configurations réseau.


### Nmap Cheat Sheet

#### Types de scans:

* **Null scan** : n'envoie aucun flag TCP.

* **FIN scan** : envoie uniquement le flag FIN.

* **Noël scan** : envoie les flags FIN, PSH et URG.

### 🔧 Découverte d'Hôtes

Portée du Réseau

          sudo nmap 192.16.200.0/24 -sn -oA tnet | grep for | cut -d" " -f5

Scanner une Liste d'Adresses IP

          cat hosts.lst  
          sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5

Scanner Plusieurs Adresses IP

          sudo nmap -sn -oA tnet 192.16.200.18 192.16.200.19 192.16.200.20 | grep for | cut -d" " -f5  
          sudo nmap -sn -oA tnet 192.16.200.18-20 | grep for | cut -d" " -f5

Scanner une Seule Adresse IP

          sudo nmap 192.16.200.18 -sn -oA host

Scan avec Requêtes ICMP Echo

          sudo nmap 192.16.200.18 -sn -oA host -PE --packet-trace

Afficher la Raison de Détection de l'Hôte

          sudo nmap 192.16.200.18 -sn -oA host -PE --reason

Désactiver les Pings ARP

          sudo nmap 192.16.200.18 -sn -oA host -PE --packet-trace --disable-arp-ping

### 🔧 Analyse des Hôtes et Ports

Scan Agressif avec Détection de Versions

          sudo nmap 192.16.200.28 -p 80 -A
     
### 🔧 Moteur de Script Nmap (NSE)

Scripts par Défaut

          sudo nmap <target> -sC

Catégorie de Scripts Spécifiques

          sudo nmap <target> --script <category>

Scripts Définis

          sudo nmap <target> --script <script-name>,<script-name>

Spécification de Scripts

          sudo nmap 192.16.200.28 -p 25 --script banner,smtp-commands

Évaluation de Vulnérabilité

          sudo nmap 192.16.200.28 -p 80 -sV --script vuln

### 🕵️ Exemples Avancés

Scan Détaillé avec Détection de Services

          nmap 192.16.200.211 -p 80 -A -sV --script http-enum

Scan Rapide Super Efficace

          nmap -sCV -v -p- -T5 192.16.200.158

Scan de Présence d'Hôtes sur un Réseau

          nmap -sn 192.16.200.0/24

Scan de Version avec Liste de Cibles et Export

          nmap -sV -p- -iL targets -oN nmap.initial -v

Scan Agressif

          nmap -A -p- -iL targets -oN nmap.aggressive -v

Scan des Vulnérabilités

          nmap -p --script=vuln -v

Scan pour Éviter la Détection par IDS/IPS

          nmap -sn -T0 192.16.200.0/24

Analyse de Découverte d'Hôtes

          nmap -sn 192.16.200.0/24

### 🔎 Options d'Analyse Spécifiques

* Analyse de Connexion TCP (-sT)

* Analyse UDP (-sU)

* Analyse TCP FIN (-sF)

* Analyse de Découverte d'Hôtes (-sn)

* Options de Synchronisation (-T0 à -T5)

### 🛠️ Commandes Courantes

Scanner Tout un Réseau

          nmap 192.16.200.0/24

Détection du Système d'Exploitation, Nom et Adresse MAC

          nmap -O 192.16.200.1

Scan Avancé avec Détection de Version, Traceroute et Scripts

          nmap -A 192.16.200.17

Afficher l'Aide Complète

          nmap --help

Scan de Tous les Ports avec Noms de Serveurs

          nmap -p 1-65535 -T4 -A -v tech.teck

### Techniques d'Évasion et d'Usurpation

Scan Furtif avec Fragmentation des Paquets

          nmap -f

Utilisation de Leurres pour Masquer l'Origine

          nmap -D RND:10 192.16.200.1

Usurpation d'Adresse Source

          nmap -S 192.16.200.100

### 🛠️ Exemples Avancés

Scan des Failles HTTP

          nmap 192.16.200.130 -p 80 --script vuln

Scan avec Plusieurs Scripts

          nmap -p 80 --script http-fileupload-exploiter --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'

Scan des Utilisateurs et Partages SMB

          nmap -A -Pn --script smb-enum-users.nse --script smb-enum-shares.nse -p139,445,21 -T4 192.16.200.23

### ✉️ Exportation des Résultats

Enregistrer les Résultats dans Plusieurs Formats

          nmap -oA report 192.16.200.23

Transformation XML en HTML

          xsltproc report.xml -o report.html

Export Format Normal

          nmap -oN normal_scan.txt

Export Format Grepable

          nmap -oG grepable_scan.txt

### ⚖️ Commutateurs Clés

* Syn Scan: **-sS**

* Analyse UDP: **-sU**

* Détection du Système d'Exploitation: **-O**

* Détection de la Version des Services: **-sV**

* Verbosité: **-v, -vV**

* Export des Résultats dans Trois Formats: **-oA**

* Scan Mode Agressif: **-A**

* Définition du Modèle de Timing à 5: **-T5**

* Scan d'un Port Spécifique: **-p 80**

* Scan d'une Plage de Ports: **-p 100-1500**

* Scan de Tous les Ports: **-p-**

* Activation d'un Script: **--script**

* Activation des Scripts de la Catégorie "vuln": **--script=vuln**



## Conclusion

Pour plus d'informations, référez-vous à la [documentation officielle](https://nmap.org/book/man.html) de Nmap qui fournit une mine d'informations pour maîtriser pleinement cet outil indispensable pour la sécurité informatique.


## ⚠️ Disclaimer :

> [!Important]
> Nmap est un outil puissant et polyvalent pour l'analyse réseau, la découverte d'hôtes et l'identification des vulnérabilités. Son efficacité repose sur une bonne maîtrise des commandes adaptées à chaque contexte. Une utilisation éthique et responsable est essentielle, car la frontière entre sécurité et intrusion est fine.

> Son usage légitime inclut :

* Des tests d'intrusion autorisés avec l'accord explicite des propriétaires des systèmes ;
* Des analyses de sécurité dans le cadre de missions légales avec consentement ;
* Des tests en laboratoire sur des environnements contrôlés.

> Toute utilisation non autorisée pour analyser ou compromettre des systèmes est illégale et peut entraîner des sanctions civiles et pénales. Je décline toute responsabilité pour tout usage inapproprié de cet Cheat Sheet.
>

Auteur : [ ATTEIB.H (LinkedIn)](https://www.linkedin.com/in/atteib-h-birackinit-83a657221/).
