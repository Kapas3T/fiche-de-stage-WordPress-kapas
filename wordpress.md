
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

Procédure d'installation d'un LAMP et de WordPress.

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
1. Tapez dans votre terminal `cat .ssh/id_ed25519.pub` - cette commande vous affiche, dans l'ordre, votre email, votre type d'encryption et vôtre clé ssh.
1. Envoyez vôtre clé ssh par mail/telegram à vôtre référent.
1. Demandez au maître de stage / référent de vous créer une VM.
1. Il vous renverra une ligne qui ressemble à celle-ci "ubuntu@12.345.678.910"
1. Dans le terminal : `ssh [la ligne qu'il vous a envoyé. ex: ubuntu@12.345.678.910]`
1. vérifiez que vous êtes correctement connecté
1. depuis ici, reprenez les mêmes étapes que dans l'étape 2 ci-dessus.

---
## Partie 4 : DOCKER

Docker est un outil qui permet de faire un paquet avec n'importe quelle application & ses dépendances et de l'executer sur n'importe 
quel serveur distant.

---

La conteneurisation est beacoup plus légère et flexible que la vitualisation. 

---

Pour démarrer WordPress sur son ordinateur : 
```
sudo systemctl start apache2.service
sudo systemctl start mariadb.service
```
Puis se rendre sur [Localhost](http://localhost).

> Ces commandes démarrent le serveur web et la database, on ne peut pas à proprement dit "démarrer wordpress"

---
 ### Installation de docker 

 ``` 
  curl -fsSL https://get.docker.com | sh 
```
---
### Les commandes 

#### Commandes relatives aux **images**

| Commande  | Action       |
| :-----: | :---------- |
| `docker run <image>` | Va aller chercher l'image <image> dans le cache local. S'il ne le trouve pas, il va directement la chercher en ligne    |
| `docker pull <image>` | Télécharger une image |
| `docker images` | Liste les images installées localement | 
| `docker rmi <image>` | Supprime l'imge "<image>" | 
| `docker build -t <image>`| Construit une image à partir d'un fichier dockerfile |


##### Commandes relative aux **containers**

| Commande  | Action       |
| :-----: | :---------- |
| `docker run -d <image>` | Fais tourner une image en daemon (en arrière-plan) |
| `docker ps` | Liste tous les conteneurs en train de tourner |
| `docker ps -a` | Liste tous les conteneurs, même ceux arrêtés |
| `docker stop <id>` | Arrête un conteneur en cours d'exécution |
| `docker rm <id>` | Supprime un conteneur |
| `docker logs <id>` | Affiche les logs d'un conteneur |
| `docker exec -it <id> sh` | Ouvre un terminal à l'intérieur d'un conteneur en cours d'exécution |

--- 

## Installer WordPress avec docker

```
sudo apt install npm

```

--- 
### cilentSQL

```
MariaDB [wordpress]> describe wp_users;
+---------------------+---------------------+------+-----+---------------------+----------------+
| Field               | Type                | Null | Key | Default             | Extra          |
+---------------------+---------------------+------+-----+---------------------+----------------+
| ID                  | bigint(20) unsigned | NO   | PRI | NULL                | auto_increment |
| user_login          | varchar(60)         | NO   | MUL |                     |                |
| user_pass           | varchar(255)        | NO   |     |                     |                |
| user_nicename       | varchar(50)         | NO   | MUL |                     |                |
| user_email          | varchar(100)        | NO   | MUL |                     |                |
| user_url            | varchar(100)        | NO   |     |                     |                |
| user_registered     | datetime            | NO   |     | 0000-00-00 00:00:00 |                |
| user_activation_key | varchar(255)        | NO   |     |                     |                |
| user_status         | int(11)             | NO   |     | 0                   |                |
| display_name        | varchar(250)        | NO   |     |                     |                |
+---------------------+---------------------+------+-----+---------------------+----------------+
10 rows in set (0.009 sec)
```
---

# Partie 5 : Déploiement en prod avec docker

```Bash
# Ajout de la clé GPG officielle de docker :
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Ajout du repo. dans les ressources APT:
sudo tee /etc/apt/sources.list.d/docker.sources
sudo apt update

# Installation des pacages docker : 
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Téléchargement de mon docker-compose WordPress customisé
wget https://raw.githubusercontent.com/Kapas3T/fiche-de-stage-WordPress-kapas/refs/heads/main/dockerKit/docker-compose.yaml

# Création de l'environnement et déploiment
mkdir SiteDocker && cd SiteDocker && sudo docker compose up -d


```