# **Dia 1**

#together

## **TypeScript**

### **Por que usar?**

Typescript basicamente é javascript com tipação de dados.

O typescript é utilizado para tipar o javascript e padronizar a entrada de dados.

Padronizando o tipo dos dados, a entrada de dados em funções e facilita a manutenção do codigo, pois é possível saber os dados que uma função espera, pela tipagem dela.

Ex: Criando uma tipagem e uma função que recebe como parametro um objeto com a tipagem criada.

      type User = {
        name: string;
        address: {
          city: string;
          uf: string;
        }
      }

      function showWelcomeMessage(user: User) {
        return `Welcome ${user.name} (${user.address.city}) - (${user.address.uf})` 
      }

      showWelcomeMessage({
        name: 'Rian',
        address: {
          city: 'São Paulo',
          uf: 'SP'
        }
      })

## **REACT**

O React trabalha com o conceito de **SPA** (single page aplication), ou seja, Todo o site será renderizado em uma única página.

Temos os arquivos *index.html*, *index.jsx* e *App.jsx*

**o arquivo *index.jsx* vai ser o primeiro arquivo js a ser executado pela aplicação.**

No *index.html* temos somente a div com id root. É dentro dessa div onde será colocado todo o conteúdo da página através de javascript. Mas como é feito isso?

Através do arquivo *index.jsx* que possui o método ReactDOM.render(conteúdo, elemento). Esse é o método responsável por renderizar os componentes escritos em jsx ou tsx e colocar dentro da div do *index.html*.

**O método render é utilizado somente 1 vez na aplicação**

O método recebe 2 argumentos, o conteúdo que deseja mostrar e o elemento que deseja inserir o conteúdo.

JSX ou TSX => HTML escrito dentro de arquivos javascript ou typescript.

Função dentro de função é algo totalmente normal.

### **COMPONENTE**

Componentes são pedaços isolados de código, que quando juntos formam uma aplicação.

Basicamente um componente é uma função que retorna um html.

**Tudo é componente**

O ideal é sempre criar um componente com a primeira letra maiuscula.

ex: Button.tsx

#### **Exportar um componente**

Existem duas formas de exportar um componente:

- export default NomeDoComponente;

      function Button(){
        return(
          <button>Clique aqui</button>
        )
      }

      export default Button;

- export function NomeDoComponente(){}; //Named export

      export function Button(){
        return(
          <button>Clique aqui</button>
        )
      }

A vantagem de usar o named export é que se tivermos importado o componente, e mudarmos o nome desse componente, vai ocorrer um erro na importação, já que o componente importado não existe mais.

Se utilizarmos o export default, esse erro não ocorre e possibilita bugs futuros, já que está importando um componente não existente.

#### **Importando um componente**

- Com export default 

      import Button from './components/Button'

      function App() {
        return (
          <div>
            <Button />
          </div>
        );
      }

      export default App;

- Com named export

      import { Button } from './components/Button'

      function App() {
        return (
          <div>
            <Button />
          </div>
        );
      }

      export default App;

Utilizando o named export é possivel importar mais de um componente de uma vez.

### **PROPRIEDADES**
  
Propriedades são informações que se pode passar para um componente, para se comportar de uma maneira diferente. 

Propriedade é bem parecido aos atributos do html, como o href da tag a.

      <a href="www.google.com" target="_blank">Clique</a>

Passando uma propriedade para o componente:

      function App() {
        return (
          <div>
            <Button text="Botão 1"/>
          </div>
        );
      }

NOME DE PROPRIEDADE SEMPRE EM *CAMEL CASE*

Por estar utilizando typescript é preciso criar uma tipagem para o componente Button, já que ele não espera receber nenhuma propriedade.

      type ButtonProps = {
        text?: string;
      }

Podemos utilizar o "?" para dizer que a propriedade pode ser default.

Por padrão damos o nome da tipagem de NomeDoComponenteProps

As propriedades passadas para o componente são enviadas como argumentos do componente, que é um objeto.

      export function Button(props: ButtonProps) {
        return (
          <button>{props.text || 'Default'}</button>
        )
      }

Sempre que queremos incluir um codigo js dentro do jsx, seja variável, condição, utilizamos { }. Se não utilizarmos será considerado como texto normal.

É possivel enviar diversos tipos de dados como propriedades, int, boolean, array.

- Enviando um int

      function App() {
        return (
          <div>
            <Button text={1} />
          </div>
        );
      }

- Enviando um array de string

      function App() {
        return (
          <div>
            <Button text={['1', '2', '3']} />
          </div>
        );
      }

Todos os componentes tem acesso a propriedade **children**, que é o valor passado como conteúdo do elemento.

- Passando um dado como conteúdo do elemento

      function App() {
        return (
          <div>
            <Button>Clique aqui</Button>
          </div>
        );
      }

- Recebendo o dado pela propriedade children

      type ButtonProps = {
        children?: string;
      }

      export function Button(props: ButtonProps) {
        return (
          <button>{props.children || 'Default'}</button>
        )
      }


Na hora de passar as propriedades para um componente, existem propriedades pre-definidas, por exemplo o atributo href da tag a, ou vc que cria todos os nomes das propriedades?

### **ESTADO**

Estado é uma informação mantida por um componente de dentro do react.

Sempre que tiver uma informação que será alterado ao longo do uso da aplicação pelo usuário é considerado um *estado*.

Sempre que uma informação não permanece com o mesmo valor durante todo o uso da aplicação, é um *estado*, é armazenado um estado. 

Ao criarmos o componente Button a seguir:

      export function Button() {
        let counter = 0

        function increment() {
          counter++;
          console.log(counter)
        }

        return (
          <button onClick={increment}>
            {counter}
          </button>
        )
      }

Quando clicamos no botão, será imprimido no console números subindo de 1 em 1, mas o texto do botão não será alterado como desejado.

Isso porque para o react mostrar uma informação que foi mudada, essa informação não pode ser uma variavel comum.
Ex: let counter. É preciso ser um estado.

- Declarando um Estado

      const [counter, setCounter] = useState(0)

Utilizamos o método useState().

O método useState recebe como argumento o valor inicial desejado do estado.

Retorna um array com duas informações, uma variável que recebe o valor do estado e uma função que altera o valor do estado.

Então utilizamos [ ] para colocar cada dado em uma variável.

- Utilizando estado no componente Button

      import { useState } from "react";

      export function Button() {
        const [counter, setCounter] = useState(0)

        function increment() {
          setCounter(counter + 1)
          console.log(counter)
        }

        return (
          <button onClick={increment}>
            {counter}
          </button>
        )
      }

Agora sim se clicarmos no botão o valor dele será alterado.

### **Dois conceitos importantes do react**

#### Imutabilidades

A partir do momento que uma variável é criada dentro de um estado de um componente, ela não sofre alteração.

Sempre que o valor dessa variável for alterada, na verdade é criada uma nova variavel com esse valor, nunca é feito um alteração. Através do função criado pelo *useState*. 

Esse conceito vem do paradigma da programação funcional.

#### Closure

