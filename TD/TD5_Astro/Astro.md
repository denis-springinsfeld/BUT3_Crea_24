# Astro

https://astro.build

Astro est un framework de construction de sites web qui vous permet de créer des sites web rapides et modernes avec JavaScript.

[doc](https://docs.astro.build/fr/guides/)

[Tuto](https://docs.astro.build/fr/tutorial/0-introduction/)

---

## 1/ Installation et configuration

### 1.1\_ Installation

```bash
# créez un nouveau projet avec npm
npm create astro@latest
```

Plusieurs options sont disponibles pour la création d'un projet Astro.

**Nous allons débuter par la création d'un projet vide - Sans TS (Type Script)**

Démarrez le serveur de dev

```bash
npm run dev
```

### 1.2\_ Intégrations

Astro prend en charge les intégrations de composants et de bibliothèques populaires.

#### 1.2.1 Intégration de React

```bash
npx astro add react
```

#### 1.2.2 Intégration de Tailwind CSS

```bash
npx astro add tailwind
```

---

## 2/ Mon Premier Blog

Nous allons suivre quelques étapes du tutoriel proposé par Astro.

### 2.1\_ Créer une nouvelle page

https://docs.astro.build/fr/tutorial/2-pages/1/

➩ Dans le répertoire `src/pages`, créez un fichier `about.astro`.

#### Structure du projet

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

### 2.2\_ Créer mon premier article de blog en Markdown

https://docs.astro.build/fr/tutorial/2-pages/2/#ajoutez-des-liens-vers-vos-articles

➩ Créez un répertoire `posts` dans le répertoire `page`.

### 2.3\_ Ajouter du contenu dynamique

https://docs.astro.build/fr/tutorial/2-pages/3/

### 2.4\_ Créer un composant de navigation :

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

### 2.5\_ Créer votre première mise en page

https://docs.astro.build/fr/tutorial/4-layouts/1/

### 2.6\_ Créez une archive de billets de blog

https://docs.astro.build/fr/tutorial/5-astro-api/1/

---

## 3/ Créer un projet Astro à partir du template blog

### 3.1\_ Créer un projet Astro à partir du template blog

### 3.2\_ Content Collections

https://docs.astro.build/fr/guides/content-collections/#définition-dun-slug-personnalisé
