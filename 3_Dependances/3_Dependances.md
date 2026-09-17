# Dépendance entre branches

## Besoin
La PO de votre équipe vous demande de modifier [modif à trouver]

## Modifier le front
### Modififaction du front
Créer une branche `feat_modif_front` \
[Réaliser la modif en question qui casse le build]

### Build / déploiement
Vérifier le statut du build et du déploiement pour votre nouvelle branche. \
On remarque deux choses :
- le job build a échoué, car [expliquer]
- le job déploiement a eu lieu quand même, et [a échoué, a fonctionné malgré tout ?]

Cette situation n'est pas souhaitable : dans le cas où le déploiement aurait lieu quand même sans que le build ait fonctionné, cela reviendrait à déployer une application incomplète ou non-fonctionnelle 

## Nouveau besoin
En s'aidant de [la page de Syntaxe Github Actions](https://docs.github.com/fr/actions/reference/workflows-and-actions/workflow-syntax), modifier deploy.yaml pour ne déclencher le job **deploy** que lorsque le job **build** a pu se terminer en succès.