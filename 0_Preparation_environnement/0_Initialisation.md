## Mise en place des prérequis

- Accéder à l'instance gitea de sa Team
- Cloner le dépôt des ressources et du front dans le vsCode distant :
    - Truster le dossier pour activer la gestion des sources
    - Ouvrir une console :
```bash
sudo su -
cd /workspaces
git clone https://giteaX.eu-west-3.cgichaos.com/team1/front.git
git clone https://github.com/yannisRenaud/TP_formation_CICD.git
chown -R coder:coder front
chown -R coder:coder TP_formation_CICD/
```


## L'environnement du TP
Environnement du Chaos Game CGI utilisé pour le TP

Une instance par personne, avec url variable (X = numéro de la team) :
- Wiki : http://doc-utilsX.eu-west-3.cgichaos.com/infrastructure.html
- VsCode : https://coderX.eu-west-3.cgichaos.com
- Gitea : https://giteaX.eu-west-3.cgichaos.com

Identifiants à retrouver sur le wiki : http://doc-utilsX.eu-west-3.cgichaos.com/gitea.html + passwords transmis sur teams

## Ce qu'on va utiliser
### Le front
Application web (angular) sur laquelle on fera quelques modifications mineures pour illustrer l'optimisation progressive des étapes d'intégration/déploiement

### Coder (VsCode)
Le VsCode sur lequel vous êtes actuellement, à partir duquel nous modifierons les fichiers du TP

### Gitea
Gitea est une forge logicielle opensource. Chaque team possède une instance gitea dédiée

Nous nous en servirons pour :
- héberger le dépôt git du front
- héberger les ressources du TP (ce que vous êtes en train de lire)
- faire tourner les pipelines que nous allons développer et améliorer dans ce TP, et qui nous permettront de build l'application, la déployer, la tester, l'analyser...