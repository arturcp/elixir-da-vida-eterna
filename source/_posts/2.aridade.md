---
title: Aridade
author: Artur Caliendo Prado
keywords: "iniciante, aridade, método barra, função barra, arity"
date: 2020-04-04 16:00:00
tags:
- iniciante
- aridade
- elixir
- arity


---

Lendo sobre Elixir, uma das coisas que me causou estranheza foi o modo como as pessoas fazem referência a uma função em blogs, artigos e redes sociais. Vamos supor que criei uma função chamada `process_file` e que vou escrever sobre ela. Talvez ela seja útil para outras pessoas, não é mesmo?

O que estava esperando encontrar era uma referência exatamente como a que escrevi ali em cima:


```
process_file
```

Porém, o que encontrei na comunidade Elixir foi isso:

```
process_file/1
```

O que é esse `/1`? Pode ser uma coisa trivial e rotineira para quem já se aventura com Elixir e Erlang, mas para quem começou agora fica aquela pulga atrás da orelha. Pior do que isso, não foi tão simples entender de imediato o que era isso já que eu não sabia que isso se chamava **Aridade**.

> Aridade nada mais é do que a quantidade de argumentos de uma função.

Meio anti-clímax, né?

Talvez eu tenha lido sobre isso na faculdade, mas, como tantas outras coisas, apaguei completamente da memória. Esse termo não é só usado na computação, ele vem da Matemática. Da Wikipedia:

> Na matemática a aridade de uma função ou operação é o número de argumentos ou operandos tomados. A aridade de uma relação é o número n de elementos que compõem as n-uplas ordenadas pertencentes à relação.

Eita.


## Mas por que isso?

Resposta curta: sobrecarga de métodos.

Resposta longa:

Em Ruby, se você criar dois métodos com o mesmo nome, mas com parâmetros diferentes, apenas um deles vai funcionar. Por exemplo, vamos definir o método `process_file` duas vezes:

```ruby
def process_file(file_name)
  puts file
end

def process_file(path, file_name)
  puts "#{path}/#{file_name}"
end
```

Se você tentar usar o primeiro método, vai receber `ArgumentError`! Veja só:

```
2.6.4 :017 > process_file('tutorial.md')
Traceback (most recent call last):
        5: from /Users/artur/.rvm/rubies/ruby-2.6.4/bin/irb:23:in `<main>'
        4: from /Users/artur/.rvm/rubies/ruby-2.6.4/bin/irb:23:in `load'
        3: from /Users/artur/.rvm/rubies/ruby-2.6.4/lib/ruby/gems/2.6.0/gems/irb-1.0.0/exe/irb:11:in `<top (required)>'
        2: from (irb):17
        1: from (irb):12:in `process_file'
ArgumentError (wrong number of arguments (given 1, expected 2))
```

O segundo método que criamos (`process_file` com dois parâmetros) tomou o lugar do primeiro (com um parâmetros). Em outras palavras, o Ruby não suporta sobrecarga de métodos.

Quer dizer, dá para criar um comportamento semelhante usando metaprogramação, mas além de ser algo que eu não recomendo, foge completamente do escopo desse post.

Se você programa em C#, por exemplo, talvez o comportamento do Ruby cause certo espanto: você está acostumado com sobrecarga de métodos e provavelmente usa isso com certa frequência, certo?

Em Elixir, assim como em Erlang, é possível fazer a sobrecarga. Por isso, quando as pessoas estão falando sobre uma função, é importante especificar qual é a aridade dela já que funções com aridades diferentes podem ter
implementações diferentes e o incauto leitor pode acabar seguindo por meandros indesejáveis.
