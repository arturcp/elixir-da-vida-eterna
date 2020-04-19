---
title: Por que escolhi Elixir
author: Artur Caliendo Prado
keywords: "iniciante, instalação, elixir, erlang, phoenix"
date: 2020-03-18 07:14:37
tags:
- iniciante
- instalação
- elixir
- erlang
- phoenix

---

Venho namorando a ideia de aprender uma linguagem funcional há algum tempo e alternei entre [Go lang](https://golang.org/) e [Elixir](https://elixir-lang.org/) sem saber para que lado correr.

Trabalho com Ruby on Rails há anos e sabia que a mudança seria menor se optasse pelo caminho dos alquimistas, mas não me decidi até 29/02/2020, dia em que eu participei pela primeira vez do ElugSP.

Outro meetup desses no mesmo dia do mesmo mês, só daqui 4 anos. Tinha de ser um sinal.

A verdade é que foi a comunidade que me ganhou. Não consegui ir no meetup de Go, mas o que vi foi o bastante para escolher qual dos dois caminhos eu iria trilhar.

![Elixir](/images/1/elixir.png)

As palestras foram interessantes, mas foi das pessoas que eu gostei mais. Encontrei a [Elaine Naomi](https://twitter.com/elaine_nw) e o [João Britto](https://twitter.com/noteu), duas pessoas incríveis com quem tive o prazer de trabalhar, direta ou indiretamente, em projetos anteriores. Também troquei algumas palavras com a [Alda Rocha](https://twitter.com/mjcoffeeholick), o [Milhouse](https://twitter.com/renanranelli) e o [Andrew Rosa](https://twitter.com/_andrewhr). Só nomes de peso na comunidade. E as pessoas se engajaram na discussão, me receberam de braços abertos e me deram a energia que faltava para me aventurar no mundo da Química.

JessePinkmanFeelings.

## A comunidade

O que me envolveu mais foi o esforço que a comunidade Elixir está fazendo para crescer de forma **inclusiva**. A história da Elixir Brasil é marcada pela luta em nome das minorias, feita por pessoas que deram tudo de si para que todos se sentissem parte da comunidade, um propósito que aplaudo de pé.

Não tenho a ilusão de que a comunidade é perfeita, mas querer fazê-la do jeito certo é mais do que se vê por aí, um exemplo a ser seguido. Naquele dia decidi que quero fazer parte disso e aqui estou, escrevendo essas primeiras linhas, escritas em português porque um dos tópicos levantados no meetup foi a dificuldade de encontrar material no idioma tupiniquim, sobre como isso dificulta a vida daqueles que não têm o privilégio - financeiro, de tempo, de oportunidade - de aprender inglês.

## Os primeiros passos

Escolha feita, é hora de botar a mão na massa. A primeira coisa a fazer é instalar tudo o que vou precisar para fazer meu primeiro site com Elixir e Phoenix, e para isso bastou uma busca rápida no Google.

Também comecei a ler [Programming Phoenix 1.4](https://www.amazon.com.br/dp/B084NV65T8), de Chris McCord, Bruce Tate e José Valim. O livro leva a gente pela mão e ensina construir nossa primeira aplicação em Phoenix, com exemplos práticos que podem ser aplicados sem muita enrolação.

Para quem veio do Rails, foi uma caminhada leve e agradável na branda aragem do outono.


## Pré-requisitos

Certifique-se de ter o Erlang instalado, ele é um pré-requisito do Elixir. Para saber se você já tem ele na sua máquina, vá ao terminal e execute:

```
erl
```

Você deve ver algo parecido com isso:


> Erlang/OTP 22 [erts-10.7] [source] [64-bit] [smp:8:8] [ds:8:8:10] [async-threads:1] [hipe] [dtrace]

Caso preciso instalar o Erlang, [este site irá te ajudar](https://www.erlang-solutions.com/resources/download.html). Se inglês não for um problema, a [própria documentação do Elixir](https://elixir-lang.org/install.html#installing-erlang) vai guiar você passo-a-passo.


## Elixir

Não vou me alongar explicando como instalar o Elixir uma vez que a [documentação oficial](https://elixir-lang.org/install.html) faz isso de forma detalhada. Se tiver dificuldades com o inglês, não se preocupe: se você procurar pelo seu sistema operacional na página, basta copiar o trecho de código e executar no terminal.

Por exemplo, para instalar no macOS, com Homebrew, basta executar:

```
brew update
brew install elixir
```

O próximo passo é instalar o Hex.

## Hex

Hex é um gerenciador de pacotes usado tanto pelo Erland quanto pelo Elixir. Instalar é bem simples desde que você já tenha o Elixir instalado:

```
mix local.hex
```

Você deve ver isso no seu terminal:


> Are you sure you want to install "https://repo.hex.pm/installs/1.10.0/hex-0.20.5.ez"? [Yn] y
> * creating /Users/<username>/.mix/archives/hex-0.20.5

A versão do hex pode ser diferente quando você instalar, ok?


## Phoenix

Para se certificar que você tem Elixir 1.5 e Erlang 18 (ou versões mais
recentes), execute:

```
elixir -v
```

O resultado vai ser algo parecido com isso:

> Erlang/OTP 22 [erts-10.7] [source] [64-bit] [smp:8:8] [ds:8:8:10] [async-threads:1] [hipe] [dtrace]
>
> Elixir 1.10.2 (compiled with Erlang/OTP 22)

Estou com a versão 22 do Erlang e a 1.10.2 do Elixir. Quase me esqueci de uma coisa importante: você vai precisar de node.js para os assets.

Vá ao terminal e execute:

```
node -v
```

Caso não tenha o node instalado, você pode baixá-lo [no site oficial](https://nodejs.org/pt-br/) - o melhor de tudo é que o site tem uma versão em português.

Agora, tudo o que resta é instalar o Phoenix e rara isso, vamos usar o mix. Se você conhece Ruby, uma boa analogia é que o mix é o Bundler, o RubyGems e o Rake, tudo ao mesmo tempo.

Vá ao terminal e execute:

```
mix archive.install hex phx_new
```

Ele vai pedir uma confirmação e voilá. Estamos prontos para começar. Para criar seu projeto em Phoenix, basta digitar:

```
mix phx.new <nome do projeto>
```

O nome do projeto deve começar com uma letra e ter apenas letras minúsculas, números e o _underscore_ (`_`). Por exemplo: `mix phx.new hello_world`.

```bash
We are almost there! The following steps are missing:

    $ cd hello_world

Then configure your database in config/dev.exs and run:

    $ mix ecto.create

Start your Phoenix app with:

    $ mix phx.server

You can also run your app inside IEx (Interactive Elixir) as:

    $ iex -S mix phx.server
```
--------------------

# Dica do dia

Vale a pena visitar o [Elixir school](http://elixirschool.com/pt/), ele tem me ajudado muito a entender melhor o Elixir.
