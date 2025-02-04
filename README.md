# Script-Nmap Guide de référence Nmap

Nmap (Network Mapper) est un outil de cartographie de réseaux qui analyse les paquets IP pour identifier les périphériques connectés, leurs services et systèmes d'exploitation. Utilisé par les administrateurs réseau, il permet de réaliser des scans de ports, de détecter des hôtes actifs et d'obtenir des informations détaillées sur les configurations réseau.


### Commandes Essentielles

#### Types de scans:

**Null scan** : n'envoie aucun flag TCP.

**FIN scan** : envoie uniquement le flag FIN.

**Noël scan** : envoie les flags FIN, PSH et URG.


*Scan rapide super efficace:

     nmap -sCV -v -p- -T5 10.10.146.158

Scan de présence d'hôtes sur un réseau:

    nmap -sn 10.10.10.0/24

Scan de version avec liste de cibles et export des résultats:

    nmap -sV -p- -iL targets -oN nmap.initial -v

Scan agressif:

    nmap -A -p- -iL targets -oN nmap.aggressive -v

Scan des vulnérabilités:

    nmap -p --script=vuln -v

Pour éviter d'être détecté par IDS ou IPS:

    nmap -sn -T0 172.18.12.0/24

Analyse de découverte d'hôtes:

    nmap -sn 172.16.50.0/24

#### Options d'Analyse Spécifiques

* Analyse de connexion TCP (-sT)

* Analyse UDP (-sU)

* Analyse TCP FIN (-sF)

* Analyse de découverte d'hôtes (-sn)

* Options de synchronisation (-T0 à -T5)

Nmap peut également effectuer des scans avec plusieurs protocoles tels que UDP, TCP, IP, ICMP, HTTP, brute force de mot de passe, et détection de failles.

### Commandes Courantes

Scanner tout un réseau:

    nmap 192.168.1.0/24

Détection du système d'exploitation, nom et adresse MAC:

    nmap -O 192.168.1.1

Scan avancé avec détection de version, traceroute et analyse de scripts:

    nmap -A 192.168.17.1

Afficher l'aide complète:

    nmap --help

Scan de tous les ports et récupération des noms de serveurs:

    nmap -p 1-65535 -T4 -A -v tech.teck

#### Techniques d'évasion et d'usurpation

Scan furtif avec fragmentation des paquets:

    nmap -f

Utilisation de leurres pour masquer l'origine:

    nmap -D RND:10 192.168.1.1

Usurpation d'adresse source:

    nmap -S 192.168.1.100

### Exemples Avancés

Scan des failles HTTP:

    nmap 192.168.28.130 -p 80 --script vuln

Scan avec plusieurs scripts:

    nmap -p 80 --script http-fileupload-exploiter --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'

Scan des utilisateurs et partages SMB:

    nmap -A -Pn --script smb-enum-users.nse --script smb-enum-shares.nse -p139,445,21 -T4 10.6.6.23

### Exportation des Résultats

Enregistrer les résultats dans plusieurs formats:

    nmap -oA report 10.6.6.23

Transformation XML en HTML:

    xsltproc report.xml -o report.html

Export format normal:

    nmap -oN normal_scan.txt

Export format grepable:

    nmap -oG grepable_scan.txt

Commutateurs Clés

    Syn Scan: -sS

    Analyse UDP: -sU

Détection du système d'exploitation: **-O**

Détection de la version des services: **-sV**

Verbosité: **-v, -vV**

Export des résultats dans trois formats: **-oA**

Scan mode agressif: **-A**

Définition du modèle de timing à 5: **-T5**

Scan d'un port spécifique: **-p 80**

Scan d'une plage de ports: **-p 100-1500**

Scan de tous les ports: **-p-**

Activation d'un script: **--script**

Activation des scripts de la catégorie "vuln": **--script=vuln**

### Conclusion

Pour plus d'informations, référez-vous à la [documentation officielle](https://nmap.org/book/man.html) de Nmap qui fournit une mine d'informations pour maîtriser pleinement cet outil indispensable pour la sécurité informatique.
