# Dia 2

#unidade

No react quando vamos dar uma classe a uma div, não usamos o atributo *class*, utilizamos *className*, já que class é uma palavra reservada do javascript.

## **Importando imagens no react**

O react não entende a forma padrão do html para importar uma imagem ou qualquer outro arquivo, é precisa fazer uma importação estilo javascript.

- Estilo padrão html

      <img src="../assets/images/illustration.svg" alt="imagem">

- Estilo javascript

      import illustrationImg from '../assets/images/illustration.svg' 

      <img src={illustrationImg} alt="imagem" />

## **Roteamento em react**

Para fazermos a navegação entre páginas com o react, utilizaremos o pacote *react-router-dom*.


Importamos os componentes *BrowserRouter* e *Route*.

      import { BrowserRouter, Route } from 'react-router-dom'

Vamos utilizar o componente BrowserRouter e dentro dele utilizamos o componente Route, para criarmos as rotas de acesso. 

      import { BrowserRouter, Route } from 'react-router-dom'

      import { NewRoom } from "./pages/NewRoom";
      import { Home } from "./pages/Home";

      function App() {
      return (
      <BrowserRouter>
            <Route path="/" exact component={ Home } />
            <Route path="/rooms/new" component={ NewRoom } />

      </BrowserRouter>
      );
      }

      export default App;

Passamos como propriedade o caminho e qual componente deve ser acessado.

O *exact* serve para avisar o router-dom, que se ele quiser acessar o componente Home, é preciso acessar exatamente a rota passada (/). Porque sem essa propriedade, o router-dom vai verificar se a rota passada começa com "/".

A propriedade *exact* recebe um valor booleano, se o valor for true, não é necessário passar nada, mas se for false é necessário passar o valor false.

- Sem o exact
      
      function App() {
      return (
      <BrowserRouter>
            <Route path="/" component={ Home } />
            <Route path="/rooms/new" component={ NewRoom } />

      </BrowserRouter>
      );
      }

Se tentarmos acessar a rota "/rooms/new", será carregado os componentes Home e NewRoom, pois a rota passada começa com "/" tambem.

Existem algumas formas de fazermos a navegação entre as páginas com a interação do usuário, por links ou por botões são algumas delas.


### - Por Botão

Utilizando um botão, vamos criar uma função que será acionada quando o usuário clicar no botão e enviara ele para a página desejada.

vamos usar o useHistory importando do react-router-dor.

      import { useHistory } from 'react-router-dom';

Utilizando o useHistory e criando a função de navegação

      export function Home() {

      const history = useHistory();

      function navigateToNewRoom() {
            history.push('/rooms/new');
      }
      
      ...
      }

Criando uma propriedade no botão, seguindo o *Camel case*, para chamar a função criada

      <button onClick={navigateToNewRoom} className="create-room">
            <img src={googleIconImage} alt="Logo do Google" />
            Crie sua sala com o Google
      </button>

### - Por link

Por link simplesmente utilizaremos o componente Link e substituiremos a tag "a" pelo Link

Importando o componente

      import { Link } from 'react-router-dom'

Substituindo a tag "a" pelo componente:

- Com a tag a:

      <p>
            Quer entrar em uma sala já existente? <a href="/">Clique aqui</a>
      </p>

- Com o Link, ao invés do href usamos o to:

      <p>
            Quer entrar em uma sala já existente? <Link to="/">Clique aqui</Link>
      </p>

## **Contextos no react**

Contextos no react são formas de compartilhar informações entre dois ou mais componentes na aplicação, essa informação pode ser qualquer coisa, desde de um texto até uma função.

O contexto permite compartilhar informações entre componentes e funções que podem modificar esses valores passados, e uma vez que esses valores são modificados, todos os lugares que estão utilizando desse valor são modificados também.

Utilizaremos o *createContext* do react e atribuiremos essa função em uma variável. O createContext recebe como parâmetro o formato da informação que será armazenado dentro do contexto.

      import { createContext } from 'react'

      export const TestContext = createContext('')

Será armazenado string no contexto.

Por volta das rotas que poderão acessar o valor do contexto, será utilizado o componente TestContext com o atributo Provider. Todo provider precisa ter a propriedade value, que recebe o valor do contexto.

      <BrowserRouter>
        <TestContext.Provider value={'Teste'}>
          <Route path="/" exact component={ Home } />
          <Route path="/rooms/new" component={ NewRoom } />
        </TestContext.Provider>
      </BrowserRouter>

Tudo que estiver dentro do Provider vai conseguir enxergar os valores do contexto. Ou seja, os componentes Home e NewRoom enxergam e tem acesso aos dados do contexto.

### **Recuperando valores do contexto**

Primeiro é preciso importar o contexto e o hook useContext, para conseguirmos recuperar os valores do contexto.

      import { useContext } from 'react'

      import { TestContext } from '../App'

Recuperando os valores do contexto e mostrando ele

      const value = useContext(TestContext)

      ...
         <h1>{value}</h1>      

Isso pode ser feito no componente Home e no NewRoom, já que estão dentro do provider.


## Hooks

Hooks basicamente são funções que só podem ser utilizadas dentro de componentes e sempre começam com o prefixo "use". useState, useEffect, useContext, ...