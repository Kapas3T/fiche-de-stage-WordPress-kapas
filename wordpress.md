
### Étape 1

Q: Qu’est-ce que WordPress?
R: WordPress est un `WCMS` ou web content management system, un WCMS permet de créer et de gérer du contenu web par le biais d'outils d'authoring (design), de collaboration et d'administration. WordPress et les WCMS en général sont une porte d'accès a la création de sites internet pour les débutants ds le domaine. Crée en 2003 par Mike Little et Matt Mullenwerg, wordpress était originellement un outil de bublication de blogs. De fil en aiguille il à été adapté pour faire énormément d'autres choses (forums, magasins en ligne, galeries de médias etc...), tout en restant open source.

Q: WordPress est-il beaucoup utilisé ? 
R: Oui, en décembre 2024, il était utilisé par 22.52% du top 1mio de sites internet, ce qui éqivaut environ 225'200. (Source: wikipédia.org/wiki/WordPress)

Q: Combien coûte WordPress ?
R: WordPress est open-source, il est donc gratuit.

Q: Quelle est la différence entre wordpress.com et wordpress.org
R: wordpress.org sert à se procurer le programme wordpress (gratuit). wordpress.com sert à se procurer tous les autres services payants de wordpress.

---

### Étape 2 

Procédure d`installation d'un LAMP et de WordPress

-> Tout texte écrit entre guillemets (guillemets non compris) sont des commandes à écrire dans le Terminal.  


1. ouvrir le terminal
1. `mkdir temp && cd temp`
1. `sudo apt install apache2 mariadb-server php php-mysql libapache2-mod-php php-xml php-gd php-mbstring php-curl php-zip unzip -y`
1. `sudo sytemctl start apache2 || sudo systemctl start mariadb.service`
1. `sudo mysql -u root`
1. `CREATE DATABASE wordpress_db;`
1. `CREATE USER user IDENTIFIED BY "password";`
1. `GRANT ALL PRIVILEGES ON wordpress_db.* TO user;`
1. `FLUSH PRIVILEGES;`
1. `EXIT;`
1. `cd ~/temp/`
1. `wget -P /home/ubuntu/wordpress/ https://wordpress.org/latest.zip`
1. `unzip latest.zip`
1. `sudo mv -r wordpress/ /var/www/html/wp`
1. `sudo chmod -R 755 /var/www/html/`
1. ouvrir : http://localhost/wp
1. renseigner les informations de la DB
1. créer son compte 
1. vous avez terminé.

---

### Étape3 

Procédure d`installation sur un VM distante

1. demandez à votre référent d'être présent
1. Tapez dans votre terminal `cat .ssh/id_ed25519.pub`
1. Envoyez la réponse par mail/telegram à vôtre référent.
1. Demandez au maître de stage / référent de vous créer une VM.
1. Il vous renverra une ligne qui ressemble à celle-ci `ubuntu@12.345.678.910`
1. Dans le terminal : `ssh connect [l'adresse qu'il vous a envoyé]`
1. vérifiez que votre adresse dans le terminal correspond a celle qui vous à été envoyée. 
1. reprenez depuis ici les mêmes étapes que dans `étape 2` ci-dessus.

