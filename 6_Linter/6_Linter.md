# Linter

## Besoin
Après l'ajout des tests, on souhaiterait aussi vérifier la qualité de notre code. \
Une des possibilités qui s'offre à nous est d'utiliser un linter. \
Il s'agit d'un outil qui analyse la syntaxe de notre code, et remonte les écarts par rapport aux conventions.

## Super-linter
Super-linter est une collection de linters et analyseurs de code disponible sur github : https://github.com/super-linter/super-linter \
C'est ce que nous utiliserons dans notre projet pour analyser :
- le YAML
- le JSON
- le TypeScript
- le JavaScript

*Conseil : le texte en sortie los de l'exécution de super-linter est plutôt fourni, surtout lorsque l'analyse du JS et du TS est activée. On vous recommande de vous contenter de l'analyse du JSON le temps de tout mettre en place*

## Utilisation de l'API
Super-linter donne la possibilité d'utiliser l'API Github pour mettre à jour le statut du commit en fonction des résultats de l'analyse. \
Cela fonctionne aussi avec Gitea, mais avec quelques aménagements à faire.

## Particularités
### Token et permissions
Lors de l'exécution d'un job, Gitea génère un token d'accès à l'API. La documentation associée se trouve ici : https://docs.gitea.com/usage/actions/token-permissions

Pour paramétrer les droits de notre token, nous utiliserons le bloc **permissions**. \
Petite particularité liée à notre usage de Gitea : la permission **statuses** proposée par Github et utilisée par Super-linter n'est pas disponible sur Gitea. A la place, nous devons paramétrer la permission **contents** à *write* plutôt qu'à *read* comme prévu initialement par l'outil.

### Variables d'environnements Github
Même si Gitea propose la plupart des variables d'environnement proposées par Github, il arrive que certaines ne soient pas disponibles.

Dans notre cas, GITHUB_EVENT_PATH n'est pas déclarée alors qu'elle est nécessaire pour le fonctionnement de Super-linter. Il faudra inclure les commandes suivantes pour lui affecter une valeur :

```shell
jq '. + {"forced": false}' "$GITHUB_EVENT_PATH" > event.json
mv event.json "$GITHUB_EVENT_PATH"
```