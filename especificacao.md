# Feature Driven Architecture

A Feature Driven Architecture (FDA) é um framework estrutural que ajuda a organizar a base de código para interfaces visuais de uma maneira que permite manter uma velocidade de desenvolvimento constante enquanto a quantidade de recursos está crescendo.

Estes são três tipos de limites que esta especificação define:

- __Sistema de arquivos__ - como nomear arquivos e pastas
- __Dependências__ - quais limites podem depender um do outro
- __Escopo de conhecimento__ - qual limite tem que tipo de conhecimento

## Razão

Temos vários modelos de componentes que nos permitem compor a UI. Temos vários modelos de fluxo de dados que simplificam o trabalho com os dados. E, no entanto, lutamos para construir um aplicativo que permita que muitas pessoas trabalhem em paralelo. Sofremos uma desaceleração exponencial quando a base de código cresce.

O motivo é a falta de acordo sobre a divisão de um aplicativo de uma forma que permita que mais pessoas trabalhem em paralelo e mantenham a complexidade sob controle.

A FDA é a peça que faltava que se baseia em modelos de fluxo de dados e componentes existentes.

Em vez de organizar o código por dados e tipos de abstração, queremos organizar o código com base nos recursos voltados para o usuário que resolvem um problema do usuário. Dessa forma, acreditamos que é mais fácil dimensionar, comunicar e navegar na base de código.

## Metas

**Descoberta e navegação** - veja como o software está estruturado observando o sistema de arquivos. Ajude a encontrar qualquer funcionalidade voltada para o usuário no código.

**Paralelização de trabalho** - permite trabalhar em paralelo com várias pessoas. Reduza o número de conflitos de mesclagem. Reduza o número de discussões sobre onde colocar algum pedaço de código.

**Refatoração** - entenda melhor o escopo de uma mudança. Ganhe muito mais confiança ao alterar um recurso sabendo que ele não afetará outros recursos. Veja quais recursos serão afetados ao alterar uma abstração compartilhada.

**Experimentos** - permite criar e remover recursos experimentais.

## Não-metas

**Language and Framework** - é independente de linguagem e framework. Ele deixa muito espaço para acomodar necessidades específicas de produtos e decisões de design.

**Modelo de fluxo de dados** - é independente do fluxo de dados. O modelo de dados unidirecional, reativo ou de ator não importa, desde que os princípios não sejam quebrados.

**Busca de dados** - é independente da camada de rede.
Websockets ou HTTP, REST, RPC ou GraphQL - não importa, desde que os princípios não sejam quebrados.

## Como

A Feature Driven Architecture define os limites fundamentais: Feature, Cluster, Screen, Shared e Library. Cada conceito segue os princípios fundamentais.

Um conceito de "Feature" é a base da Feature Driven Architecture. Todo o resto existe para apoiá-lo.

Quebrar qualquer princípio descrito nesta arquitetura levará a problemas específicos em sua base de código, e o objetivo aqui é definir os benefícios e as compensações.

## Princípios Fundamentais

1. Princípios fundamentais

    Evite um ponto central de falha, tanto quanto possível.

1. Co-localização

    Localize as dependências o mais próximo possível de seus consumidores.

1. Isolamento

    Os subsistemas devem saber o mínimo possível. Cada pedaço de conhecimento tem um preço de acoplamento.

1. Descartabilidade

    Otimize para facilitar a remoção. A remoção de uma pasta de recursos em uma implementação ideal removeria a maior parte do recurso. O resto deve ser fácil de rastrear e remover de forma limpa.
    
1. Compartilhamento explícito

    Torne o compartilhamento de código entre limites super explícito.

## Feature

> Uma feature é um bloco(s) de construção complexo reutilizável e isolado voltado para o usuário que resolve um problema específico para um usuário.

O escopo da feature geralmente depende do produto e das necessidades organizacionais, mas um feature específica deve ter um escopo claramente definido por seus mantenedores.

[Leia mais sobre como identificar um recurso.](./feature.md)

Uma feature segue estes princípios:

1. Uma feature não pode saber da existência de qualquer outra Feature.

   Este princípio é **o mais importante** e, sem ele, toda a sua arquitetura é considerada quebrada.

1. Uma feature não pode saber sobre a tela em que foi usado.

   Sem ele, você não poderá reutilizar uma Feature em várias telas.

1. Uma feature deve ser coeso.

   Uma feature deve colocar sua implementação no local associado ao nome do feature.

1. Uma feature pode ter dependências.

   Uma feature deve expressar dependências em um formato projetado para ser entendido e fornecido por seus consumidores.

1. Uma feature deve ser descartável.

   Você deve ser capaz de remover um feature sem deixar nenhum resquício para trás.

1. Uma feature deve ser composta.

   Você deve ser capaz de compor várias features na mesma tela ou em telas diferentes sem modificar uma feature.

## Estrutura


```sh
└── src/
    ├── app/                    
    |                           
    ├── components/             
    |   ├── {some-component}/   
    |   ...                     
    |                           
    ├── config/                
    |   ├── {some-config}/        
    |   ...                     
    |                           
    ├── constants/              
    |   ├── {some-constant}/        
    |   ...                     
    |                           
    ├── contexts/               
    |   ├── {some-context}/        
    |   ...                     
    |                           
    ├── feature/         
    |   ├── {some-feature}/        
    |   |   ├── api/            
    |   |   ├── components/          
    |   |   └── contexts/
    |   |   └── hooks/ 
    |   |   └── constants.ts/     
    |   |   └── index.tsx/  
    |   |   └── tpyes.ts/  
    |   |   └── utils.ts/            
    |   ...                 
    |                       
    ├── hooks/                 
    |   ├── {some-hook}/        
    |   ...                 
    |                       
    ├── pages/                 
    |   ├── {some-page}/        
    |   |   ├── lib/            
    |   |   ├── model/          
    |   |   └── ui/             
    |   ...                 
    |                       
    ├── services/              
    |   ├── {some-service}/        
    |   ...                 
    |                       
    ├── styles/                
    |   ├── {some-style}/        
    |   ...                 
    |                       
    ├── types/                 
    |   ├── {some-type}/        
    |   ...                 
    |                       
    ├── utils/                 
    |   ├── {some-util}/        
    |   ...                 
    |                       
    └── index.tsx/          
```


