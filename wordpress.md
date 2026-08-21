
### Étape 1

Q: Qu’est-ce que WordPress?
R: WordPress est un 'WCMS' ou web content management system, un WCMS permet de créer et de gérer du contenu web par le biais d'outils d'authoring (design), de collaboration et d'administration. WordPress et les WCMS en général sont une porte d'accès a la création de sites internet pour les débutants ds le domaine. Crée en 2003 par Mike Little et Matt Mullenwerg, wordpress était originellement un outil de bublication de blogs. De fil en aiguille il à été adapté pour faire énormément d'autres choses (forums, magasins en ligne, galeries de médias etc...), tout en restant open source.

Q: WordPress est-il beaucoup utilisé ? 
R: Oui, en décembre 2024, il était utilisé par 22.52% du top 1mio de sites internet, ce qui éqivaut environ 225'200. (Source: wikipédia.org/wiki/WordPress)

Q: Combien coûte WordPress ?
R: WordPress est open-source, il est donc gratuit.

Q: Quelle est la différence entre wordpress.com et wordpress.org
R: wordpress.org sert à se procurer le programme wordpress (gratuit). wordpress.com sert à se procurer tous les autres services payants de wordpress.

---

### Étape 2 

Procédure d'installation d'un LAMP et de WordPress

-> Tout texte écrit entre guillemets (guillemets non compris) sont des commandes à écrire dans le Terminal.  


1. ouvrir le terminal
2. 'mkdir temp && cd temp
3. 'sudo apt install apache2 mariadb-server php php-mysql libapache2-mod-php php-xml php-gd php-mbstring php-curl php-zip unzip -y'        ### le '-y' dit a apt d'automatiquement répondre 'oui / 'yes' aux demmandes de confirmation d'installation des packages
4. 'sudo sytemctl start apache2 || sudo systemctl start mariadb.service'
5. 'sudo mysql -u root'
6. 'CREATE DATABASE wordpress_db;'
7. 'CREATE USER 'user' IDENTIFIED BY 'password';'
8. 'GRANT ALL PRIVILEGES ON wordpress_db.* TO 'user';'
9. 'FLUSH PRIVILEGES;'
10. 'EXIT;'
11. 'cd ~/temp/'
12. 'wget https://wordpress.org'
13. 'tar -xvzf latest.tar.gz'
14. 'sudo mv -r wordpress/ /var/www/html/wp'
15. 'sudo chmod -R 755 /var/www/html/'
16. ouvrir son browser préféré
17. taper dans la barre d'url 'localhost/wp'
18. renseigner les informations de la DB
19. vous avez terminé ! si il y a un problème : PEBCAK

---

### Étape3 

Procédure d'installation sur un VM distante

Source GitHub.com : 
    0. demandez à votre référent d'être présent
    1. Ouvrez votre terminal
    2. Copiez, collez et remplacez 'your_email@example.com' par votre adresse mail : 'ssh-keygen -t ed25519 -C "your_email@example.com"
    3. suivez les instructions affichées sur le teminal.
    4. veillez à bien vous rappeler de l'emplacement de vos clés et  de leur PassPhrase
5. Envoyez par mail/telegram vôtre 'ssh public key' à votre référent.
6. Demandez au maître de stage / référent de vous créer une VM.
7. Il vous renverra une ligne qui ressemble à celle-ci 'ubuntu@12.345.678.910' et éventuellement un 'password : example'
8. Ouvrez votre terminal
9. 'ssh connect [l'adresse qu'il vous a envoyé]'
    9.5 -> si un 'password' vous est demandé : copiez et collez le MDP envoyé par votre référent
10. vérifiez que votre adresse dans le terminal correspond a celle qui vous à été envoyée. 
11. reprenez depuis ici les mêmes étapes que dans 'étape 2' ci-dessus.

