# Déploiement automatisé de React avec GitHub Actions

GitHub Pages est un service d'hébergement de site statique qui vous permet d'héberger votre site Web directement à partir d'un référentiel GitHub. C'est une excellente option pour héberger des sites Web statiques, de la documentation et des blogs personnels. 

```https://<username>.github.io/<repository-name>/```


## Projet React

Créer un projet :

```bash
npm create vite@latest
```

## Repo Github
Push votre projet sur Github

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <repository-url>
git push -u origin main
```

## Installation de GitHub Pages

Installer le package gh-pages, qui simplifie le déploiement de votre application React sur GitHub Pages :

```bash
npm install gh-pages --save-dev
```

## Configuration des scripts de déploiement

Dans votre fichier **package.json**, ajoutez les scripts suivants pour automatiser le processus de déploiement :

```bash
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d dist", // here `dist` is the build folder of your project
  "postdeploy": "echo 'Deployment complete!'",
}
```


Dans le fichier **vite.config.js**, ajoutez la configuration suivante pour vous assurer que votre application React est correctement déployée :

```bash
export default defineConfig({
  base: "/<repository-name>/", // add repository name here
  plugins: [react()],
})
```

## Déploiement sur GitHub Pages

Pour déployer votre application React sur GitHub Pages, exécutez la commande suivante :

```bash
npm run deploy
```

Accéder à votre application en utilisant l'URL suivante : https://<username>.github.io/<repository-name>/









