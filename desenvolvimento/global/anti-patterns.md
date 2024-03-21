<p align="center">
  <a target="_blank">
    <img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/20210115214527/6-Types-of-Anti-Patterns-to-Avoid-in-Software-Development.png" alt="Clean Code Logo">
  </a>
</p>

# Anti Patterns

## Índice

1. [Introdução](#introdução)
2. [Código Espaguete](#código-espaguete)
3. [Copy-Paste Programming](#copy-paste-programming)
4. [God Object](#god-object)
5. [Design Rigidez](#design-rigidez)
6. [Big Ball of Mud](#big-ball-of-mud)
7. [Golden Hammer](#golden-hammer)
8. [Overengineering](#overengineering)
9. [Not Inventing Here](#not-invented-here)

[VOLTAR](../../README.md)

## Introdução

Padrões anti são práticas comuns no desenvolvimento de software que, apesar de inicialmente parecerem soluções viáveis, acabam resultando em problemas e dificuldades ao longo do tempo. Eles são chamados de "anti-padrões" porque representam abordagens que geralmente são consideradas ineficientes, ineficazes ou até prejudiciais. Aqui estão alguns exemplos comuns de anti-padrões no desenvolvimento de software:

[⬆ voltar ao topo](#índice)

## Código Espaguete

Refere-se a um código desorganizado e complexo, com muitos loops aninhados, estruturas de controle confusas e pouca ou nenhuma modularização. Isso torna o código difícil de entender, manter e estender.

Ao invés disso: Um script com loops aninhados, estruturas de controle confusas e falta de modularização.

```javascript
function processUserData() {
  for (let i = 0; i < users.length; i++) {
    if (users[i].age > 18) {
      console.log(users[i].name + " is an adult.");
    }
  }
}
```

Desta forma: Separar a lógica em funções ou métodos bem definidos, utilizando estruturas de controle claras e evitando a aninhamento excessivo de loops.

```javascript
function isAdult(user) {
  return user.age > 18;
}

function processUserData(users) {
  const adultUsers = users.filter(isAdult);
  adultUsers.forEach((user) => console.log(user.name + " is an adult."));
}
```

[⬆ voltar ao topo](#índice)

## Copy-Paste Programming

Copy-Paste Programming (Programação Copiar-Colar) acontece quando os desenvolvedores copiam e colam blocos de código de um lugar para outro em vez de abstrair a lógica em funções ou componentes reutilizáveis. Isso leva à duplicação de código, tornando-o mais difícil de manter e atualizar.

Ao invés disso: Copiar e colar blocos de código semelhantes em vários lugares do código-base.

```javascript
function calculateCircleArea(radius) {
  return Math.PI * radius * radius;
}

function calculateRectangleArea(width, height) {
  return width * height;
}
```

Desta forma: Abstrair a lógica comum em funções reutilizáveis e chamá-las sempre que necessário, evitando a duplicação de código.

```javascript
function calculateArea(shape) {
  if (shape.type === "circle") {
    return Math.PI * shape.radius * shape.radius;
  } else if (shape.type === "rectangle") {
    return shape.width * shape.height;
  }
}
```

[⬆ voltar ao topo](#índice)

## God Object

O Objeto Deus ou "God Object" refere-se a uma classe que acumula muitas responsabilidades e funcionalidades, tornando-se centralizada demais e dificultando a compreensão e manutenção do código. É uma violação do princípio de responsabilidade única.

Ao invés disso: Uma classe que contém muitos métodos e atributos, realizando várias funcionalidades diferentes.

```javascript
class GodObject {
  constructor() {
    this.handleUser = function (user) {
      // muita lógica aqui
    };
    this.handleProducts = function (products) {
      // muita lógica aqui
    };
    // mais métodos aqui...
  }
}
```

Desta forma: Dividir a funcionalidade em classes menores e mais específicas, cada uma com uma responsabilidade clara e bem definida.

```javascript
class UserManager {
  handleUser(user) {
    // lógica para manipular usuários
  }
}

class ProductManager {
  handleProducts(products) {
    // lógica para manipular produtos
  }
}
```

[⬆ voltar ao topo](#índice)

## Design Rigidez

Isso ocorre quando o código é difícil de modificar devido a um design inflexível. Mudanças simples exigem grandes modificações em várias partes do sistema, o que aumenta o risco de introduzir bugs.

Ao invés disso: Um sistema em que fazer uma pequena alteração requer modificações extensivas em várias partes do código.

```javascript
function calculateTotalPrice(products) {
  let totalPrice = 0;
  for (let i = 0; i < products.length; i++) {
    totalPrice += products[i].price;
  }
  return totalPrice * 1.1; // adicionar 10% de imposto
}
```

Desta forma: Adotar princípios de design como SOLID para criar um código flexível e extensível, de modo que pequenas mudanças possam ser feitas facilmente sem afetar outras partes do sistema.

```javascript
function calculateTotalPrice(products, taxRate) {
  let totalPrice = 0;
  for (let i = 0; i < products.length; i++) {
    totalPrice += products[i].price;
  }
  return totalPrice * (1 + taxRate);
}
```

[⬆ voltar ao topo](#índice)

## Big Ball of Mud

Descreve sistemas que crescem organicamente ao longo do tempo sem uma arquitetura clara ou planejamento adequado. Eles se tornam difíceis de entender e manter devido à falta de estrutura e organização.

Ao invés disso: Um sistema monolítico com pouca ou nenhuma separação entre as preocupações e sem uma estrutura clara.

```javascript
// Código não estruturado e desorganizado
function handleFormSubmission() {
  // Lógica para validar formulário
  // Lógica para enviar dados para o servidor
  // Lógica para atualizar a interface do usuário
  // Lógica para manipular erros
}
```

Desta forma: Utilizar padrões de arquitetura como MVC (Model-View-Controller) ou MVVM (Model-View-ViewModel) para dividir o sistema em componentes distintos com

```javascript
// Refatorar o código em módulos e componentes bem definidos
function validateForm() {
  // Lógica para validar formulário
}

function sendDataToServer() {
  // Lógica para enviar dados para o servidor
}

function updateUI() {
  // Lógica para atualizar a interface do usuário
}

function handleFormSubmission() {
  validateForm();
  sendDataToServer();
  updateUI();
}
```

[⬆ voltar ao topo](#índice)

## Golden Hammer

Isso ocorre quando os desenvolvedores aplicam uma única solução (geralmente uma ferramenta, tecnologia ou padrão de design) a todos os problemas, independentemente de sua adequação. Isso pode levar a soluções sub-ótimas e à falta de consideração de alternativas.

Ao invés disso: Utilizar sempre a mesma biblioteca ou framework para todas as tarefas, independentemente da adequação.

```javascript
// Usando jQuery para manipulação do DOM em um projeto simples onde vanilla JavaScript seria suficiente
$(".submit-btn").click(function () {
  // Lógica para manipular clique do botão
});
```

Desta forma: Avaliar diferentes ferramentas e tecnologias para cada problema específico e escolher aquela que melhor se adapta às necessidades do projeto.

```javascript
// Usando JavaScript nativo para manipulação do DOM
document.querySelector(".submit-btn").addEventListener("click", function () {
  // Lógica para manipular clique do botão
});
```

[⬆ voltar ao topo](#índice)

## Overengineering

Refere-se a uma abordagem excessivamente complexa e elaborada para resolver um problema simples. Isso pode resultar em código inchado, difícil de entender e manter.

Ao invés disso: Criar uma solução complexa e cheia de recursos para um problema simples.

```javascript
// Implementar um sistema de gerenciamento de estado complexo (como Redux) para uma aplicação simples
import { createStore } from "redux";

function reducer(state, action) {
  // Lógica para atualizar o estado com base na ação
}

const store = createStore(reducer);
```

Desta forma: Adotar uma abordagem simples e direta para resolver o problema, evitando adicionar funcionalidades desnecessárias ou complexidade excessiva.

```javascript
// Usar um estado local simples (como useState do React) para uma aplicação simples
let count = 0;

function increment() {
  count++;
  render();
}

function decrement() {
  count--;
  render();
}

function render() {
  console.log(count);
}
```

[⬆ voltar ao topo](#índice)

## Not Invented Here

Isso acontece quando os desenvolvedores rejeitam soluções existentes em favor de criar suas próprias soluções internas, mesmo que soluções externas estejam prontamente disponíveis e sejam melhores.

Ao invés disso: Rejeitar soluções existentes e reinventar a roda desenvolvendo uma solução interna.

```javascript
// Reimplementar uma biblioteca de utilidades internamente, em vez de usar uma biblioteca amplamente adotada como Lodash
function customMap(array, callback) {
  const result = [];
  for (let i = 0; i < array.length; i++) {
    result.push(callback(array[i]));
  }
  return result;
}
```

Desta forma: Avaliar soluções externas disponíveis e utilizar aquela que melhor se adequa aos requisitos do projeto, economizando tempo e recursos.

```javascript
// Utilizar bibliotecas externas como Lodash para funcionalidades comuns
const numbers = [1, 2, 3, 4, 5];
const squares = _.map(numbers, (num) => num * num);
console.log(squares); // Output: [1, 4, 9, 16, 25]
```

[⬆ voltar ao topo](#índice)

Reconhecer e evitar padrões anti é importante para promover uma boa prática de desenvolvimento de software, garantindo a qualidade, manutenibilidade e escalabilidade do código.

## Créditos

- Author - [Creator And Music PRO Developers Team](https://github.com/musicpro-live)
- MusicPRO Website - [MusicPRO Live](https://musicpro.live/sobre)
- CreatorPRO Website - [CreatorPRO Live](https://creatorpro.live)
- Twitter - [@MusicPro](https://twitter.com/musicprolive) [@CreatorPro](https://twitter.com/creatorpro_live)
