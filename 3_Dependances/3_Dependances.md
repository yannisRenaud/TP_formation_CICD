# Dépendance entre branches

## Besoin
La CYBER vous demande de modifier urgemment la version de rxjs vers la version 15.0.4

## Modifier le front
### Modififaction du front
Créer une branche `feat_modif_front` \
Modifier la version du package rxjs dans package.json

### Build / déploiement
Vérifier le statut du build et du déploiement pour votre nouvelle branche. \
On remarque deux choses :
- le job build a échoué, car la version demandée par la CYBER n'existe pas
- le job déploiement a eu lieu quand même, et a heureusement échoué car l'artifact recherché n'existe pas

Cette situation n'est pas souhaitable : dans le cas où le déploiement aurait lieu quand même sans que le build ait fonctionné, cela reviendrait à déployer une application incomplète ou non-fonctionnelle 

## Nouveau besoin
En s'aidant de [la page de Syntaxe Github Actions](https://docs.github.com/fr/actions/reference/workflows-and-actions/workflow-syntax), modifier deploy.yaml pour ne déclencher le job **deploy** que lorsque le job **build** a pu se terminer en succès.

Observer les changements au niveau du workflow sur Gitea