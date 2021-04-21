# Index.js

No `index.js` é onde renderizamos os componentes na div `root` da página `html`, por exemplo:  
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
No início do nosso arquivo, notamos que precisamos importar algumas coisas:
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
```
- Importação do React
- Importação do ReactDOM, Como a nossa DOM do Browser
- Importação de componentes  


Dentro de `ReactDOM.render(<NomeDoComponente />);` onde colocamos todos os nossos componentes!  

**OBS**: dentro de `ReactDOM.render(<NomeDoComponente />);` podemos escrever nosso `html` também diretamente, mas deixamos os nossos componentes fazer isso pra gente!

# Conceitos do React
## Componentes
Para criar um componente, criamos um arquivo `.js` com a primeira letra maiúscula, por exemplo: `NomeDoComponente.js`.  

Podemos criar nosso **componente** da seguinte forma:
```javascript
function App() {
  return (
    <>Conteúdo HTML</>
  );
}

export default App;
```
Note que no final do nosso **componente** `App.js` tem a seguinte linha:
`export default App;`. Isso significa que estamos exportando nosso componente.  

Para renderizar nosso componente no arquivo `index.js` devemos importá-lo da seguinte forma:
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App'; // Importação do nosso componente App.js!

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
Quando precisamos colocar mais de uma tag, precisamos colocar dentro de uma `<div></div>` ou colocar dentro de uma tag sem nome, por exemplo: `<></>`.
```javascript
function App() {
  return (
    <>
      <h1>Daniel Silveira</h1>
      <p>
        Texto de exemplo
      </p>
    </>
  );
}

export default App;
```

Para importar um componente dentro de outro, podemos primeiro exportar o que criamos por exemplo:
```javascript
export default function Button() { // Exportando componente
  return (
    <button>Click me</button>
  )
}
```
E quando formos importar, fazemos da seguinte forma:
```javascript
import Button from "./Button";

function App() {
  return (
    <>
      <Button />
      <Button />
      <Button />
      <Button />
    </>
  );
}

export default App;
```
## Fragmento
O React, permite que você crie uma tag sem nome `<></>`, quando for renderizar mais de uma tag dentro de um componente, por exemplo:
```javascript
function App() {
  return (
    <>
      <Button />
      <Button />
      <Button />
      <Button />
    </>
  );
}
```
# Propriedade
É uma informação que a gente repassa de um componente para outro.  

Quando estamos escrevendo o HTML, temos várias tags. Como exemplo, temos a tag `<img src=""/>` com atributo `src=""` que é o caminho da nossa imagem. No HTML chamamos isso de atributo, no **React** chamamos isso de **Propriedade**.

## Adicionando propriedades
No caso, vamos colocar um texto no botão adicionando a propriedade `title=""`, por exemplo:
```javascript
import Button from "./Button";

function App() {
  return (
    <>
      <Button title="Button 1"/>
      <Button title="Button 2"/>
      <Button title="Button 3"/>
      <Button title="Button 4"/>
      <Button title="Button 5"/>
    </>
  );
}

export default App;
```
E no componente `Button.js`, vamos acessar as propriedades `title=""`.

Todo componente, como é uma função, ele recebe como primeiro parâmetro, as propriedades que estão sendo passadas para o botão:
```javascript
export default function Button(props) {
  return (
    <button>Click me</button>
  )
}
```
As `props` são um objeto javascript, que têm todos os dados que a gente repassa todas as propriedades que a gente passa para o botão em si.  
Sempre quando colocarmos um código entre `{}(chaves)` dentro do HTML, estamos colocando código javascript dentro dele.  
Por exemplo:
```javascript
export default function Button(props) {
  return (
    <button>{props.title}</button>
  )
}
```

## Propriedade Children
Ao invés de recebermos uma propriedade no nosso botão, iremos definir um filho como propriedade.  
Por exemplo:
```javascript
import Button from "./Button";

function App() {
  return (
    <>
      <Button>Button 1</Button>
      <Button>Button 2</Button>
      <Button>Button 3</Button>
      <Button>Button 4</Button>
      <Button>Button 5</Button>
    </>
  );
}
```
Quando usamos este método de incluir como filho, no nosso componente `Button.js`, fazemos da seguinte forma:
```javascript
export default function Button(props) {
  return (
    // <button>{props.title}</button>
    <button>{props.children}</button>
  )
}
```
Então, acessamos o nosso filho dentro do nosso componente `Button.js`
# Estado
 
Uma forma de manipular informações de dentro de um componente.  

## Criando um primeiro estado
 O estado, é uma informação que posso armazenar num componente onde quando um usuário executar uma ação neste, esse valor possa ser alterado.

Para criar um estado no React preciso fazer da seguinte forma:
- Importar o `useState` do React;
```javascript
import { useState } from 'react'
```
Na tag HTML do `<Button></Button>` preciso utilizar a propriedade chamada `onClick`, pois, vai ser onde vou precisar executar uma função que irá incrementar + 1 no nosso counter.  

Então, antes do `return()` da nossa função do componente, podemos criar nossa função de incremento, da seguinte forma:  
```javascript
const [counter, setCounter] = useState(1);

  function increment() {
    setCounter(counter + 1);
  }
```

Dentro da nossa propriedade, vou inserir a função criada antes do return() `<button onClick={increment}>{props.children}</button>`