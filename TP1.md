# Compte Rendu - TP 1 - Binôme 22
## Auteurs et date
Clément MORELLI

Thibault GILG

Date : 06/02/2020

## Exercice 2 : Prise en main de l’interpréteur de commandes
###  Manuel
1. ```Which``` affiche les chemins d'accès complets des commandes saisis en paramètres que le shell utiliserait pour les exécuter. 
```
**Résultat console bash :**
Clements-Macbook:~ clement$ which cd
/usr/bin/cd
```
2. Une fois qu'on se trouve dans une page du manuel, on tape ```/terme``` et le terme sera surligné sur l'écran.
Exemple :
```man which``` Le Manuel s'ouvre
Dans le manuel on tape```/option``` , tout les mots options se surligne.
3. Pour quitter le manuel, on presse la touche ```Q```.

4. Nous affichons la première page de la section 6 avec la commande ```man 6 intro```. Cette page introductrice correspond à la section concernant les jeux et les petits programmes drôles disponibles sur le système. Elle décrit la section, précise les auteurs et les conditions de copyright et cite la source.
### Navigation dans l’arborescence des fichiers
1. Pour aller dans le dossier */var/log* , on effectue la commande ```cd /chemin```. Donc dans notre cas ```cd /var/log```.
```
**Résultat console bash :**
Clements-Macbook:script clement$ cd /var/log
Clements-Macbook:log clement$
```
Un chemin est dit relatif lorsque'il est instancié par rapport à l'endroit où l'utilisateur se situe dans l'arborescence. Un chemin est dit absolu lorsque'il est instancié par rapport à la racine (depuis "/").

2. Étant donné que nous somme dans le dossier */var/log* , il nous faut aller dans le dossier */var* parent de *log*. Pour remonter dans le dossier parent, on effectue la commande ```cd ..```.
```
**Résultat console bash :**
Clements-Macbook:log clement$ cd ..
Clements-Macbook:var clement$
```
3. Pour retourner dans le dossier personnel, on effectue la commande ```cd```.
```
**Résultat console bash :**
Clements-Macbook:var clement$ cd
Clements-Macbook:~ clement$
```
4. Pour revenir au dossier précédent, on effectue la commande ```cd -```.
```
**Résultat console bash :**
Clements-Macbook:~ clement$ cd -
/var
Clements-Macbook:var clement$
```
5. En tapant ```cd root```, pour aller au dossier */root*, on obtient le message ```bash: cd: /root: Permission denied```. L'utilisateur simple n'a pas accès au dossier */root.*
```
**Résultat console bash :**
Clements-Macbook:var clement$ cd root
-bash: cd: root: Permission denied
```
6. La commande ```sudo cd /root``` permet d'exécuter des script avec les droits de super utilisateur. Cela est requis pour des tâches d'administration. Ensuite, on doit taper le mot de passe de l'utilisateur. Cependant, dans notre cas cela ne marche pas puisque ```cd``` n'est pas un script.
```
**Résultat console bash :**
Clements-Macbook:~ clement$ sudo cd /root
Password:
/usr/bin/cd: line 4: cd: /root: No such file or directory
```
7. Pour créer cette arborescence, on effectue les commandes suivantes: 
* ```mkdir Dossier1 Dossier2``` pour créer les dossiers *Dossier1* et *Dossier2*. 
* ```cd Dossier1 ; touch Fichier1``` pour aller dans le dossier *Dossier1* et créer le fichier *Fichier1*
* ```cd ..``` pour retourner dans le dossier parent
* ```cd Dossier2 ; mkdir Dossier2.1 Dossier2.2``` pour aller dans le dossier *Dossier2* et créer les dossiers *Dossier2.1* et *Dossier2.2*.
* ```cd Dossier2.2 ; touch Fichier2 Fichier3``` pour aller dans le dossier *Dossier2.2* et créer les fichiers *Fichier2* et *Fichier3*.
```
**Résultat console bash :**
Clements-Macbook:~ clement$ mkdir Dossier1 Dossier2
Clements-Macbook:~ clement$ ls
Dossier1  Dossier2
Clements-Macbook:~ clement$ cd Dossier1 ; touch Fichier1
Clements-Macbook:Dossier1 clement$ ls
Fichier1
Clements-Macbook:Dossier1 clement$ cd ..
Clements-Macbook:~ clement$ cd Dossier2 ; mkdir Dossier2.1 Dossier2.2
Clements-Macbook:Dossier2 clement$ ls
Dossier2.1  Dossier2.2
Clements-Macbook:Dossier2 clement$ cd Dossier2.2 ; touch Fichier2 Fichier3
Clements-Macbook:Dossier2.2 clement$ ls
Fichier2  Fichier3
```
8. Il est impossible de supprimer un élément qui n'est pas directement dans le répertoire de courant sans indiquer le chemin à emprunter pour aller au fichier. De plus, la commande ```rm``` seul fonctionne uniquement pour les fichiers, et non pour les dossiers. La commande ```rm Fichier1 Dossier1``` ne fonctionne donc pas.
```
**Résultat console bash :**
Clements-Macbook:~ clement$ rm Fichier1 Dossier1
rm: Fichier1: No such file or directory
rm: Dossier1: is a directory
```
9.  Il faut utiliser la commande ```rmdir``` ou ```rm -d```pour supprimer un dossier. 
```
**Résultat console bash :**
Clements-Macbook:~ clement$ mkdir A
Clements-Macbook:~ clement$ ls
A  Dossier1
Dossier2  
Clements-Macbook:~ clement$ rmdir A
Clements-Macbook:~ clement$ ls
Dossier1  Dossier2
``` 
Deuxième solution :
``` 
**Résultat console bash :**
Clements-Macbook:~ clement$ mkdir A
Clements-Macbook:~ clement$ ls
A  Dossier1
Clements-Macbook:~ clement$ rm -d A
Clements-Macbook:~ clement$ ls
Dossier1  Dossier2
``` 
10. Lorsqu'on essaye de supprimer *Dossier2* avec la commande ```rmdir```, on obtient ce message d'erreur : ```rmdir: impossible de supprimer 'd': Le dossier n'est pas vide```. En effet, on ne peut supprimer un dossier non vide avec cette commande.
```
**Résultat console bash :**
Clements-Macbook:~ clement$ rmdir Dossier2
rmdir: Dossier2: Directory not empty
``` 
11. On utilise la commande ```rm -fr Dossier2``` pour supprimer un dossier non vide.
```
**Résultat console bash :**
Clements-Macbook:~ clement$ rm -fr Dossier2
Clements-Macbook:~ clement$ ls
Dossier1
``` 
### Commandes importantes
1. Pour afficher l'heure, on utilise la commande ```date``` qui affiche également la date. 
```
**Résultat console bash :**
Clements-Macbook:~ clement$ date
Dim  9 fév 2020 12:54:14 CET
``` 
La commande ```time``` permet de mesurer le temps d'exécution d'une commande. Elle fournit le temps réel  (temps total), le temps utilisateur (durée nécessaire au processeur pour exécuter les ordres du programme) et le temps système (durée nécessaire au processeur pour traiter les ordres du système d'exploitation).
```
**Résultat console bash :**
Clements-Macbook:~ clement$ time
real  0m0.001s
user  0m0.000s
sys  0m0.000s
``` 
2. La commande ```ls``` affiche le contenue d'un répertoire. Et la commande ```la``` affiche le contenue d'un répertoire y compris les fichier commençant par "." 
```
**Résultat console bash :**
Clements-Macbook:~ clement$ ls
Applications  Movies
Applications (Parallels)
Clements-Macbook:~ clement$ la
.CFUserTextEncoding  .packettracer
.DS_Store  .spyder
.Trash  Applications
.anaconda  Applications (Parallels)
``` 
Ainsi, les fichiers commençant par un point sont des fichiers cachés.

3. Pour savoir ou se situe la commande ```ls```, on utilise ```which``` comme vu précédemment.
Ainsi, on voit que la commande ```ls``` se situe ici: ```/bin/ls```.
```
**Résultat console bash :**
Clements-Macbook:~ clement$ which ls
/bin/ls
``` 

4. La commande ```ll``` permet d'afficher tout les fichiers et dossiers d'un répértoire avec des détails tel que leurs droits, qui la crée, ou il se situe quand il a été crée. De plus, Avec la commande ```alias'```, on s'aperçoit que la commande ```ll``` est équivalente à la commande ```ls -alF```. Il n'existe pas d'entré de manuel pour cette commande car ce n'est qu'un alias qui n'est qu'un ```ls``` avec des options. Donc, le manuel n'est disponible que pour la commande ```ls```. ```-a``` n'ignore pas les fichiers commençant par ".", ```-l```  utilise des listings de long format et ```--F``` "classify" => classe les fichiers
```
**Résultat console bash :**
Clements-Macbook:~ clement$ ll
total 88
drwxr-xr-x+ 34 clement  staff 1088  9 fév 15:22 ./
drwxr-xr-x 6 root admin  192 29 sep 22:22 ../
```
```
**Résultat console bash :**
Clements-Macbook:~ clement$ alias ll
ls -alF
``` 
5. Pour aﬀicher les fichiers contenus dans le dossier "/bin", il faut utiliser la commande ```ls```.
```
**Résultat console bash :**
clements-macbook:~ clement$ ls /bin
[  dd  launchctl  pwd  test
bash  df  link  rm  unlink
cat  echo  ln  rmdir  wait4path
chmod  ed  ls  sh  zsh
cp  expr  mkdir  sleep
csh  hostname  mv  stty
dash  kill  pax  sync
date  ksh  ps  tcsh
```
6. La commande ```ls..``` permet d'afficher tout les fichiers et dossiers du répértoire parents, du répertoire au dessus de celui que l'on se trouve.
``` 
**Résultat console bash :**
clements-macbook:bin clement$ ls ..
Applications  System  cores  opt  usr
CLÚMENT  Users  dev  private  var
Library  Volumes  etc  sbin
Preboot  bin  home  tmp
```
7. Pour connaitre le chemin complet du dossier courant, on utilise la commande ```pwd```.
``` 
**Résultat console bash :**
clements-macbook:bin clement$ pwd
/bin
```
8. La commande ``` echo 'yo' > plop``` envoie le texte "yo" dans un fichier nommé "plop". Si plop n'existe pas il est crée, si il existe le contenue est supprimer et devient uniquement "yo". Donc, si on fait deux fois cette commande cela revient au meme  que si on le faisait que une seule fois car le premier "yo" est écrasé.
``` 
**Résultat console bash :**
clements-macbook:~ clement$  echo 'yo' > plop
clements-macbook:~ clement$ cat plop
yo
clements-macbook:~ clement$  echo 'yo' > plop
clements-macbook:~ clement$ cat plop
yo
``` 
9. La commande ``` echo 'yo' >> plop``` envoie le texte "yo" dans un fichier nommé "plop". Si plop n'existe pas il est crée, si il existe le contenue n'est supprimer, "yo" est ajouté à la suite. Donc, si on fait deux fois cette commande le fichier contient 2 "yo".
``` 
**Résultat console bash :**
clements-macbook:~ clement$ echo 'yo' >> plop
clements-macbook:~ clement$ echo 'yo' >> plop
clements-macbook:~ clement$ cat plop
yo
yo
``` 
10. La commande ``` file``` sert à nous donner le type de l'object passer en paramètres. La commande ``` file``` test l'argument (nom du fichier/dossier) dans l'intention de le classer. Elle procède selon 3 traitements : filesystem tests, magic tests, language tets. Le premier test qui réussi engendre la classification. ```filesytem tests``` test le programme regarde si le fichier est vide. ```magic tests ``` est utilisé pour checker les fichiers avec des formats fixés particuliers. Et```language tests ``` , si aucun test ne réussit, le test de language examine si le fichier est un fichier text. Le system analyse alors le rangement des caractères ASCII, ISO-8859-x, ... Par exemple, le mot clé "struct" indique que le fichier est programme C.
``` 
**Résultat console bash :**
thibault@thibault-gilg:~/Documents/4A/S8/Admin Système$ file Cours.txt
Cours.txt: UTF-8 Unicode text
thibault@thibault-gilg:~/Documents/4A/S8/Admin Système$ file TP1
TP1: directory
``` 
11. On crée un fichier toto avec le texte "Hello toto !" vec la commande vu précédemment de la forme ```echo 'texte' >> fichier```. Ensuite, nous créons un lien entre toto et titi avec la commande ```ln toto titi```. Ainsi, on voit que le contenue de toto se retrouve dans titi. Si l'on écrit dans toto, cela écrit dans titi et inversement. De plus, si l'on supprime toto, titi reste intact.
```
Clements-Macbook:Dossier1 clement$ echo 'Hello toto !' >> toto
Clements-Macbook:Dossier1 clement$ ln toto titi
Clements-Macbook:Dossier1 clement$ cat toto
Hello toto !
Clements-Macbook:Dossier1 clement$ cat titi
Hello toto !
Clements-Macbook:Dossier1 clement$ echo 'Hello toto !' >> toto
Clements-Macbook:Dossier1 clement$ cat titi
Hello toto !
Hello toto !
Clements-Macbook:Dossier1 clement$ echo 'Hello toto !' >> titi
Clements-Macbook:Dossier1 clement$ cat toto
Hello toto !
Hello toto !
Hello toto !
Clements-Macbook:Dossier1 clement$ rm toto
Clements-Macbook:Dossier1 clement$ cat titi
Hello toto !
Hello toto !
Hello toto !
``` 
12. Nous créons un lien symbolique entre titi et tutu avec la commande ```ln -s titi tutu```Le contenu de 'titi' se retrouve dans le fichier 'tutu' grâce au lien symbolique. Si l'on écrit dans titi, cela écrit dans tutu et inversement. Cependant, contrairement au lien précédent, les 2 fichiers sont dépendants et ainsi la suppression de l'un entraine également la suppression de l'autre fichier.
```
**Résultat console bash :**
Clements-Macbook:Dossier1 clement$ ln -s titi tutu
Clements-Macbook:Dossier1 clement$ echo 'Coucou !' >> titi
Clements-Macbook:Dossier1 clement$ cat tutu
Hello toto !
Hello toto !
Hello toto !
Coucou !
Clements-Macbook:Dossier1 clement$ echo 'Coucou !' >> tutu
Clements-Macbook:Dossier1 clement$ cat titi
Hello toto !
Hello toto !
Hello toto !
Coucou !
Coucou !
Clements-Macbook:Dossier1 clement$ rm titi
Clements-Macbook:Dossier1 clement$ cat tutu
cat: tutu: No such file or directory
``` 
13. Pour afficher le contenu de ```/var/log/syslog ``` on utilise ```cat```. Lors du défilement du résultat on peut l'interrompre par la commande ```CTRL + S``` puis le reprendre par la commande ```CTRL + Q```.
14. Pour aﬀichez les 5 premières lignes du fichier ```/var/log/syslog ```, on utilise ```head -n 5 [nomFichier]```,puis les 15 dernières on utilise ```tail -n 15 [nomFichier]```, puis seulement les lignes 10 à 20 on utilise ```sed -n '10,15p' [nomFichier]```
```
**Résultat console bash :**
thibault@thibault-gilg:~$ head -n 5 /var/log/syslog
Feb  8 12:11:09 thibault-gilg rsyslogd:  [origin software="rsyslogd" swVersion="8.32.0" x-pid="991" x-info="http://www.rsyslog.com"] rsyslogd was HUPed
Feb  8 12:11:10 thibault-gilg kernel: [  312.606032] audit: type=1400 audit(1581160270.971:54): apparmor="DENIED" operation="open" profile="/usr/sbin/cups-browsed" name="/usr/share/cups/locale/" pid=16207 comm="cups-browsed" requested_mask="r" denied_mask="r" fsuid=0 ouid=0
Feb  8 12:11:10 thibault-gilg kernel: [  312.606036] audit: type=1400 audit(1581160270.971:55): apparmor="DENIED" operation="open" profile="/usr/sbin/cups-browsed" name="/usr/share/locale/" pid=16207 comm="cups-browsed" requested_mask="r" denied_mask="r" fsuid=0 ouid=0
Feb  8 12:11:11 thibault-gilg colord[1104]: failed to get session [pid 16206]: Aucune donnée disponible
Feb  8 12:11:11 thibault-gilg gnome-shell[2653]: JS WARNING: [resource:///org/gnome/shell/ui/notificationDaemon.js 121]: reference to undefined property "image-path"
```
```
**Résultat console bash :**
thibault@thibault-gilg:~$ tail -n 15 /var/log/syslog
Feb  9 15:24:17 thibault-gilg NetworkManager[996]: <info>  [1581258257.2730] device (wlp1s0): supplicant interface state: authenticating -> associating
Feb  9 15:24:17 thibault-gilg wpa_supplicant[1032]: wlp1s0: WPA: Key negotiation completed with d4:60:e3:13:5b:12 [PTK=CCMP GTK=CCMP]
Feb  9 15:24:17 thibault-gilg wpa_supplicant[1032]: wlp1s0: CTRL-EVENT-CONNECTED - Connection to d4:60:e3:13:5b:12 completed [id=0 id_str=]
Feb  9 15:24:17 thibault-gilg gnome-shell[1294]: An active wireless connection, in infrastructure mode, involves no access point?
Feb  9 15:24:17 thibault-gilg gnome-shell[1966]: An active wireless connection, in infrastructure mode, involves no access point?
Feb  9 15:24:17 thibault-gilg NetworkManager[996]: <info>  [1581258257.3106] device (wlp1s0): supplicant interface state: associating -> 4-way handshake
Feb  9 15:24:17 thibault-gilg NetworkManager[996]: <info>  [1581258257.3128] device (wlp1s0): supplicant interface state: 4-way handshake -> completed
Feb  9 15:24:17 thibault-gilg wpa_supplicant[1032]: wlp1s0: CTRL-EVENT-SIGNAL-CHANGE above=1 signal=-76 noise=9999 txrate=28900
Feb  9 15:24:18 thibault-gilg systemd-resolved[849]: Server returned error NXDOMAIN, mitigating potential DNS violation DVE-2018-0001, retrying transaction with reduced feature level UDP.
Feb  9 15:24:18 thibault-gilg systemd-resolved[849]: message repeated 5 times: [ Server returned error NXDOMAIN, mitigating potential DNS violation DVE-2018-0001, retrying transaction with reduced feature level UDP.]
Feb  9 15:24:23 thibault-gilg gnome-shell[1966]: Some code accessed the property 'WindowPreviewMenu' on the module 'windowPreview'. That property was defined with 'let' or 'const' inside the module. This was previously supported, but is not correct according to the ES6 standard. Any symbols to be exported from a module must be defined with 'var'. The property access will work as previously for the time being, but please fix your code anyway.
Feb  9 15:25:53 thibault-gilg dbus-daemon[973]: [system] Activating via systemd: service name='org.freedesktop.hostname1' unit='dbus-org.freedesktop.hostname1.service' requested by ':1.145' (uid=1000 pid=3982 comm="gedit " label="unconfined")
Feb  9 15:25:53 thibault-gilg systemd[1]: Starting Hostname Service...
Feb  9 15:25:53 thibault-gilg dbus-daemon[973]: [system] Successfully activated service 'org.freedesktop.hostname1'
Feb  9 15:25:53 thibault-gilg systemd[1]: Started Hostname Service.
```
```
**Résultat console bash :**
thibault@thibault-gilg:~$ sed -n '10,15p' /var/log/syslog
Feb  8 12:12:39 thibault-gilg org.gnome.Shell.desktop[2653]: Ouverture dans une session de navigateur existante.
Feb  8 12:12:49 thibault-gilg org.gnome.Shell.desktop[2653]: [16472:1:0208/121249.737428:ERROR:child_process_sandbox_support_impl_linux.cc(79)] FontService unique font name matching request did not receive a response.
Feb  8 12:12:49 thibault-gilg org.gnome.Shell.desktop[2653]: [16472:1:0208/121249.738866:ERROR:child_process_sandbox_support_impl_linux.cc(79)] FontService unique font name matching request did not receive a response.
Feb  8 12:12:50 thibault-gilg org.gnome.Shell.desktop[2653]: [16536:1:0208/121250.383211:ERROR:child_process_sandbox_support_impl_linux.cc(79)] FontService unique font name matching request did not receive a response.
Feb  8 12:12:50 thibault-gilg org.gnome.Shell.desktop[2653]: [16536:1:0208/121250.383958:ERROR:child_process_sandbox_support_impl_linux.cc(79)] FontService unique font name matching request did not receive a response.
Feb  8 12:12:50 thibault-gilg org.gnome.Shell.desktop[2653]: [16536:1:0208/121250.392370:ERROR:child_process_sandbox_support_impl_linux.cc(79)] FontService unique font name matching request did not receive a response.
```
15. La commande``` dmesg | less ``` affiche le contenue de la mémoire tampon (``` dmesg```) mais page par page grâce au ```less ```.
16. Pour afficher le contenue du fichier /etc/passwd on utilise ```cat``` et il contient les informations de chaque utilisateur identifié sur le système : mot de pase crypté, numéro d'utilisateur, nom complet, répertoire de base de l'utilisateur. Exemple : ```kadmin_admin:*:218:-2:Kerberos Admin Service:/var/empty:/usr/bin/false```.Pour afficher la page de manuel de ce fichier il faut utiliser la commande ```man passwd'```.
17. Pour afficher seulement la première colonne triée par ordre alphabétique inverse on utilise la commande ``` cut -d ':' -f1 /etc/passwd | sort -r ```. On envoie  seulement la première colonne avec```cut -d ':'``` de  ```/etc/passwd``` à ```-r```qui trie à l'inverse.
```
thibault@thibault-gilg:~$ cut -d ':' -f1 /etc/passwd | sort -r 
www-data
whoopsie
uuidd
uucp
usbmux
```
18. Pour connaitre le nombre d'utilisateur ayant un compte sur cette machine, on utilise la commande ```cut -f1 -d: /etc/passwd | wc -l```. On à la liste en colonne des utilisateurs que l'on envoie à ```wc -l``` afin de la compter.
```
Clements-Macbook:~ clement$ cut -f1 -d: /etc/passwd | wc -l
110
```
19. Pour connaitre le nombre de pages de manuel qui comportent le mot-clé conversion dans leur description , on utilise la commande ```man -k conversion | wc -l```. On obtient 4 pages.
```
thibault@thibault-gilg:~$ man -k conversion | wc -l
4
```
20. Pour recherchez tous les fichiers se nommant passwd présents sur la machine, on utilise la commande ```find / -name 'passwd'```. On obtient alors une très longue liste avec des accès denier. Il serais plus pertinent de précéder la commande ci-dessus par ```sudo``` car certains fichiers ont un accès restreint aux simples utilisateurs.
```
thibault@thibault-gilg:~$ find / -name 'passwd'
```
21. Pour que la liste des fichiers trouvés soit enregistrée dans le fichier ~/list_passwd_files.txt et que les erreurs soient redirigées vers le fichier spécial /dev/null on utilise les commandes :
```find /name passwd 1> ~/list_passwd_files.txt```. 1 correspond fichier qui sont bien trouvés.
```find /name passwd 2> dev/null```. 2 correspond aux erreurs du programme par exemple accès denier, donc il n'a pas pu chercher dedans car il n'a pas l'autorisation donc, il ne sait pas donc erreur.
```
thibault@thibault-gilg:/etc$ find / -name 'passwd' 2> ~/dev/null
/etc/pam.d/passwd
/etc/cron.daily/passwd
/etc/passwd
/snap/core18/1668/etc/pam.d/passwd
/snap/core18/1668/etc/passwd
```
22. Lorsque l'on utilise la commande  ```grep -ri "alias ll" ```, on obtient où est défini l’alias ```ll  ```. Il est donc définit à cette adresse ```.bashrc ```.
23. Tout d'abord, on installe  ```locate``` avec  ```sudo apt install locate```.  Ensuite, on peut chercher history.log en utilisant ```locate```. On obtient donc que history.log se situe ici /var/log/apt
```
**Résultat console bash :**
thibault@thibault-gilg:/etc$ locate history.log
/var/log/apt/history.log
/var/log/apt/history.log.1.gz
/var/log/apt/history.log.2.gz
/var/log/apt/history.log.3.gz
```
24. Lorsque que l'on crée un fichier et que l'on le cherche avec la commande ```locate```, le fichier n'apparaît pas parce que ```locate``` cherche dans un fichier contenant tous les noms des fichiers. Or, ce fichier n'est pas automatiquement mis à jour lorsqu'on vient de créer un fichier. Ainsi, il ne trouve pas le fichier.

## Exercice 4 : Personnalisation du shell

3. Décommenter la ligne ```force_color_prompt=yes``` et recharger le fichier *.bashrc* permet de faire passer l'invite de commande en couleurs. On obtient ```user@host``` en vert et ```chemin_courant``` en bleu. 
4. Pour avoir la forme souhaitée de l'invite de commande, nous avons remplacé la séquence concernant les couleurs par celle-ci : ```\[\e[01;35m\]\A\[\e[00m\] - \[\e[01;32m]\u@\h\[\e[00m\]:\[\e[01;36m\]\w\[\e[00m\]\$```. 
* La séquence ```\[\e[01;35m\]\A``` permet d'afficher l'heure (```\A```) en violet, dont le code couleur est 35.
* Les séquences ```\[\e[00m\] - ```, ```\[\e[00m\]: ``` et ```\[\e[00m\]\$``` permettent d'afficher respectivement le tiret, les deux points et le $
 en blanc, dont le code couleur est 0.
 * La séquence ```\[\e[01;32m]\u@\h``` permet d'afficher les noms de l'utilisateur et de la machine en vert, dont le code couleur est 32.
 * La séquence ```\[\e[01;36m\]\w``` permet d'afficher le chemin courant en cyan, dont le code couleur est 36.

