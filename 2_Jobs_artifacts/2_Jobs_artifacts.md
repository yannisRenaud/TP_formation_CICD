# Jobs et artifacts

## Besoin
Dans la première étape, nous avons utilisé le fichier fichier *deploy.yml* pour automatiser l'étape de build dans le job "deploy".

On souhaite maintenant séparer le build et le déploiement en deux jobs distincts pour plus de cohérence.

## Etapes à ajouter à deploy.yml
### Job build
Ajouter un job nommé **build**. Celui-ci comprendra les étapes de build ajoutées précédemment ainsi que l'action checkout permettant de récupérer le code.

Le job deploy conservera les steps de déploiement.

### Artifact
Le fait de séparer les steps en plusieurs jobs implique de gérer un **artifact**.

Ici il s'agit des fichiers générés par le job Build, puisqu'on souhaite les utiliser dans le job deploy.

On utilisera pour cela les actions :
- upload-artifact
- download-artifact
