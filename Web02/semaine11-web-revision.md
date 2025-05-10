# Révision pour le cours Web02

## JavaScript avancé et TypeScript

### JavaScript avancé
- **Promises et async/await**
  - Les Promises permettent de gérer les opérations asynchrones
  - `async/await` simplifie le code asynchrone avec une syntaxe synchrone
  ```javascript
  // Promise example
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));

  // Async/await example
  async function fetchData() {
    try {
      const response = await fetch('https://api.example.com/data');
      const data = await response.json();
      return data;
    } catch (error) {
      console.error(error);
    }
  }
  ```

- **Destructuring**
  - Permet d'extraire des valeurs d'objets ou de tableaux
  ```javascript
  const person = { name: 'John', age: 30 };
  const { name, age } = person;

  const numbers = [1, 2, 3];
  const [first, second] = numbers;
  ```

- **Spread/Rest operators**
  - `...` pour étendre ou regrouper des éléments
  ```javascript
  // Spread
  const arr1 = [1, 2, 3];
  const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

  // Rest
  function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
  }
  ```

- **Modules ES6**
  - Organisation du code en modules réutilisables
  ```javascript
  // Export
  export const PI = 3.14;
  export function square(x) { return x * x; }

  // Import
  import { PI, square } from './math.js';
  ```

### TypeScript

- **Types de base**
  ```typescript
  let name: string = "John";
  let age: number = 30;
  let isActive: boolean = true;
  let ids: number[] = [1, 2, 3];
  let person: [string, number] = ["John", 30]; // Tuple
  ```

- **Interfaces**
  ```typescript
  interface User {
    id: number;
    name: string;
    email?: string; // Propriété optionnelle
  }

  const user: User = {
    id: 1,
    name: "John"
  };
  ```

- **Classes**
  ```typescript
  class Person {
    private name: string;
    
    constructor(name: string) {
      this.name = name;
    }
    
    greet(): string {
      return `Hello, my name is ${this.name}`;
    }
  }
  ```

- **Generics**
  ```typescript
  function getArray<T>(items: T[]): T[] {
    return new Array().concat(items);
  }

  let numArray = getArray<number>([1, 2, 3]);
  let strArray = getArray<string>(["a", "b", "c"]);
  ```

- **Avantages de TypeScript**
  - Détection d'erreurs à la compilation
  - Meilleure autocomplétion et navigation dans le code
  - Documentation intégrée au code source
  - Maintenance plus aisée des applications complexes

## Bibliothèques JavaScript

### React
- **Composants**
  - Unités de base pour construire des interfaces
  - Composants fonctionnels et de classe
  ```jsx
  // Functional component
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }

  // Class component
  class Welcome extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}</h1>;
    }
  }
  ```

- **État (state) et props**
  - Props: données passées d'un composant parent à un enfant
  - State: données gérées à l'intérieur d'un composant
  ```jsx
  function Counter() {
    const [count, setCount] = useState(0);
    
    return (
      <div>
        <p>Compteur: {count}</p>
        <button onClick={() => setCount(count + 1)}>Incrémenter</button>
      </div>
    );
  }
  ```

- **Hooks**
  - `useState`: gérer l'état local
  - `useEffect`: gérer les effets secondaires
  - `useContext`: accéder au contexte
  ```jsx
  function Example() {
    const [count, setCount] = useState(0);
    
    useEffect(() => {
      document.title = `Vous avez cliqué ${count} fois`;
    }, [count]);
    
    return (
      <div>
        <p>Vous avez cliqué {count} fois</p>
        <button onClick={() => setCount(count + 1)}>Cliquez ici</button>
      </div>
    );
  }
  ```

### jQuery
- **Sélection d'éléments**
  ```javascript
  $('#id');            // Sélectionne par ID
  $('.class');         // Sélectionne par classe
  $('div');            // Sélectionne par balise
  $('div.class');      // Sélection combinée
  ```

- **Manipulation du DOM**
  ```javascript
  $('#id').text('Nouveau texte');        // Modifier le texte
  $('.class').html('<p>Contenu HTML</p>'); // Modifier le HTML
  $('div').addClass('highlight');        // Ajouter une classe
  $('p').css('color', 'red');            // Modifier le style
  ```

- **Gestion des événements**
  ```javascript
  $('#button').click(function() {
    alert('Bouton cliqué!');
  });
  
  $('.input').on('change', function() {
    console.log($(this).val());
  });
  ```

- **AJAX avec jQuery**
  ```javascript
  $.ajax({
    url: 'https://api.example.com/data',
    method: 'GET',
    dataType: 'json',
    success: function(response) {
      console.log(response);
    },
    error: function(xhr, status, error) {
      console.error(error);
    }
  });

  // Version simplifiée
  $.get('https://api.example.com/data', function(data) {
    console.log(data);
  });
  ```

### Vue.js
- **Instance Vue et composants**
  ```javascript
  const app = new Vue({
    el: '#app',
    data: {
      message: 'Hello Vue!'
    }
  });

  // Composant Vue
  Vue.component('todo-item', {
    props: ['todo'],
    template: '<li>{{ todo.text }}</li>'
  });
  ```

- **Directives**
  ```html
  <div v-if="seen">Maintenant vous me voyez</div>
  <div v-for="item in items" :key="item.id">{{ item.text }}</div>
  <button v-on:click="doSomething">Cliquez-moi</button>
  <input v-model="message">
  ```

- **Computed properties et watchers**
  ```javascript
  new Vue({
    el: '#app',
    data: {
      message: 'Hello',
      firstName: 'John',
      lastName: 'Doe'
    },
    computed: {
      fullName() {
        return this.firstName + ' ' + this.lastName;
      }
    },
    watch: {
      message(newVal, oldVal) {
        console.log(`Message changé de ${oldVal} à ${newVal}`);
      }
    }
  });
  ```

### Autres bibliothèques populaires
- **Lodash**: Utilitaires pour manipuler des tableaux, objets, etc.
- **Axios**: Client HTTP pour effectuer des requêtes AJAX
- **D3.js**: Bibliothèque pour la visualisation de données
- **Chart.js**: Création de graphiques et diagrammes
- **Moment.js**: Manipulation et formatage de dates
- **Three.js**: Création de graphismes 3D avec WebGL
