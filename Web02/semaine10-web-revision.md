# Fiche de révision complète - JavaScript

## Introduction
JavaScript est un langage de programmation dynamique, orienté objet et basé sur des prototypes qui permet d'ajouter de l'interactivité aux pages web. Créé en 1995 par Brendan Eich, il est devenu l'un des trois piliers du développement web moderne aux côtés de HTML et CSS. Aujourd'hui, JavaScript s'utilise aussi bien côté client (navigateur) que côté serveur (Node.js).

## Concepts fondamentaux

### Variables et types de données

#### Déclaration de variables
- **`var`**: Portée de fonction, peut être redéclarée, hoisting complet
- **`let`**: Portée de bloc, ne peut pas être redéclarée, hoisting partiel
- **`const`**: Portée de bloc, ne peut être ni redéclarée ni réassignée, hoisting partiel

```javascript
var x = 10;        // Ancienne façon (à éviter)
let y = 20;        // Variable modifiable
const z = 30;      // Variable constante
```

#### Types de données primitifs
- **String**: Chaînes de caractères
  ```javascript
  const nom = "JavaScript";
  const phrase = `Le langage ${nom} est puissant`;  // Template literals
  ```

- **Number**: Entiers et nombres à virgule flottante
  ```javascript
  const entier = 42;
  const decimal = 3.14;
  const infini = Infinity;
  const pasUnNombre = NaN;
  ```

- **Boolean**: Valeurs true ou false
  ```javascript
  const vrai = true;
  const faux = false;
  ```

- **Undefined**: Valeur d'une variable non définie
  ```javascript
  let nonDefinie;  // valeur est undefined
  ```

- **Null**: Valeur représentant l'absence de valeur
  ```javascript
  const valeurVide = null;
  ```

- **Symbol**: Valeur unique et immuable (ES6+)
  ```javascript
  const symbole = Symbol('description');
  ```

- **BigInt**: Entiers de taille arbitraire (ES2020)
  ```javascript
  const grandNombre = 9007199254740991n;
  ```

#### Types de données complexes
- **Object**: Collection de paires clé-valeur
  ```javascript
  const personne = {
    nom: 'Dupont',
    prenom: 'Jean',
    age: 30
  };
  ```

- **Array**: Collection ordonnée de valeurs
  ```javascript
  const nombres = [1, 2, 3, 4, 5];
  const mixte = [1, "deux", { trois: 3 }, [4]];
  ```

- **Function**: Bloc de code réutilisable
  ```javascript
  function addition(a, b) {
    return a + b;
  }
  ```

#### Conversion entre types
```javascript
// String vers Number
const str = "42";
const num1 = Number(str);    // 42
const num2 = parseInt(str);  // 42
const num3 = +str;           // 42

// Number vers String
const num = 42;
const str1 = String(num);    // "42"
const str2 = num.toString(); // "42"
const str3 = `${num}`;       // "42"

// Vers Boolean
const bool1 = Boolean("");           // false
const bool2 = Boolean(0);            // false
const bool3 = Boolean(null);         // false
const bool4 = Boolean(undefined);    // false
const bool5 = Boolean(NaN);          // false
const bool6 = Boolean("texte");      // true
```

### Opérateurs

#### Opérateurs arithmétiques
```javascript
const a = 10, b = 3;
const addition = a + b;         // 13
const soustraction = a - b;     // 7
const multiplication = a * b;   // 30
const division = a / b;         // 3.3333...
const modulo = a % b;           // 1
const exposant = a ** b;        // 1000
const increment = ++a;          // 11 (pré-incrémentation)
const decrement = b--;          // 3 (post-décrémentation)
```

#### Opérateurs de comparaison
```javascript
const x = 5, y = '5';
x == y;   // true (égalité avec conversion)
x === y;  // false (égalité stricte sans conversion)
x != y;   // false
x !== y;  // true
x > 3;    // true
x <= 5;   // true
```

#### Opérateurs logiques
```javascript
const a = true, b = false;
a && b;   // false (ET logique)
a || b;   // true (OU logique)
!a;       // false (NON logique)

// Court-circuit
const nom = utilisateur && utilisateur.nom;  // évite l'erreur si utilisateur est null/undefined
const valeurParDefaut = valeurPotentielle || 'défaut';
```

#### Opérateur de coalescence des nuls (ES2020)
```javascript
const valeur = null ?? 'défaut';  // 'défaut'
const nombre = 0 ?? 42;           // 0 (car 0 n'est pas null/undefined)
```

#### Opérateur ternaire
```javascript
const age = 20;
const statut = age >= 18 ? 'adulte' : 'mineur';
```

### Structures de contrôle

#### Conditionnelles
```javascript
// If, else if, else
if (condition1) {
  // code exécuté si condition1 est true
} else if (condition2) {
  // code exécuté si condition2 est true
} else {
  // code exécuté si aucune condition n'est true
}

// Switch
const jour = 'lundi';
switch (jour) {
  case 'lundi':
    console.log('Début de semaine');
    break;
  case 'vendredi':
    console.log('Fin de semaine');
    break;
  default:
    console.log('Milieu de semaine');
}
```

#### Boucles
```javascript
// For
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// While
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}

// Do-while
let j = 0;
do {
  console.log(j);
  j++;
} while (j < 5);

// For...of (itération sur les valeurs d'un itérable)
const fruits = ['pomme', 'banane', 'orange'];
for (const fruit of fruits) {
  console.log(fruit);
}

// For...in (itération sur les propriétés énumérables d'un objet)
const personne = { nom: 'Dupont', prenom: 'Jean', age: 30 };
for (const prop in personne) {
  console.log(`${prop}: ${personne[prop]}`);
}
```

### Fonctions

#### Types de déclaration
```javascript
// Déclaration de fonction (hoistée)
function addition(a, b) {
  return a + b;
}

// Expression de fonction
const soustraction = function(a, b) {
  return a - b;
};

// Fonction fléchée (ES6)
const multiplication = (a, b) => a * b;

// Fonction fléchée avec bloc
const division = (a, b) => {
  if (b === 0) throw new Error("Division par zéro");
  return a / b;
};
```

#### Paramètres
```javascript
// Paramètres par défaut (ES6)
function saluer(nom = 'visiteur') {
  return `Bonjour, ${nom} !`;
}

// Rest parameters (ES6)
function somme(...nombres) {
  return nombres.reduce((acc, val) => acc + val, 0);
}
somme(1, 2, 3, 4);  // 10

// Déstructuration des paramètres
function afficherPersonne({ nom, prenom, age }) {
  console.log(`${prenom} ${nom}, ${age} ans`);
}
afficherPersonne({ nom: 'Dupont', prenom: 'Jean', age: 30 });
```

#### Closures
```javascript
function creerCompteur() {
  let compteur = 0;
  return function() {
    compteur++;
    return compteur;
  };
}

const incrementer = creerCompteur();
incrementer();  // 1
incrementer();  // 2
```

#### IIFE (Immediately Invoked Function Expression)
```javascript
(function() {
  const variable = "locale à l'IIFE";
  console.log(variable);
})();
```

### Objets

#### Création et manipulation
```javascript
// Littéral d'objet
const personne = {
  nom: 'Dupont',
  prenom: 'Jean',
  age: 30,
  adresse: {
    rue: '123 rue Principale',
    ville: 'Paris'
  },
  presentation: function() {
    return `Je m'appelle ${this.prenom} ${this.nom}`;
  }
};

// Accès aux propriétés
console.log(personne.nom);           // Dot notation
console.log(personne['prenom']);     // Bracket notation

// Ajout/modification de propriétés
personne.email = 'jean@example.com';
personne['telephone'] = '0123456789';

// Suppression de propriétés
delete personne.age;

// Vérification d'existence de propriété
'nom' in personne;                   // true
personne.hasOwnProperty('email');    // true
```

#### Méthodes avancées
```javascript
// Object.keys(), Object.values(), Object.entries() (ES8)
const keys = Object.keys(personne);              // ['nom', 'prenom', ...]
const values = Object.values(personne);          // ['Dupont', 'Jean', ...]
const entries = Object.entries(personne);        // [['nom', 'Dupont'], ...]

// Object.assign() (ES6)
const personneCopie = Object.assign({}, personne);

// Spread operator (ES9)
const personneClone = { ...personne };

// Object.freeze(), Object.seal()
const objImmuable = Object.freeze({ valeur: 42 }); // Ne peut plus être modifié
const objScelle = Object.seal({ valeur: 42 });     // Peut être modifié mais pas étendu
```

#### Prototypes et héritage
```javascript
// Constructeur d'objet
function Personne(nom, prenom, age) {
  this.nom = nom;
  this.prenom = prenom;
  this.age = age;
}

// Ajout d'une méthode au prototype
Personne.prototype.presentation = function() {
  return `Je m'appelle ${this.prenom} ${this.nom}`;
};

// Création d'une instance
const jean = new Personne('Dupont', 'Jean', 30);

// Héritage prototypal
function Employe(nom, prenom, age, poste) {
  Personne.call(this, nom, prenom, age);
  this.poste = poste;
}

Employe.prototype = Object.create(Personne.prototype);
Employe.prototype.constructor = Employe;

Employe.prototype.presentationPro = function() {
  return `${this.presentation()}, je suis ${this.poste}`;
};
```

#### Classes (ES6)
```javascript
class Personne {
  constructor(nom, prenom, age) {
    this.nom = nom;
    this.prenom = prenom;
    this.age = age;
  }
  
  presentation() {
    return `Je m'appelle ${this.prenom} ${this.nom}`;
  }
  
  static creerAnonyme() {
    return new Personne('Anonyme', '', 0);
  }
}

class Employe extends Personne {
  constructor(nom, prenom, age, poste) {
    super(nom, prenom, age);
    this.poste = poste;
  }
  
  presentationPro() {
    return `${super.presentation()}, je suis ${this.poste}`;
  }
}
```

### Arrays (Tableaux)

#### Création et accès
```javascript
// Création
const nombres = [1, 2, 3, 4, 5];
const tableauVide = [];
const tableauTaille = new Array(5);  // Tableau de 5 éléments vides
const tableauValeurs = new Array(1, 2, 3); // [1, 2, 3]

// Accès par index
const premier = nombres[0];   // 1
const dernier = nombres[nombres.length - 1];  // 5

// Modification
nombres[0] = 10;
```

#### Méthodes de base
```javascript
// Ajout/suppression à la fin
nombres.push(6);     // Ajoute 6 à la fin, retourne la nouvelle longueur
const dernier = nombres.pop();  // Supprime et retourne le dernier élément

// Ajout/suppression au début
nombres.unshift(0);  // Ajoute 0 au début, retourne la nouvelle longueur
const premier = nombres.shift(); // Supprime et retourne le premier élément

// Modification sur une plage
// splice(index de départ, nombre d'éléments à supprimer, éléments à ajouter...)
nombres.splice(1, 2, 'a', 'b');  // Remplace 2 éléments à partir de l'index 1

// Extraction de sous-tableau
// slice(index de début inclus, index de fin exclu)
const sousTableau = nombres.slice(1, 3);
```

#### Méthodes de parcours et transformation
```javascript
const nombres = [1, 2, 3, 4, 5];

// forEach: exécute une fonction pour chaque élément
nombres.forEach((valeur, index, array) => {
  console.log(`Valeur ${valeur} à l'index ${index}`);
});

// map: crée un nouveau tableau en transformant chaque élément
const doubles = nombres.map(x => x * 2);  // [2, 4, 6, 8, 10]

// filter: crée un nouveau tableau avec les éléments qui passent le test
const pairs = nombres.filter(x => x % 2 === 0);  // [2, 4]

// reduce: réduit le tableau à une seule valeur
const somme = nombres.reduce((acc, val) => acc + val, 0);  // 15

// find: retourne le premier élément qui satisfait le test
const premier = nombres.find(x => x > 3);  // 4

// findIndex: retourne l'index du premier élément qui satisfait le test
const index = nombres.findIndex(x => x > 3);  // 3

// some: vérifie si au moins un élément satisfait le test
const auMoinsUn = nombres.some(x => x > 4);  // true

// every: vérifie si tous les éléments satisfont le test
const tous = nombres.every(x => x > 0);  // true
```

#### Autres méthodes utiles
```javascript
// join: concatène les éléments avec un séparateur
const chaine = nombres.join('-');  // "1-2-3-4-5"

// sort: trie le tableau en place
nombres.sort((a, b) => b - a);  // Tri décroissant

// reverse: inverse l'ordre des éléments
nombres.reverse();

// flat (ES2019): aplanit un tableau multi-niveaux
const multi = [1, [2, [3, 4]]];
const aplati = multi.flat(2);  // [1, 2, 3, 4]

// includes (ES7): vérifie la présence d'un élément
nombres.includes(3);  // true
```

### DOM (Document Object Model)

#### Sélection d'éléments
```javascript
// Par ID
const element = document.getElementById('monId');

// Par classe
const elements = document.getElementsByClassName('maClasse');

// Par balise
const paragraphes = document.getElementsByTagName('p');

// Par sélecteur CSS (retourne le premier élément trouvé)
const premier = document.querySelector('.maClasse p');

// Par sélecteur CSS (retourne tous les éléments correspondants)
const tous = document.querySelectorAll('div > p');
```

#### Manipulation du DOM
```javascript
// Création d'éléments
const div = document.createElement('div');
const texte = document.createTextNode('Contenu');

// Ajout d'éléments
div.appendChild(texte);
document.body.appendChild(div);

// Insertion avant un élément
const referenceElement = document.getElementById('reference');
document.body.insertBefore(div, referenceElement);

// Insertion à une position spécifique (Element.insertAdjacentElement)
referenceElement.insertAdjacentElement('beforebegin', div); // avant l'élément
referenceElement.insertAdjacentElement('afterbegin', div);  // premier enfant
referenceElement.insertAdjacentElement('beforeend', div);   // dernier enfant
referenceElement.insertAdjacentElement('afterend', div);    // après l'élément

// Suppression d'éléments
element.remove();  // Méthode moderne
element.parentNode.removeChild(element);  // Méthode compatible
```

#### Manipulation de contenu
```javascript
// innerHTML: contenu HTML
element.innerHTML = '<strong>Nouveau contenu</strong>';

// textContent: contenu textuel (sans formatage HTML)
element.textContent = 'Texte brut';

// value: valeur des éléments de formulaire
document.getElementById('monInput').value = 'Nouvelle valeur';
```

#### Manipulation des attributs
```javascript
// Obtenir un attribut
const href = element.getAttribute('href');

// Définir un attribut
element.setAttribute('title', 'Information');

// Vérifier la présence d'un attribut
element.hasAttribute('disabled');

// Supprimer un attribut
element.removeAttribute('hidden');

// Attributs spéciaux (dataset)
element.dataset.info = 'valeur';  // Crée l'attribut data-info="valeur"
const info = element.dataset.info;  // Récupère la valeur de data-info
```

#### Gestion des classes CSS
```javascript
// classList
element.classList.add('nouvelle-classe');
element.classList.remove('ancienne-classe');
element.classList.toggle('active');  // Ajoute ou supprime selon l'état
element.classList.contains('active');  // Vérifie la présence

// className (ancienne méthode)
element.className = 'classe1 classe2';
```

#### Gestion des styles
```javascript
// Style inline
element.style.color = 'red';
element.style.fontSize = '16px';
element.style.display = 'none';

// Récupération des styles calculés
const styles = window.getComputedStyle(element);
const couleur = styles.color;
```

### Événements

#### Ajout et suppression d'écouteurs d'événements
```javascript
// Méthode moderne (addEventListener)
function handleClick(event) {
  console.log('Cliqué!', event.target);
}

element.addEventListener('click', handleClick);
element.removeEventListener('click', handleClick);

// Syntaxe avec fonction anonyme ou fléchée
element.addEventListener('click', function(event) {
  console.log('Cliqué!');
});

element.addEventListener('click', (event) => {
  console.log('Cliqué avec fonction fléchée!');
});

// Ancien style (à éviter)
element.onclick = function() {
  console.log('Cliqué!');
};
```

#### Types d'événements courants
```javascript
// Souris
element.addEventListener('click', handler);
element.addEventListener('dblclick', handler);
element.addEventListener('mousedown', handler);
element.addEventListener('mouseup', handler);
element.addEventListener('mousemove', handler);
element.addEventListener('mouseover', handler);
element.addEventListener('mouseout', handler);

// Clavier
element.addEventListener('keydown', handler);
element.addEventListener('keyup', handler);
element.addEventListener('keypress', handler);

// Formulaire
element.addEventListener('submit', handler);
element.addEventListener('focus', handler);
element.addEventListener('blur', handler);
element.addEventListener('change', handler);
element.addEventListener('input', handler);

// Document
window.addEventListener('load', handler);
window.addEventListener('DOMContentLoaded', handler);
window.addEventListener('resize', handler);
window.addEventListener('scroll', handler);
```

#### Propagation des événements
```javascript
// Arrêter la propagation (empêche la remontée)
element.addEventListener('click', function(event) {
  event.stopPropagation();
});

// Empêcher le comportement par défaut
element.addEventListener('click', function(event) {
  event.preventDefault();
});

// Capture vs Bubbling
parent.addEventListener('click', handler, true);  // Phase de capture
child.addEventListener('click', handler, false);  // Phase de bubbling (défaut)
```

#### Délégation d'événements
```javascript
// Plutôt que d'attacher un événement à chaque élément...
document.getElementById('liste').addEventListener('click', function(event) {
  if (event.target.tagName === 'LI') {
    console.log('Élément de liste cliqué:', event.target.textContent);
  }
});
```

### Asynchrone

#### Callbacks
```javascript
function chargerDonnees(url, callback) {
  // Code asynchrone
  setTimeout(() => {
    const donnees = { id: 1, nom: 'Exemple' };
    callback(null, donnees);  // null pour l'erreur, données en 2e paramètre
  }, 1000);
}

chargerDonnees('api/donnees', (erreur, donnees) => {
  if (erreur) {
    console.error('Erreur:', erreur);
    return;
  }
  console.log('Données:', donnees);
});
```

#### Promises
```javascript
function chargerDonnees(url) {
  return new Promise((resolve, reject) => {
    // Code asynchrone
    setTimeout(() => {
      const donnees = { id: 1, nom: 'Exemple' };
      if (donnees) {
        resolve(donnees);
      } else {
        reject(new Error('Données non disponibles'));
      }
    }, 1000);
  });
}

chargerDonnees('api/donnees')
  .then(donnees => {
    console.log('Données:', donnees);
    return traiterDonnees(donnees);
  })
  .then(resultat => {
    console.log('Résultat:', resultat);
  })
  .catch(erreur => {
    console.error('Erreur:', erreur);
  })
  .finally(() => {
    console.log('Opération terminée');
  });
```

#### Async/Await (ES2017)
```javascript
async function obtenirDonnees() {
  try {
    const donnees = await chargerDonnees('api/donnees');
    console.log('Données:', donnees);
    
    const resultat = await traiterDonnees(donnees);
    console.log('Résultat:', resultat);
    
    return resultat;
  } catch (erreur) {
    console.error('Erreur:', erreur);
    throw erreur;  // Relance l'erreur
  } finally {
    console.log('Opération terminée');
  }
}

// Appel de la fonction async
obtenirDonnees()
  .then(resultat => console.log('Succès:', resultat))
  .catch(erreur => console.error('Échec:', erreur));
```

#### Fetch API
```javascript
// GET Request
fetch('https://api.exemple.com/donnees')
  .then(response => {
    if (!response.ok) {
      throw new Error(`Erreur HTTP: ${response.status}`);
    }
    return response.json();
  })
  .then(data => console.log('Données:', data))
  .catch(error => console.error('Erreur:', error));

// POST Request
fetch('https://api.exemple.com/donnees', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    nom: 'Jean',
    age: 30
  })
})
.then(response => response.json())
.then(data => console.log('Réponse:', data))
.catch(error => console.error('Erreur:', error));

// Avec async/await
async function envoyerDonnees() {
  try {
    const response = await fetch('https://api.exemple.com/donnees');
    if (!response.ok) {
      throw new Error(`Erreur HTTP: ${response.status}`);
    }
    const data = await response.json();
    console.log('Données:', data);
  } catch (error) {
    console.error('Erreur:', error);
  }
}
```

## Bonnes pratiques

### Variables et portée
- Utiliser `const` par défaut pour les variables qui ne seront pas réassignées
- Utiliser `let` uniquement lorsque la réassignation est nécessaire
- Éviter `var` en raison de son comportement de hoisting et sa portée de fonction
- Déclarer les variables au plus proche de leur utilisation
- Éviter les variables globales pour prévenir les conflits de noms

### Fonctions
- Préférer les fonctions fléchées pour les callbacks et les fonctions anonymes courtes
- Utiliser les paramètres par défaut plutôt que des vérifications conditionnelles
- Nommer clairement les fonctions pour indiquer leur objectif
- Appliquer le principe de responsabilité unique (une fonction = une tâche)
- Favoriser les fonctions pures (sans effets secondaires)

### Code propre
- Utiliser des noms de variables descriptifs (éviter les noms à une lettre sauf pour les itérateurs)
- Respecter une convention de nommage cohérente (camelCase pour les variables/fonctions, PascalCase pour les classes)
- Ajouter des commentaires pour expliquer le "pourquoi", pas le "quoi"
- Utiliser la décomposition pour extraire des valeurs des objets et tableaux
- Privilégier les méthodes de tableau (map, filter, reduce) aux boucles for traditionnelles
- Éviter les longues chaînes de conditions imbriquées

### Gestion d'erreurs
- Utiliser les blocs try/catch pour gérer les erreurs de façon élégante
- Créer des classes d'erreur personnalisées pour des erreurs spécifiques
- Valider les entrées utilisateur avant traitement
- Ne jamais supprimer silencieusement les erreurs (au moins les logger)
- Gérer les cas d'erreur dans les promesses avec .catch()

### Performances
- Éviter les manipulations DOM excessives (regrouper les modifications)
- Utiliser la délégation d'événements pour les listes d'éléments similaires
- Débouncer les événements fréquents comme resize ou scroll
- Préférer les template strings aux concaténations de chaînes avec +
- Éviter de créer inutilement des closures dans des boucles

### Sécurité
- Ne jamais faire confiance aux entrées utilisateur (toujours valider et assainir)
- Éviter d'utiliser eval() ou Function() constructor
- Se méfier de innerHTML avec du contenu non maîtrisé (risque de XSS)
- Utiliser HTTPS pour les requêtes API
- Faire attention aux vulnérabilités CSRF dans les requêtes Ajax

## Ressources complémentaires
- [MDN Web Docs](https://developer.mozilla.org/fr/docs/Web/JavaScript)
- [JavaScript.info](https://javascript.info/)
- [Eloquent JavaScript](https://eloquentjavascript.net/)
- [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS)
- [ESLint](https://eslint.org/) pour l'analyse statique de code