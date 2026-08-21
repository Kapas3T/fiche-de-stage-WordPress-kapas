Procédure d'installation d'un LAMP et de WordPress

Copyright @Kapas3T™ all tights reserved. ;)

-> Tout texte écrit entre guillemets (guillemets non compris) sont des commandes à écrire dans le Terminal.  


1. ouvrir le terminal
2. "mkdir temp && cd temp"
3. "sudo apt install apache2 mariadb-server php php-mysql libapache2-mod-php php-xml php-gd php-mbstring php-curl php-zip unzip -y"        ### le "-y" dit a apt d'automatiquement répondre "oui / "yes" aux demmandes de confirmation d'installation des packages
4. "sudo sytemctl start apache2 || sudo systemctl start mariadb.service"
5. "sudo mysql -u root"
6. "CREATE DATABASE wordpress_db;"
7. "CREATE USER 'user' IDENTIFIED BY 'password';"
8. "GRANT ALL PRIVILEGES ON wordpress_db.* TO 'user';"
9. "FLUSH PRIVILEGES;"
10. "EXIT;"
11. "cd ~/temp/"
12. "wget https://wordpress.org"
13. "tar -xvzf latest.tar.gz"
14. "sudo mv -r wordpress/ /var/www/html/wp"
15. "sudo chmod -R 755 /var/www/html/"
16. ouvrir son browser préféré
17. taper dans la barre de recherche "localhost/wp"
18. renseigner les informations de la DB
19. vous asvez terminé ! si il y a un problème : PEBCAK
