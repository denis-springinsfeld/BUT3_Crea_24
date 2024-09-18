# Tailwind avancé 2

---

## 4/ Variante de classe

### 4_1 Méthode 1

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

export default function Button(variant = "primary", size = "medium", ...rest) {
  return (
    <button
      {...rest}
      className={`${baseClasses} ${variantsLookup[variant]} ${sizesLookup[size]}`}
    />
  );
}
```

### 4_2 Méthode 2 : Class Variance Autority CVA

https://www.npmjs.com/package/class-variance-authority

https://cva.style/docs/examples/react/tailwind-css

- Installation

```bash
npm i class-variance-authority
```

⚠️ Pour que _Tailwind CSS IntelliSense_ continue à fonctionner, ajoutez au fichier `settings.json`

```json
{
  "tailwindCSS.experimental.classRegex": [
    ["cva\\(([^)]*)\\)", "[\"'`]([^\"'`]*).*?[\"'`]"],
    ["cx\\(([^)]*)\\)", "(?:'|\"|`)([^']*)(?:'|\"|`)"]
  ]
}
```

- Utilisation

```javascript
import { cva } from "class-variance-authority";
const base = "mes classes de base";

const buttonVariants = cva(base, {
  variants: {
    intent: {
      primary: "",
      secondary: "",
      alert: "",
    },
    size: {
      small: "",
      medium: "",
    },
    rounde: {
      rd: "",
      nrd: "",
    },
  },
  compoundVariants: [],
  defaultVariants: {
    intent: "primary",
    size: "medium",
  },
});

export default function ButtonCVA({
  className,
  intent,
  size,
  rounde,
  children,
  ...props
}) {
  return (
    <button
      className={buttonVariants({ intent, size, rounde, className })}
      {...props}
    >
      {children}
    </button>
  );
}
```

---

## TD TP API

### Exercice 1

En utilisant
