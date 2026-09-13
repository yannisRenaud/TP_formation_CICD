# Build de l'application

## Besoin
L'application Angular a besoin d'être buildée pour être utilisée en production. \
Pour éviter de le faire manuellement, nous souhaitons automatiser cette étape dans gitea.

Le déploiement a déjà été automatisé, et l'emplacement pour ajouter les étapes de build est présent dans le fichier *deploy.yml*

## Activer Gitea Actions sur le dépôt
Se rendre sur gitea. Dans la configuration du dépôt front, activer les Actions

## Architecture du fichier deploy.yml
*deploy.yml* est un fichier **workflow**. Ce type de fichier est utilisé par gitea pour faire fonctionner les [Gitea Actions](https://docs.gitea.com/usage/actions/overview)

La syntaxe des workflows est très similaire à celle de Github Actions. Le format utilisé pour ces fichiers est le format  yaml

Syntaxe Github Actions : https://docs.github.com/fr/actions/reference/workflows-and-actions/workflow-syntax

``` yaml
# Le nom du workflow
name: Deploy (main)

# La section "on" permet de définir quels événements déclencheront l'exécution du workflow. Elle peut être poussée beaucoup plus loin en fonction des besoins
# Ici, le déclenchement aura lieu à chaque push sur le dépôt
on: push

# La section "env" permet de déclarer des variables qui pourront être utilisées dans tout le workflow
env:
  AWS_REGION: "${{ secrets.LOCATION_NORMALIZED }}"
  VM_USER: "root-doc"
  VM_HOST: "vmfront-${{ secrets.TEAM_NAME }}.internal.doc.${{ env.AWS_REGION }}"

# Un workflow est composé d'un ou plusieurs jobs
jobs:
  # Ici, le seul job déclaré est le job "deploy"
  deploy:
    # Chaque job tourne sur un conteneur dédié. L'image à utiliser est déclarée par "runs-on"
    runs-on: ubuntu-22.04

    # Un job contient une séquence de tâches appelées "steps"
    steps:
      # "uses" permet de faire appel à une "Action" (du code réutilisable)
      # Ici, on utilise actions/checkout (https://github.com/actions/checkout) qui permet de cloner le dépôt dans le workspace du runner qui exécute notre job
      # @v4 correspond au tag du dépôt qu'on souhaite utiliser
      - uses: actions/checkout@v4
      
      # Ici, on a une step qui exécutera plusieurs commandes (d'où l'utilisation d'un | )
      # ─── Install tools ──────────────────────────────────────────────
      - name: Install tools
        run: |
          apt-get update -qq
          apt-get install -y -qq curl unzip openssh-client
      
      [...]

      # Une step simple, qui exécute une seule commande
      - name: Install dependencies
        run: npm ci
```

## Etapes à ajouter à deploy.yml
### Installer Node.js
Nous allons utiliser pour cela la v3 de l'action [actions/setup-node](https://github.com/actions/setup-node)

Particularité de setup-node par rapport à checkout : il faut fournir la version de node que l'on souhaite utiliser (la 18 dans notre cas) en paramètre avec l'instruction **with** \
Le nom du paramètre à utiliser est à trouver sur la page github de setup-node

### Installer les dépendances
Il faut installer les dépendances du projet avec la commande
`npm ci`

### Build l'application Angular
On utilisera pour cela la commande
`npm run build -- --configuration production`

