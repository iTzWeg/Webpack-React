# Webpack-React
Repositório com configurações base para servidor de desenvolvimento ReactJS
## Prompt
Iniciar o servidor com **NPM Start** no prompt
## Porta Local
para alterar a porta do servidor local
deve ser alterado nos arquivos
### webpack.config.js
`module.exports = {
    devtool: 'sorce-map',
    entry: [
        'react-hot-loader/patch',
        'webpack-dev-server/client?http://localhost:3000',
        'webpack/hot/only-dev-server',
        path.join(__dirname,'src', 'index')
    ],`

**altere a porta na propriedade entry**
#### Server.js

`.listen(3000,(err) =>{
    if(err){
        return console.log(err);
    }
    console.log('Listening on http://localhost:3000');
} )`

**Altere o primeiro parametro de listen**





## Modulo 1 - Parte 2

### Aula M1#A07 - Props

Para passar props devemos utilizar uma sintaxe parecida com as propriedades do HTML quando instanciarmos nosso componente exemplo:
 `<Title name='Wellington de Andrade' />` 
 
 para pegarmos as props usando JSX no arquivo do componente devemos usar **{this.props.NOME_DA_PROP }** na função render exemplo:
 `<div>Olá {this.props.name} </div> `
 


### Aula M1#A08 - Atributos HTML

Algumas propriedades do html tem a mesma sintaxe de palavras reservadas do JS, por isso tem uma forma diferente em JSX como por exemplo o class e o for.

No JSX se usa className e htmlFor respectivamente para esses casos.

#### HTML
`<div ***class***="container"></div>`
`<label ***for**="User>Label</label>`
`<input id='User' type="text">` 

#### JSX (REACT)
`<div ***className***="container"></div>`
`<label ***htmlFor**="User>Label</label>`
`<input id='User' type="text">`


### Aula M1#A09 - getDefaultProps

Caso a propriedade não seja passada no momento da renderização do componente pode ser utilizada a  função getDefaultProps para definir valores padrões para esses casos exemplo:

``` 
getDefaultProps: function () {
    return {
      name: 'Desconhecido'
    }
  },
  ```
 
Após o **createClass**.



### Aula M1#A10 - Outros tipos de dados via props

Para passar outros tipos de dados (!string) devemos utilizar as **{}** por exemplo:

`<Title idade ={18}/>`


### Aula M1#A11 - Rendezirando componentes com funções puras

#### Funções puras :
São funções que independete do(s) parametro(s) passados retornam o mesmo valor.

exemplo
```
function soma(a,b){
return a+ b;
}
```

#### Funções Impuras:
São funções que modificam um objeto ou que retornam um valor diferente mesmo que passe o(s) mesmo(s) parâmetros.
Exemplo:
```
function randomiza(a,b){
return Math.Random(a + b);
}
```

#### Renderizando componentes com funções puras
##### Componente - Função
O componente se torna uma função:
```
const Title =(props) => (
<h1>Olá {`${props.name}`}</h1>
)
```
Observe que as props são recebidas como um parametro e são passadas da mesma forma no render:
```
const App = React.createClass({
  render: function () {
    return (
      <div>Aplicação
        <Title name='Wellington de Andrade' />
        <span>
          Sem props <Title />
        </span>
      </div>
    )
  }
}
```
Pode também ser realizada a seguinte sintax  para extrair as props desejadas.
```
const Title = ({ name }) => (
  <h1>Olá {`${name}`}</h1>
)
```
##### Usando o Default props

Para utilizar o defaultProps com funções puras deve se criar um metodo estático da seguinte forma com as props desejadas:
```
Title.defaultProps = {
name: 'Visitante'
}
```
### Aula M1#A12 - Rendezirando componentes com classes

utilizando classes do EcmaScript 2015(6) podemos renderizar componentes extendendo a classe React.Component:
```
class App extends React.Component {
  render () {
    return (
      <div>
        Aplicação
        <Title name='Programador React' />
      </div>
    )
  }
}
```

### Aula M1#A13 - Conhecendo a prop key.

A prop key é utilizada como um identificador pelo React quando temos varios componentes sendo renderizados dentro de uma iteração.
deve ser um valor unico de identificação que ajuda o react a ser mais performatico e identificar mudanças nos componentes renderizados em tela.
Exemplo:
```
class App extends React.Component {
  render () {
    return (
      <div>
        {['blue', 'red', 'green'].map((square) => (
          <Square key={square} color={square} />
        ))}
      </div>
    )
  }
}
```



####### OBS - Style Objetct React:
Para o React o atributo style quando utilizado inline( propriedade do HTML - STYLE) se torna um objeto com todas propriedades utilizadas pelo CSS com sintaxe do JS. 
```
const Square = ({ color }) => (
  <div style={{
    backgroundColor: color,
    height: '100px',
    width: '100px'
  }}
  />
)
```

### Aula M1#A14 - Problemas ao duplicar uma Key
Quando duplicamos uma Key o React entende que ele é o mesmo objeto que o outro objeto de Key igual.
Como no exemplo:
```
class App extends React.Component {
  render () {
    return (
      <div>
        {['blue', 'red', 'blue'].map((square) => (
          <Square key={square} color={square} />
        ))}
      </div>
    )
  }
}
``` 
Pra evitar esse problema devemos utilizar um identificador unico como por exemplo a posição de um array.

Para implementar esta opção devemos realizar o seguinte código:
```
class App extends React.Component {
  render () {
    return (
      <div>
        {['blue', 'red', 'blue'].map((square,index) => (
          <Square key={index} color={square} />
        ))}
      </div>
    )
  }
}
```
No metodo Map podemos passar um segundo parâmetro com o Index das posições do array [0,1,2...] sendo assim a Key dentro da iteração se torna unica para cada um dos elementos.

### Aula M1#A15 - Eventos
os eventos são escritos Inline no component, os eventos tem a sintaxe de on + Nome do evento (camelCase) exemplo - onClick.
```

class App extends React.Component {
  render () {
    return (
      <div onClick={function (e) {
        alert('clickou')
      }}
      >
        <Square color='red' />
      </div>
    )
  }
}
```
### Aula M1#A16 - A prop Children

Para ter uma maior flexibilidade de seus componentes se pode utilizar a prop Children, onde você coloca um texto e\ou  componentes React ou HTML dentro do seu componente e eles são renderizados. Conforme exemplo:

``` 
class App extends React.Component {
  render () {
    return (
      <div>
        <Button><sapn>Texto Children</sapn></Button>
      </div>
    )
  }
}
``` 

Já o Componente ficará da seguinte forma:
```
const Button = ({ children }) => (
  <button>{children}</button>
)
```

### Aula M1#A17 - Composição

Composição em React pode ser utilizada ou definida como a criação de um componente generico que pode ser utilizado em outros componentes mais especificos.
Como por exemplo:
###### Botão Generico
```
import React from 'react'

const Button = ({ children }) => (
  <button>{children}</button>
)
export default Button

```
###### Botão Like
```

import React from 'react'
import Button from './button'

const ButtonLike = () => (
  <Button>Like</Button>
)

export default ButtonLike
```

Podemos passar props entre estes componentes, como por exemplo funções como no exemplo:
###### Generico 
- Recebe uma Prop handleClick que é uma função para o componentes especifico e chama a propriedade onClick do Html via JSX passando o handleClick.
```
const Button = ({children, hadleClick}) => (
<button onClick ={handleClick}>
{children}
</button>
)
````
###### Especifico
- Passa dentro da tag do componente especifico a prop handleClick com a função como parametro.
```
const ButtonLike = () => (
  <Button handleClick={() => alert('Like')}>Like</Button>
)
```
### Aula M1#A18 - State

State é o estado da sua aplicação, um state não pode ser alterado diretamente e é setado diretamente no constructor, apenas é alterado deixando assim seu componente dinamico atraves da fumlçao setState(this.setState) retornando um objeto.

A Classe fica da seguinte forma:

```
class App extends React.Component {
  constructor () {
    super()
    this.state = {
      text: 'Wellington'
    }
  }

  render () {
    return (
      <div
        className='container' onClick={() => this.setState({
          text: 'Alterado'
        })}
      >
        {this.state.text}
      </div>
    )
  }
}
```

Ao clicar na div o React (Re) renderiza seu componente novamente setando o this.state.text como Alterado.

### Aula M1#A19 - Arrow Functions


- Sintaxe:
```
const sum = (a,b) => a + b;
```
- Motivos:

Deixar o código menos verboso e mais simples.


### Aula M1#A20 - Stateful X Stateless

#### Stateful 
São componentes que manipulam estados, obrigatoriamente tem de ser classes que extendem o Component do React.
- Exemplo:
```

class App extends React.Component {
  constructor () {
    super()
    this.state = {
      color: 'green'
    }
  }

  render () {
    return (
      <div>
        <Square color={this.state.color} />
        {['red', 'green', 'blue'].map((color) => (
          <Button
            key={color}
            handleClick={() => this.setState({ color })}
          >
            {color}
          </Button>
        ))}
      </div>
    )
  }
}
```

O Componente App é um Stateful, pois manipula o State e passa ele como parametro para o Square que o recebe como uma propriedade e é (re) renderizado com a cor do botão selecionada. O Botão por sua vez ao ser clicado altera o state setando ele com o valor de cada botão atribuido no map do array.

#### Stateless
Não manipula estados e podem ser qualquer tipo de componente.

####### Observações e Anotações : Não se deve mudar props de forma manual dentro do componente filho, as props devem vir sempre do componente pai.

- Exemplo:
```
const Square = ({ color }) => (
  <div style={{
    backgroundColor: color,
    height: '100px',
    width: '100px'
  }}
  />
)
Square.defaultProps = {
  color: 'red'
}
```
O Square por sua vez é uma função pura que recebe por parametro uma prop de seu elemento pai, neste exemplo o APP, e renderiza uma div com a cor passada pela prop.

```
const Button = ({ children, handleClick }) => (
  <button onClick={handleClick}>
    {children}
  </button>
)
```
O Button é também uma função pura que recebe dois parametros um children ( Elementos filhos - Aula M1#A16 - A prop Children) e uma prop que é uma função chamada handleClick, o Button é formado por um botão do html que possui como propriedade o onClick que chama a prop handleClick(uma função) e rendezira o children neste caso como texto do botão.

### Aula M1#A20 - Lifecycle dos componentes
####Fluxos:(Metodos - servem para saber momentos especificos da vida do componente)
##### Mountin
####### Montagem do Componente
- componentWillMount - Antes do componente montar
- componentDidMount - Montou

##### Unmounting
####### Desmomtagem do Componente
- componentWillUnmount - Saber quando o componente será desmontado ou removido da tela

##### Updating
####### Atualização
- componentWillReceiveProps(nextProps) - Antes de ser atualizado e recebe os parametros das proximas props.
- shouldComponentUpdate(nextProps, nextState) - Serve para verificar se deve ou não atualizar o component, recebe as próximas props e próximo state - Retorna Bool.
- componentWillUpdate(nextProps, nextState) - Passou do should e ainda vai ser atualizado.
- componentDidUpdate(prevProps, prevState) - Pós atualização.

### Aula M1#A22 - Lifecycle fluxo de montagem/ desmontagem
 - Implementação de exemplo utilizando alguns dos metodos usados na aula acima:
  ###### timer.js
  ``` 
    'use strict'
import React, { Component } from 'react'

class timer extends Component {
  constructor () {
    super()
    this.state = {
      time: 0
    }
  }

  //  componente foi montado
  componentDidMount () {
  //  atribuindo um intervalo para alterar o state time para + 1  a cada 1 sec
    this.timer = setInterval(() => this.setState({ time: this.state.time + 1 })
      , 1000)
  }

  //   quando o componente vai ser desmontado
  componentWillUnmount () {
  //  Apagando o timer para não dar erro ao desmontar o componente
    clearInterval(this.timer)
  }

  render () {
    return (<div>Timer: {this.state.time}</div>)
  }
}
export default timer
```
###### app.js
```
import React from 'react'
import Timer from './timer'

class App extends React.Component {
  constructor () {
    super()
    this.state = {
      showTimer: true
    }
  }

  render () {
    return (
      <div>
        {/* adicionando um condicional se (true && true) mostra o timer */}
        {this.state.showTimer && <Timer />}
        <button
          onClick={() => this.setState({ showTimer: !this.state.showTimer })}
        >
          Show || hide timer
        </button>
      </div>
    )
  }
}
```

--- Comentarios no código -----

    
 
