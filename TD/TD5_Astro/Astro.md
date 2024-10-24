# Astro

https://astro.build

Astro est un nouveau framework de construction de sites web qui vous permet de créer des sites web rapides et modernes avec JavaScript.

[doc](https://docs.astro.build/fr/guides/)

[Tuto](https://docs.astro.build/fr/tutorial/0-introduction/)

## 1/Créer un projet

```bash
# créez un nouveau projet avec npm
npm create astro@latest
```

Plusieurs options sont disponibles pour la création d'un projet Astro.

**Nous allons débuter par la création d'un projet vide. Sans TS**

Démarrez le serveur de dev

```bash
npm run dev
```

## 2/ Intégrations

Astro prend en charge les intégrations de composants et de bibliothèques populaires.

### 2.1/ Intégration de React

```bash
npx astro add react
```

### 2.2/ Intégration de Tailwind CSS

```bash
npx astro add tailwind
```

## 3/ Mon Premier Blog

Nous allons suivre quelques étapes du tutoriel proposé par Astro.

### 3.1/ Créer une nouvelle page

https://docs.astro.build/fr/tutorial/2-pages/1/

➩ Dans le répertoire `src/pages`, créez un fichier `about.astro`.

# Structure du projet

- public
- src
  - pages
    - index.astro
    - about.astro

Remarques :

- Les fichiers `.astro` sont des fichiers Astro.
- la partie haute du fichier est le **frontmatter**, c'est la zone comprise entre `---`.

➩ Testez votre nouvelle page en démarrant le serveur de développement, et en saisissant l'URL `http://localhost:4321/about`.

➩ Ajouter des liens vers les pages de votre site.

### 3.2/ Créer mon premier article de blog en Markdown

https://docs.astro.build/fr/tutorial/2-pages/2/#ajoutez-des-liens-vers-vos-articles

➩ Créez un répertoire `posts` dans le répertoire `page`.

### 3.3/ Ajouter du contenu dynamique

https://docs.astro.build/fr/tutorial/2-pages/3/

### 3.4/ Styliser votre site

https://docs.astro.build/fr/tutorial/2-pages/4/

### 3.5/ Créer un composant de navigation :

https://docs.astro.build/fr/tutorial/3-components/1/

➩ Créez un composant de navigation : `Navigation.astro` dans le répertoire `src/components`.

```astro
---
---

<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>
```

➩ Importez le composant de navigation dans `src/pages/index.astro` et `src/pages/about.astro`.

```astro
---
import Navigation from '../components/Navigation.astro'
---
  <Navigation />
```

➩ Création d'un composant de `Header` et d'un composant de `Footer`.

### 3.6/ Créer votre première mise en page

https://docs.astro.build/fr/tutorial/4-layouts/1/

### 3.7/ Créez une archive de billets de blog

https://docs.astro.build/fr/tutorial/5-astro-api/1/
