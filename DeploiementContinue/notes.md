# Cours de déploiement continue
Création du dossier working_copy
Création d'un fichier index.html dedans
Création sur le dossier parent de working_copy, un dossier remote
Dans le dossier remote on fait un:
```sh
git init --bare
```
Ensuite dans le dossier working_copy on fait un:
```
git init
```
Ensuite on commit le fichier 'index.html'
Ensuite on ajoute une remote dans le répertoire working_copy, cette remote sera le répertoire remote créer tout à l'heure:
```
git remote add origin ../remote/
```
Maintenant on fait un push depuis working_copy:
```
git push origin master
```
On vient de faire un push sur la remote "../remote/"

## ajouter un message lors du post update

On va dans le répertoire remote/hooks
On copie le fichier post-update.sample en post-update
```
cp hooks/post-update.sample post-update
```
Dans le fichier post-update on ajoute la ligne suivante avant la ligne "exec...":
```
echo "something"
```
Ensuite on retourne sur le répertoire working_copy et on fait une modification sur le fichier index.html
On fait un nouveau commit.
On push sur la remote et nous obtenons un message "remote: something" avant l'affichage du changement de référence de commit.

## Conteneur multistage
Construire un conteneur à partir d'un autre en utilisant les from dans un Dockerfile (voir la doc).
(voir les docker build args)

Exemple: activation d'OP_CACHE sur php en production mais pas en environnement de test
```
opcache.memory_consumption=256
opcache.max_accelerated_files=2000
opcache.validate_timestamp=0 #pour désactiver l'expiration du cache
```

## Autre
### Minio
Permet de stocker des objets de données.

### The Twelve-Factor App
Aujourd'hui pour les serveurs, ont fait du déclaratifs, on déclare des configurations de serveur et on déclenche des création de serveur au besoin et on supprime se le serveur ne marche plus correctement.

### Variables d'environnements
Ne pas utiliser les variables d'environnement, définir plutôt des fichiers d'environnement qui possède une valeur du même non que son nom d'environnement, qu'il faudra ensuite lire et trim sur le container où il sera utilisé.

```
parameters:
    env(AUTH_FILE): '../config/auth.json'
google:
    auth: '%env(trim:file:AUTH_FILE)%'
```

Voir vault pour le montage des mots de passe en fichier "temp/" et pas en fichier physique.

Le cache peux être fait avant le déploiement.

# Steps
1. Faire tourner "Biat"
2. Faire une step pour supprimer dans le répertoire de déploiement les fichiers qui ne sont pas utiles (en fonction d'un environnement donnée = PROD / DEV).
3. Build, artifactoring (reprendre ce que j'ai pris dans la deuxième step pour la 3ème)
4. Déploiement

# Steps
Cloner le projet et le faire marcher.
Mettre sur un gitlab
Activer le CI

Construire l'image Docker:
- php, apache, projet symfony
- composer pas dans l'image de production (stage) (yarn install)
- on active pas l'opcache, on peux ajouter des outils de débug pour symfony et XDebug
- tag de version dev-XXX


Pour la master: (image de prod)
- pas de cache, pas de composer, php, apache.
- build-args avec les variables d'environnement pour la version production
