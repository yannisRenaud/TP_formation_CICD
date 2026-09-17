# Branches

## Besoin
La PO de votre équipe vous demande de tester une modification de la couleur de la barre du menu en bleu.

## Modifier la couleur
### Modififaction du front
Créer une branche `feat_menu_bleu` \
Dans front\src\styles.css, changez la valeur de .cgi > background-color en #0d6efd

### Build / déploiement
Vérifier le statut du build et du déploiement pour votre nouvelle branche. \
Rendez-vous sur l'URL du front : c'est très moche, les clients ont arrêté d'acheter des barbecues depuis quelques minutes. 
L'entreprise est proche de la ruine et vous n'aurez pas d'augmentation cette année.

C'est un problème, car en travaillant sur une branche de dev, nous avons cassé l'application en prod 
(l'augmentation aussi, mais c'est une formation CICD)

## Nouveau besoin
Modifier deploy.yaml pour ne déclencher le workflow que lorsqu'on push sur `main`, en s'aidant de [la page de Syntaxe Github Actions](https://docs.github.com/fr/actions/reference/workflows-and-actions/workflow-syntax)
