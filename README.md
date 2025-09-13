# React - Notas Introdutórias

Notas de aula sobre conceitos introdutórios de React.js baseadas no tutorial oficial do React.

## Sumário

1. [Criando um Projeto React com Vite](#criando-um-projeto-react-com-vite)
2. [O que é React?](#o-que-é-react)
3. [Criando e Aninhando Componentes](#criando-e-aninhando-componentes)
4. [Escrevendo Markup com JSX](#escrevendo-markup-com-jsx)
5. [Adicionando Estilos](#adicionando-estilos)
6. [Exibindo Dados](#exibindo-dados)
7. [Renderização Condicional](#renderização-condicional)
8. [Renderizando Listas](#renderizando-listas)
9. [Respondendo a Eventos](#respondendo-a-eventos)
10. [Atualizando a Tela](#atualizando-a-tela)
11. [Usando Hooks](#usando-hooks)
12. [Compartilhando Dados Entre Componentes](#compartilhando-dados-entre-componentes)
13. [Próximos Passos](#próximos-passos)

## Criando um Projeto React com Vite

O Vite é uma ferramenta moderna de build que oferece desenvolvimento rápido e otimizado para projetos React. Siga os passos abaixo para criar um novo projeto React com TypeScript usando o Vite:

### Pré-requisitos

- Node.js (versão 18 ou superior)
- npm ou yarn

### Passo a Passo

1. **Criar o projeto**:
   ```bash
   npm create vite@latest meu-app-react -- --template react-ts
   ```

2. **Navegar para o diretório do projeto**:
   ```bash
   cd meu-app-react
   ```

3. **Instalar as dependências**:
   ```bash
   npm install
   ```

4. **Iniciar o servidor de desenvolvimento**:
   ```bash
   npm run dev
   ```

5. **Abrir no navegador**:
   O Vite mostrará uma URL local (geralmente `http://localhost:5173`) onde você pode visualizar seu projeto.

### Estrutura do Projeto

Após criar o projeto, você terá a seguinte estrutura:

```
meu-app-react/
├── public/
├── src/
│   ├── assets/
│   ├── App.css
│   ├── App.tsx
│   ├── index.css
│   ├── main.tsx
│   └── vite-env.d.ts
├── index.html
├── package.json
├── tsconfig.json
└── vite.config.ts
```

As modificações abaixo serão realizadas em `meu-app-react/src/App.tsx` e `meu-app-react/src/App.css`.

## O que é React?

React é uma biblioteca JavaScript para construir interfaces de usuário. Você constrói interfaces complexas a partir de pequenos e isolados pedaços de código chamados "componentes".

React tem alguns tipos diferentes de componentes, mas vamos começar com `React.Component`:

```tsx
import React, { Component } from 'react';

class ShoppingList extends Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Lista de Compras para {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}
```

Usaremos principalmente componentes funcionais com hooks, que são mais modernos:

```tsx
function ShoppingList({ name }: { name: string }) {
  return (
    <div className="shopping-list">
      <h1>Lista de Compras para {name}</h1>
      <ul>
        <li>Instagram</li>
        <li>WhatsApp</li>
        <li>Oculus</li>
      </ul>
    </div>
  );
}
```

A mesma funcionalidade pode ser escrita usando arrow function:

```tsx
const ShoppingList = ({ name }: { name: string }) => {
  return (
    <div className="shopping-list">
      <h1>Lista de Compras para {name}</h1>
      <ul>
        <li>Instagram</li>
        <li>WhatsApp</li>
        <li>Oculus</li>
      </ul>
    </div>
  );
};
```

## Criando e Aninhando Componentes

Componentes React são funções JavaScript que retornam markup. Eles devem começar com letra maiúscula:

```tsx
const MyButton = () => {
  return (
    <button>Eu sou um botão</button>
  );
};
```

Agora você pode aninhar `MyButton` em outro componente:

```tsx
const App = () => {
  return (
    <div>
      <h1>Bem-vindo ao meu app</h1>
      <MyButton />
    </div>
  );
};

export default App;
```

Note que `<MyButton />` começa com letra maiúscula. É assim que você reconhece um componente React. Nomes de componentes React sempre devem começar com letra maiúscula, enquanto tags HTML devem ser minúsculas.

## Escrevendo Markup com JSX

A sintaxe de markup que você viu acima é chamada *JSX*. É opcional, mas a maioria dos projetos React usa JSX pela conveniência.

JSX é mais rígido que HTML. Você deve fechar tags como `<br />`. Seu componente também não pode retornar múltiplas tags JSX. Você deve envolvê-las em um parent compartilhado, como `<div>...</div>` ou um wrapper vazio `<>...</>`:

```tsx
const AboutPage = () => {
  return (
    <>
      <h1>Sobre</h1>
      <p>Olá.<br />Como você está?</p>
    </>
  );
};
```

## Adicionando Estilos

Em React, você especifica uma classe CSS com `className`. Funciona da mesma forma que o atributo `class` do HTML:

```tsx
<img className="avatar" />
```

Então você escreve as regras CSS para ela em um arquivo CSS separado:

```css
/* Em seu CSS */
.avatar {
  border-radius: 50%;
  width: 100px;
  height: 100px;
}
```

React não prescreve como você adiciona arquivos CSS. No caso mais simples, você adiciona uma tag `<link>` ao seu HTML.

## Exibindo Dados

JSX permite colocar markup dentro de JavaScript. Chaves curvas permitem "escapar de volta" para JavaScript para que você possa incorporar alguma variável do seu código e exibi-la para o usuário. Por exemplo, isso exibirá `user.name`:

```tsx
const user = {
  name: 'Ana Silva',
  imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
  imageSize: 90,
};

const Profile = () => {
  return (
    <>
      <h1>{user.name}</h1>
      <img
        className="avatar"
        src={user.imageUrl}
        alt={'Foto de ' + user.name}
        style={{
          width: user.imageSize,
          height: user.imageSize
        }}
      />
    </>
  );
};

export default Profile;
```

## Renderização Condicional

Em React, não há sintaxe especial para escrever condições. Em vez disso, você usará as mesmas técnicas que usa ao escrever código JavaScript regular. Por exemplo, você pode usar uma declaração `if` para incluir JSX condicionalmente:

```tsx
let content;
if (isLoggedIn) {
  content = <AdminPanel />;
} else {
  content = <LoginForm />;
}
return (
  <div>
    {content}
  </div>
);
```

Se você preferir código mais compacto, pode usar o operador `?` condicional. Ao contrário de `if`, funciona dentro de JSX:

```tsx
<div>
  {isLoggedIn ? (
    <AdminPanel />
  ) : (
    <LoginForm />
  )}
</div>
```

Quando você não precisa do branch `else`, também pode usar uma sintaxe lógica `&&` mais curta:

```tsx
<div>
  {isLoggedIn && <AdminPanel />}
</div>
```

## Renderizando Listas

Você dependerá de recursos JavaScript como loops `for` e a função de array `map()` para renderizar listas de componentes.

Por exemplo, digamos que você tenha um array de produtos:

```tsx
const products = [
  { title: 'Repolho', id: 1 },
  { title: 'Alho', id: 2 },
  { title: 'Maçã', id: 3 },
];
```

Dentro do seu componente, use a função `map()` para transformar um array de produtos em um array de itens `<li>`:

```tsx
const listItems = products.map(product =>
  <li key={product.id}>
    {product.title}
  </li>
);

return <ul>{listItems}</ul>;
```

Observe como `<li>` tem um atributo `key`. Para cada item em uma lista, você deve passar uma string ou um número que identifique unicamente esse item entre seus siblings. Geralmente, uma key deve vir de seus dados, como um ID de banco de dados.

## Respondendo a Eventos

Você pode responder a eventos declarando funções *manipuladoras de evento* dentro de seus componentes:

```tsx
const MyButton = () => {
  const handleClick = () => {
    alert('Você clicou em mim!');
  };

  return (
    <button onClick={handleClick}>
      Clique em mim
    </button>
  );
};
```

Observe como `onClick={handleClick}` não tem parênteses no final! Não *chame* a função manipuladora de evento: você só precisa *passá-la para baixo*. React chamará seu manipulador de evento quando o usuário clicar no botão.

## Atualizando a Tela

Frequentemente, você vai querer que seu componente "lembre" de alguma informação e a exiba. Por exemplo, talvez você queira contar o número de vezes que um botão é clicado. Para fazer isso, adicione *state* ao seu componente.

Primeiro, importe `useState` do React:

```tsx
import { useState } from 'react';
```

Agora você pode declarar uma *variável de state* dentro do seu componente:

```tsx
const MyButton = () => {
  const [count, setCount] = useState(0);
  
  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <button onClick={handleClick}>
      Clicado {count} vezes
    </button>
  );
};
```

Você obtém duas coisas de `useState`: o state atual (`count`) e a função que permite atualizá-lo (`setCount`). Você pode nomeá-los como quiser, mas a convenção é escrever `[something, setSomething]`.

## Usando Hooks

Funções que começam com `use` são chamadas *Hooks*. `useState` é um Hook built-in fornecido pelo React. Você pode encontrar outros Hooks built-in na [referência da API do React](https://react.dev/reference/react). Você também pode escrever seus próprios Hooks combinando os existentes.

Hooks são mais restritivos que outras funções. Você só pode chamar Hooks *no topo* de seus componentes (ou outros Hooks). Se você quiser usar `useState` em uma condição ou loop, extraia um novo componente e coloque lá.

## Compartilhando Dados Entre Componentes

No exemplo anterior, cada `MyButton` tinha seu próprio `count` independente, e quando cada botão foi clicado, apenas o `count` para o botão clicado mudou.

Frequentemente, você precisará que componentes *compartilhem dados e sempre sejam atualizados juntos*.

Para fazer ambos os componentes `MyButton` exibirem o mesmo `count` e atualizarem juntos, você precisa mover o state dos botões individuais "para cima" para o componente mais próximo que contém todos eles.

```tsx
import { useState } from 'react';

const App = () => {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <h1>Contadores que atualizam juntos</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
};

const MyButton = ({ count, onClick }: { count: number; onClick: () => void }) => {
  return (
    <button onClick={onClick}>
      Clicado {count} vezes
    </button>
  );
};

export default App;
```

A informação que você passa para baixo dessa forma é chamada *props*. Agora o componente `App` contém o state `count` e o manipulador de evento `handleClick`, e *passa ambos para baixo como props* para cada um dos botões.

## Próximos Passos

Agora você conhece o básico de como escrever código React! Confira o [Tutorial](https://react.dev/learn/tutorial-tic-tac-toe) para colocar isso em prática e construir seu primeiro mini-app com React.

### Recursos Adicionais

- [Documentação Oficial do React](https://react.dev/)
- [Documentação do Vite](https://vite.dev/)
- [TypeScript com React](https://react.dev/learn/typescript)
- [React DevTools](https://react.dev/learn/react-developer-tools)

### Conceitos Avançados para Estudar

- Context API
- useEffect e outros Hooks
- Roteamento com React Router
- Gerenciamento de Estado (Redux, Zustand)
- Testing com Jest e React Testing Library
- Build e Deploy
