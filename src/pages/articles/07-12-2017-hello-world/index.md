---
path: "/hello-world"
date: 2017-07-12T17:12:33.962Z
title: "My First Gatsby Post"
---

![https://cdn-images-1.medium.com/max/1800/1*Ea-TTjr8AKGdsg1nnBsZWw.jpeg](https://cdn-images-1.medium.com/max/1800/1*Ea-TTjr8AKGdsg1nnBsZWw.jpeg)

Photo by Me :D

### React Hooks — Um “Breve” Resumo

Este artigo foi escrito com a finalidade fornecer um resumo dos principais aspectos do _Hooks_ de uma maneira simples e direta para que você já consiga escrever seus primeiros componentes de função. Ele é voltado principalmente a usuários que possuam ao menos o conhecimento básico de React.

Serão abordados os seguintes temas:

- Motivos para usar _Hooks_
- Migrando uma aplicação com componentes de classe
- Definição de um _Hook_
- Estados
- Ciclo de vida
- Criando um _Hook_ customizado

### Por que usar Hooks?

Em grandes projetos que utilizam componentes de classe é comum encontrar lógicas que não se relacionam compartilhando o mesmo método de ciclo de vida, atribuindo complexidade ao componente e dificultando a manutenção. Com o _Hook_ `useEffect` se torna simples a divisão do código em pequenos blocos que possuam apenas conteúdos relacionados.

Em componentes de classes se torna difícil reaproveitar lógicas de estado sem recorrer a frameworks que nos obriga a refatorar o código utilizando diversos _wrappers_ e _reducers_. Em componentes de função isso é resolvido criando o seu próprio _Hook_.

Classes se tornam complexas para diversos desenvolvedores iniciantes, principalmente pelo entendimento do uso do `this`, o código se torna verboso e sempre é necessário se lembrar do _bind_ de _event listeners_.

### Como migrar um projeto para Hooks?

_Hooks_ foi criado para ser totalmente compatível com componentes definidos como classes, podendo em um projeto coexistir componentes de função e de classe que se relacionam.

É possível adotar uma estratégia de adesão gradual desta tecnologia, apenas criando novos componentes em _Hooks_ e refatorando o código antigo apenas quando necessário trabalhar sobre ele.

### O que é um Hook?

_Hook_ é uma função que permite a utlização de recursos do React para lidar com estados e ciclos de vida em um componente de função.

É possível criar um _Hook_ customizado para reaproveitar comportamentos e lógicas de estado que se repetem em diferentes componentes.

> Obs: Um Hook pode ser utilizado apenas em componentes de função.

### Estados

Para lidar com os estados de um componente de função é utilizado o _Hook_ `useState`. Ele recebe como parâmetro o valor inicial do estado a ser utlizado durante a primeira renderização e retorna um par de valores, sendo estes as atuais informações do estado e uma função para atualizá-las.

[https://gist.github.com/TheAlfadur/3dc2f3f0305a24f9f9945e2a56a9a146#file-usestateexample-js](https://gist.github.com/TheAlfadur/3dc2f3f0305a24f9f9945e2a56a9a146#file-usestateexample-js)

[https://codesandbox.io/s/react-hooks-state-exemplo-m6ckx?file=/src/App.js](https://codesandbox.io/s/react-hooks-state-exemplo-m6ckx?file=/src/App.js)

O código acima é um exemplo da utilização do `useState`, para definição do estado de contagem que será inicializado com o valor `0` . É utilizado _desestruturação_ para declaração do estado `count` e sua função de atualização `setCount`_._ Neste componente ao clicar sobre o botão, o valor do estado será incrementado utilizando `setCount`.

Este mesmo exemplo em um componente de classe seria semelhante ao código abaixo:

[https://gist.github.com/TheAlfadur/ea6fb7f897ed86d0d6c962a972ac3fdb#file-classcomponentstateexample-js](https://gist.github.com/TheAlfadur/ea6fb7f897ed86d0d6c962a972ac3fdb#file-classcomponentstateexample-js)

[https://codesandbox.io/s/react-state-exemplo-xst3x?file=/src/App.js](https://codesandbox.io/s/react-state-exemplo-xst3x?file=/src/App.js)

> Obs: leia sobre desestruturação em: https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Atribuicao_via_desestruturacao

Um estado é geralmente utilizado para armazenar _números, textos, vetores_ e _objetos._ Independente do tipo do valor a ser armazenado, a utilização segue o mesmo padrão do primeiro exemplo.

[https://gist.github.com/TheAlfadur/5f40f200d025e8a284b205eda8b03d21#file-usestateexamplewithobject-js](https://gist.github.com/TheAlfadur/5f40f200d025e8a284b205eda8b03d21#file-usestateexamplewithobject-js)

[https://codesandbox.io/s/react-hooks-state-exemplo-ux3l5?file=/src/App.js:0-229](https://codesandbox.io/s/react-hooks-state-exemplo-ux3l5?file=/src/App.js:0-229)

### Ciclo de vida

Diferente de componentes de classe que possuem métodos específicos para cada estágio do ciclo de vida, em componentes de função é utilizado o _Hook_ `useEffect` para lidar efeitos colaterais sobre as renderizações do componente.

No exemplo abaixo será exibido um log com o valor do estado `count` na primeira montagem do componente e toda vez que o mesmo for renderizado novamente. Ao final da execução do efeito e também quando o componente se demontar, o log informando a ocorrência será executado através da função retornada pelo `useEffect`.

[https://gist.github.com/TheAlfadur/484e59414bd01d2c027f207c18c68eb2#file-useeffectexemple-js](https://gist.github.com/TheAlfadur/484e59414bd01d2c027f207c18c68eb2#file-useeffectexemple-js)

[https://codesandbox.io/s/react-hooks-useeffect-exemplo-4k5fc?file=/src/App.js](https://codesandbox.io/s/react-hooks-useeffect-exemplo-4k5fc?file=/src/App.js)

As funções que são retornadas por um `useEffect` são conhecidas como “funções de limpeza”, normalmente usadas para limpar a lógica do componente e remover eventos antes da próxima renderização. É possível compreender sua execução analisando as mensagens de log. Sempre que o estado mudar e uma nova renderização for se iniciar, a função de limpeza será executada antes que o efeito da próxima renderização ocorra.

É possível customizar a execução do efeito através do segundo parâmetro opcional do `useEffect`, para otimizar a performance do componente pulando a execução em momentos não necessários.

No próximo exemplo o efeito que executa o log do contador será iniciado apenas quando o estado `count` for atualizado. O mesmo se aplica ao log sobre o nome da pessoa que será executado na atualização do estado `person`.

[https://gist.github.com/TheAlfadur/30a4f8697d3e3b2b51348bf823af2293#file-useeffectexemple2-js](https://gist.github.com/TheAlfadur/30a4f8697d3e3b2b51348bf823af2293#file-useeffectexemple2-js)

[https://codesandbox.io/s/react-hooks-useeffect-pulando-execucao-exemplo-61yvv?file=/src/App.js:0-599](https://codesandbox.io/s/react-hooks-useeffect-pulando-execucao-exemplo-61yvv?file=/src/App.js:0-599)

No exemplo acima a lógica pertencente a cada um dos estados se mantém separada de forma organizada em dois efeitos distintos, diferente de um componente de classe do qual é nessário que todas as lógicas compartilhem os mesmos métodos de ciclo de vida, fazendo com que as duas lógicas sejam executados em toda renderização do componente. Veja o exemplo abaixo:

[https://gist.github.com/TheAlfadur/ad9bdb369154aaef34f582069159be60#file-classcomponentlifecycleexample-js](https://gist.github.com/TheAlfadur/ad9bdb369154aaef34f582069159be60#file-classcomponentlifecycleexample-js)

[https://codesandbox.io/s/react-ciclo-de-vida-exemplo-gzgh7?file=/src/App.js:0-831](https://codesandbox.io/s/react-ciclo-de-vida-exemplo-gzgh7?file=/src/App.js:0-831)

> Obs: É possível impedir a que os dois logs sejam executados em toda renderização de um componente de classe, ao invés de executar apenas quando o estado referente ao log é atualizado, como ocorre no exemplo em Hooks. Seria necessário aplicar condicionais verificando a mudança do estado, o que tornaria ainda mais confusa a lógica em seu ciclo de vida.

> Obs: É possível simular a execução dos métodos de ciclo de vida componentDidMount e componentWillUnmount em um componente de função passando um vetor vazio [] no segundo parâmetro do useEffect. Desta maneira o valor das dependências do efeito sempre serão as mesmas, garantindo que ele e seu método de limpeza seja executado apenas uma vez.

### Criando seu prório Hook

Com o crescimento de um projeto, é comum durante o desenvolvimento encontrar comportamentos e lógicas de estado que se repetem, normalmente espalhadas em diferentes componentes. Para evitar a redundância do código e facilitar a manuntenção do projeto, em componentes de função, é possível criar e utilizar um _Hook_ personalizado para lidar com a lógica que é compartilhada entre os componentes.

Um exemplo seria a busca pelo tamanho da janela do navegador para lidar com a responsividade. Em projetos _WEB,_ é comum encontrar componentes que necessitam identificar o tamanho da janela para mudar seu comportamento e se adequar ao espaço disponível. O código abaixo ilustra a criação de um _Hook_ customizado, ele nos permite obter a largura atual da janela em qualquer componente de função.

[https://gist.github.com/TheAlfadur/439ffe042cf2e6d6e64bd1c0fb92b3cd#file-usewindowwidth-js](https://gist.github.com/TheAlfadur/439ffe042cf2e6d6e64bd1c0fb92b3cd#file-usewindowwidth-js)

[https://codesandbox.io/s/hook-customizado-0n0gu?file=/src/useWindowWidth.js:0-411](https://codesandbox.io/s/hook-customizado-0n0gu?file=/src/useWindowWidth.js:0-411)

> Obs: useLayoutEffect é um Hook do React que é sempre executado de forma síncrona após a renderização do componente. Muito utilizado para leitura do DOM.

> Obs: É aconcelhável seguir a convenção de utilização do use no início de todo nome de Hook.

Sempre que a dimensão da janela mudar, o evento _resize_ será disparado, atualizando o estado `width` e retornando a largura atual para o componente onde o _Hook_ é usado.

Para demonstrar a utilização do _Hook_, o componente abaixo mudará a descrição de _Desktop_ para _Mobile_ quando a largura da janela estiver abaixo `500px`.

[https://gist.github.com/TheAlfadur/736bc880e20e4535f86593ee0c8caada#file-app-js](https://gist.github.com/TheAlfadur/736bc880e20e4535f86593ee0c8caada#file-app-js)

[https://codesandbox.io/s/hook-customizado-0n0gu?file=/src/App.js](https://codesandbox.io/s/hook-customizado-0n0gu?file=/src/App.js)

A largura atual da janela sempre estará disponível em `width`. Mesmo que a janela seja redimencionada, o `useWindowWidth` manterá o valor atualizado.

### Conclusão

O _Hooks_ é uma alternativa a componentes de classe com o objetivo de simplificar e organizar componentes React. Com códigos simples e bem divididos através do `useEffect`, criando _Hook_ customizado para reaproveitar lógicas de estado que se repetem e até removendo a necessidade do uso do `this` para desenvolvedores iniciantes.

Este é um resumo do básico necessário para a utilização do _Hooks_, sobre este tema podemos encontrar maiores informações e detalhes na própria documentação do [React](https://pt-br.reactjs.org/docs/hooks-intro.html). Agora cabe a você se aventurar nesta brincadeira!