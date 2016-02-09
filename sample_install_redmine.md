# Installation de Ruby
Installation de ruby version 1.9.3 (pour compatibilité Readmine 2.1) [Ruby Website](https://www.ruby-lang.org/fr/)
> apt-get install ruby -v ‘1.9.3’

# Installation de la base de donnée
Installation du driver mysql (bdd utiliser par Redmine 2.1)
> apt-get install mysql

# Installation de bundler
Bundler est un logiciel d'installer et de guarantir la compatibilité entre les différentes dépendances
[Bundler](http://bundler.io/)
> gem install bundler

# Installation de Redmine
1 Récupération des sources de [Redmine](http://www.redmine.org/projects/redmine/wiki/Download)
2 Extraction des sources
>tar zxvf redmine-*.tar.gz
3 Installation des dépendances
>bundle install --without development test postgresql sqlite

# Création de la base de donnée
Création de la base de donnée pour Redmine avec c’est privilèges
>create database redmine character set utf8;
>create user ‘redmine’@’localhost’ identified by ‘my_password’;
>grant all privileges on redmine.* to ‘redmine’@’localhost’;
>grant all privileges on redmine.* to ‘redmine’@’localhost’ identified by ‘my_password’;

# Ajustement de la configuration de redmine
Copie du fichier d'exemple database.yml.example
>copy config/database.yml.example to config/database.yml
Puis on modifie le fichier
>production:
>	adapter: mysql
>	database: redmine
>	host: localhost
>	username: redmine
>	password: my_password

# Configuration des clée de sécurité
Génération aléatoire du clée pour Rails
>generate_secret_token

# Chargement de la langue
Insertion de la configuration dans la bdd
>RAILS_ENV=production REDMINE_LANG=fr rake redmine:load_default_data

# Ajustement des permissions système
>mkdir tmp tmp/pdf public/pluging_assets
>chown -R redmine:redmine files log tmp public/pluging_assets
>chmod -R 755 files log tmp public/pluging_assets