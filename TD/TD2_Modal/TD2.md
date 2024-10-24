# TD2

## A Tailwind avancé

### 1/ Limitations

#### 1_1 Etat par defaut :

```javascript
function Button({ children, ...restProps }) {
  return (
    <button
      {...restProps}
      className="rounded-lg bg-emerald-600 px-5 py-2 font-semibold text-white hover:bg-emerald-500 active:bg-emerald-700"
    >
      {children}
    </button>
  );
}

export default function App() {
  return (
    <div className="grid h-screen place-content-center">
      <Button className="">Click me</Button>
    </div>
  );
}
```

#### 1_2 Ajout d'une props `className` :

- 🚀 Ajouter la classe `bg-blue-500` dans le composant `Button` à l'aide de la props `className`. Qu'observez-vous ?

Ici l'ajout d'une classe `bg-blue-500` dans le composant `Button` ne fonctionnera pas car la props `className` est définie avant et sera écrasée par l'attribut `className` du composant.

- 🚀 Déplaçons `restProps` à la fin. Qu'observez-vous ?

Ici l'ensemble des classes de l'attribut `className` de `Button` sont écrasés par la props `className`.

#### 1_3 Concaténation des classes Tailwind avec un template literal :

```javascript
// Dans le composant Button
...
className={`rounded-lg bg-emerald-600 px-5 py-2 font-semibold text-white hover:bg-emerald-500 active:bg-emerald-700 ${className}`}
...
```

- 🚀 Concaténation des classes à l'aide du template littéral. Qu'observez-vous ?

Nous avons un conflit entre `bg-emerald-600` et `bg-blue-500`.

- Relancer le serveur. Qu'observez-vous ?

- Idem testez avec `bg-red-500`.

💡 **Remarque** : Les conflits entre les classes Tailwind - apparaissentt avec l'extension _Tailwind CSS IntelliSense_.

⚠️ **Attention** au mode de création des classes dans Tailwind : 'just-in-time compiler' : l'order des classes Tailwind compilées est un 'ordre alphabétique' et non l'ordre de déclaration.

---

### 2/ TailwindMerge

**TailwindMerge** est un outil qui vous permet de fusionner plusieurs classes CSS Tailwind et résout automatiquement les conflits entre les classes en supprimant les classes en conflit avec une classe définie plus tard. C'est particulièrement utile lorsque vous souhaitez remplacer les classes CSS Tailwind dans vos composants.

https://www.npmjs.com/package/tailwind-merge
https://github.com/dcastil/tailwind-merge/blob/v2.0.0/docs/features.md

- Installation

```bash
npm install tailwind-merge

```

- Utilisation

Utilisation simple :

```javascript
// Dans le composant Button
import {twMerge} from "tailwind-merge";

...
className = {twMerge(
  "rounded-lg bg-emerald-600 px-5 py-2 font-semibold text-white hover:bg-emerald-500 active:bg-emerald-700",
  className)}
...
```

Utilisation avec condition :

```javascript
// Dans le composant Button
...
className = {twMerge("rounded-lg bg-emerald-600 px-5 py-2 font-semibold text-white hover:bg-emerald-500 active:bg-emerald-700",
  className,
  active && "bg-gray-600")}
...
```

---

### 3/ Variante de classe

```javascript
const baseClasses = "rounded-md font-medium focus:outline-none";

const variantsLookup = {
  primary:
    "bg-cyan-500 text-white shadow-lg hover:bg-cyan-400 focus:bg-cyan-400 focus:ring-cyan-500",
  secondary:
    "bg-slate-200 text-slate-800 shadow hover:bg-slate-300 focus:bg-slate-300 focus:ring-slate-500",
  danger:
    "bg-red-500 text-white shadow-lg uppercase tracking-wider hover:bg-red-400 focus:bg-red-400 focus:ring-red-500",
  text: "text-slate-700 uppercase underline hover:text-slate-600 hover:bg-slate-900/5 focus:text-slate-600 focus:ring-slate-500",
};

const sizesLookup = {
  small: "px-3 py-1.5 text-sm focus:ring-2 focus:ring-offset-1",
  medium: "px-5 py-3 focus:ring-2 focus:ring-offset-2",
  large: "px-8 py-4 text-lg focus:ring focus:ring-offset-2",
};

export default function Button = ({ variant = "primary", size = "medium", className, ...rest }) => {
  return (
    <button
      {...rest}
      className={twMerge(baseClasses, variantsLookup[variant], sizesLookup[size], className)}
    />
  );
};
```

---

## B Partagez votre state entre différents composants

### 1/ State : Parent vers enfant / Enfant vers parent

Créer un composant `Counter` qui affiche un compteur et un bouton `+1`.


```jsx
import { useState } from "react";

// Composant Parent
export default function App() {
  // State
  const [count, setCount] = useState(0);

  const handleIncrement = () => {
    setCount(count + 1);
  };

  return (
    <div className="flex h-screen flex-col items-center justify-center gap-6">
      <h1 className="text-4xl font-bold">{count}</h1>
      <Compteur increment={handleIncrement} reset={setCount} />
    </div>
  );
}

// Composant Enfant
const Compteur = ({ increment, reset }) => {
  return (
    <>
      <button
        className="rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700"
        onClick={increment}
      >
        Incremente
      </button>
      <button
        className="rounded bg-gray-500 px-4 py-2 font-bold text-white hover:bg-blue-700"
        onClick={() => reset(0)}
      >
        Reset
      </button>
    </>
  );
};
```
```jsx
import { useState } from "react";
import { twMerge } from "tailwind-merge";

// Composant Parent
export default function App() {
  // State
  const [count, setCount] = useState(0);

  const handleIncrement = () => {
    setCount(count + 1);
  };

  return (
    <div className="flex h-screen flex-col items-center justify-center gap-6">
      <h1 className="text-4xl font-bold">{count}</h1>
      <Compteur increment={handleIncrement} reset={setCount} />
    </div>
  );
}

// Composant Enfant
const Compteur = ({ increment, reset }) => {
  return (
    <>
      <Boutton onClick={increment} className="bg-green-500">
        Incrementer
      </Boutton>
      <Boutton onClick={() => reset(0)} className="bg-red-500">
        Reset
      </Boutton>
    </>
  );
};

// Composant Enfant Enfant

const Boutton = ({ children, onClick, className }) => {
  return (
    <button
      className={twMerge(
        "rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700",
        className,
      )}
      onClick={onClick}
    >
      {children}
    </button>
  );
};
```


```jsx
import { useState } from "react";
import { twMerge } from "tailwind-merge";

// Composant Parent
export default function App() {
  // State
  const [count, setCount] = useState(0);

  const handleIncrement = () => {
    setCount(count + 1);
  };

  // Composition
  return (
    <div className="flex h-screen flex-col items-center justify-center gap-6">
      <h1 className="text-4xl font-bold">{count}</h1>
      <Compteur>
        <Boutton onClick={handleIncrement} className={"bg-red-500"}>
          Incrémenter
        </Boutton>
        <Boutton
          onClick={() => {
            setCount(0);
          }}
          className={"bg-gray-500"}
        >
          Reset
        </Boutton>
      </Compteur>
    </div>
  );
}

// Composant Enfant
const Compteur = ({ children }) => {
  return <>{children}</>;
};

// Composant Enfant Enfant

const Boutton = ({ children, onClick, className }) => {
  return (
    <button
      className={twMerge(
        "rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700",
        className,
      )}
      onClick={onClick}
    >
      {children}
    </button>
  );
};
```

## Condition if, constition? true:false , && 
```jsx
import { useState } from "react";
import { twMerge } from "tailwind-merge";

// Composant Parent
export default function App() {
  // State

  const [isOpen, setIsOpen] = useState(false);

  const handleClick = () => {
    setIsOpen(!isOpen);
  };

  return (
    <div className="flex h-screen flex-col items-center justify-center gap-6">
      <Boutton onClick={handleClick}>Open Modale</Boutton>

      {isOpen && <Modale onClick={handleClick}>C'est une Modale</Modale>}
    </div>
  );
}

// Composant Enfant Enfant

const Boutton = ({ children, onClick, className }) => {
  return (
    <button
      className={twMerge(
        "rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700",
        className,
      )}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const Modale = ({ children, onClick }) => {
  return (
    <div
      onClick={onClick}
      className="fixed left-0 top-0 flex h-full w-full items-center justify-center bg-black bg-opacity-50"
    >
      <div className="rounded bg-white p-4">{children}</div>
    </div>
  );
};
```


### Exercices

Reproduire la modale (video1).

### C Formulaires
```jsx
import { useState } from "react";

import { twMerge } from "tailwind-merge";

import Bulle from "./components/icons/Bulle";

export default function App() {
  const [name, setName] = useState("");

  const [isComplete, setIsComplete] = useState(false);

  const handleSubmit = () => {
    setIsComplete(!isComplete);
  };

  const handleInput = (e) => {
    setName(e.target.value);
  };

  const handleResetName = () => {
    setName("");
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <label htmlFor="name">Nom</label>

        <input
          onSubmit={(e) => e.preventDefault()}
          className="border-2 border-indigo-600 p-4"
          type="text"
          placeholder="Entrer votre nom"
          value={name}
          onInput={handleInput}
        />
      </form>

      <Boutton className="mt-4" onClick={handleResetName}>
        Reset
      </Boutton>
      <Boutton className="mt-4" onClick={handleSubmit}>
        Submit
      </Boutton>

      {isComplete && <Modale onClick={handleSubmit}>Bonjour {name}</Modale>}
    </div>
  );
}

// Composant Enfant Enfant

const Boutton = ({ children, onClick, className }) => {
  return (
    <button
      className={twMerge(
        "rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700",
        className,
      )}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const Modale = ({ children, onClick }) => {
  return (
    <div
      onClick={onClick}
      className="fixed left-0 top-0 flex h-full w-full items-center justify-center bg-black bg-opacity-50"
    >
      <div className="rounded bg-white p-4">{children}</div>
    </div>
  );
};

}

// Composant Enfant Enfant

const Boutton = ({ children, onClick, className }) => {
  return (
    <button
      className={twMerge(
        "rounded bg-blue-500 px-4 py-2 font-bold text-white hover:bg-blue-700",
        className,
      )}
      onClick={onClick}
    >
      {children}
    </button>
  );
};

const Modale = ({ children, onClick }) => {
  return (
    <div
      onClick={onClick}
      className="fixed left-0 top-0 flex h-full w-full items-center justify-center bg-black bg-opacity-50"
    >
      <div className="rounded bg-white p-4">{children}</div>
    </div>
  );
};
```


## SUJET TP

## Formulaire d'inscription à la newsletter avec message de réussite et d'erreur.

Choisir une marque/entreprise et son design system sur un des deux sites suivant:
https://designsystems.fr/
https://adele.uxpin.com

On vous demande de construire ce formulaire d'inscription à un bulletin d'information pour cette marque/entreprise en respectant scrupuleusement son design system.
Vos utilisateurs devraient être en mesure de :

- Ajoutez leur e-mail et soumettez le formulaire
- Voir un message de réussite avec leur e-mail après avoir soumis le formulaire avec succès ex: "Merci pour votre abonnement! Votre e-mail `pierre.faire@gtag.com` a bien été ajouté à notre liste d'abonnés."
- Voir les messages de validation/erreur du formulaire si :
  - Le champ est vide
  - L'adresse e-mail n'est pas formatée correctement
- Optimisez l'interface en fonction de la taille de l'écran de l'appareil de l'utilisateur
- Jouez avec les micro-interactions pour rendre l'expérience utilisateur plus agréable (animation, hover, etc.)

Technique ReactJS + TailwindCss + Framermotion
