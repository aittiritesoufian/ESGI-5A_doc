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
