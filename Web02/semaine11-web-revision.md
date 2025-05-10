# Fiche de révision - Norme ECMAScript

## Introduction
ECMAScript est la spécification standardisée du langage de script dont JavaScript est une implémentation. Elle est maintenue par l'organisation ECMA International.

## Historique et évolution

### ECMAScript 1 (1997)
- Première version standardisée

### ECMAScript 2 (1998) et 3 (1999)
- Améliorations mineures et standardisation des expressions régulières

### ECMAScript 5 (2009)
- Mode strict: `"use strict";`
- Méthodes d'array: `forEach()`, `map()`, `filter()`, `reduce()`
- JSON natif: `JSON.parse()` et `JSON.stringify()`
- Accesseurs de propriétés: getters et setters

### ECMAScript 6 / ES2015
- Déclarations avec `let` et `const`
- Arrow functions: `() => {}`
- Classes: `class Nom {}`
- Modules: `import` et `export`
- Promesses: `Promise`
- Template literals: `` `texte ${variable}` ``
- Déstructuration: `const { prop } = obj`
- Paramètres par défaut et rest: `function(a=1, ...args)`
- Spread operator: `[...array]`

### ECMAScript 2016 (ES7)
- Opérateur exponentiel: `**`
- Méthode `Array.prototype.includes()`

### ECMAScript 2017 (ES8)
- Async/await: `async function() { await ... }`
- `Object.values()`, `Object.entries()`

### ECMAScript 2018 (ES9)
- Rest/Spread pour objets: `{...obj}`
- Promise.finally()

### ECMAScript 2019-2022 (ES10-ES13)
- `Array.flat()` et `Array.flatMap()`
- `Object.fromEntries()`
- Optional chaining: `obj?.prop`
- Nullish coalescing: `??`
- Private class fields: `#propriete`
- Top-level await

## Compatibilité
- Transpileurs (Babel) pour la rétrocompatibilité
- Polyfills pour ajouter des fonctionnalités manquantes

## Bonnes pratiques
- Utiliser les fonctionnalités modernes avec transpilation pour la compatibilité
- Favoriser les constructions déclaratives plutôt qu'impératives
- Profiter de la décomposition et des opérateurs de propagation pour un code plus lisible
- Employer async/await pour gérer l'asynchronisme de manière plus claire