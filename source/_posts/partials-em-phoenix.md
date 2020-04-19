---
title: Partials em Phoenix
author: Artur Caliendo Prado
keywords: "phoenix, elixir, partial, html"
date: 2020-04-19 18:00:00
tags:
- phoenix
- partial
- elixir
- html

---

Criar uma `partial` nada mais é do que separar um pedaço de uma view em um arquivo próprio, seja para facilitar a manutenção do código, seja para reuso.

Vamos supor que temos o seguinte trecho de código HTML:

```html
<section class="inner-section product">
  <div class="container">
    <div class="row margin-top-50">
      <div class="col-12">
        <h1>Quibe de abóbora</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-12 col-md-8 col-md-push-4 product-details-container">
        <p class="no-margin-top">
          Quem não gosta de chegar em casa e comer um jantarzinho delicioso feito em poucos minutos? Se você é como a gente e ama unir praticidade com sabor, vai adorar nosso Quibe de Abóbora.
        </p>

        <div class="row">
          <div class="col-sm-6">
            <p class="no-margin-top">O produto</p>
            <div class="description-data">
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Id, placeat repudiandae! Facilis aspernatur quaerat earum asperiores nostrum totam minima consequuntur ipsum fuga voluptas esse enim nulla dolorum, eaque eligendi iste.
            </div>
            <span class="questionnaire-link-hint">Clique na resposta para encontrar os ingredientes</span>
          </div>

          <div class="col-sm-6">
            <p class="no-margin-top">A empresa</p>
            <p class="description-data">
              <a href="/empresa/mr-veggy">Mr. Veggy</a>
            </p>
            <div class="description-data">
              Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aspernatur totam dicta consequuntur ipsam qui commodi soluta doloremque, sed eius est. Ipsa provident velit, esse reprehenderit distinctio vero assumenda eveniet repudiandae.
            </div>
          </div>
        </div>

        <div class="row">
          <p class="text-center">Produtos relacionados</p>
          <div class="col-xs-12 col-sm-3">
            <a href="/produto/hamburguer-de-ervilha">
              <img src="https://vdeveganca.s3.amazonaws.com/product/image/1/hamburguer-de-ervilha.jpeg">
              <span>Hambúrguer de ervilha</span>
            </a>
          </div>

          <div class="col-xs-12 col-sm-3">
            <a href="/produto/coxinha-de-jaca">
              <img src="https://vdeveganca.s3.amazonaws.com/product/image/2/coxinha-de-jaca.jpg">
              <span>Coxinha de jaca</span>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

São muitas linhas de código, é difícil manter um HTML assim (e, para ser sincero, essa é uma versão simplificada do HTML original, que é mais longo e bem mais verboso).

Contudo, dá para encontrar algumas "sessões" ou "áreas" dentro desse template. Por exemplo, temos uma área que lida apenas com os dados do produto e outra que lida com os dados da empresa que faz esse produto. Pouco depois, temos um bloco inteiro para exibir produtos relacionados.

É algo assim:

```html
<section class="inner-section product">
  <div class="container">
    <div class="row margin-top-50">
      <div class="col-12">
        <h1>Quibe de abóbora</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-12 col-md-8 col-md-push-4 product-details-container">
        <p class="no-margin-top">
          Quem não gosta de chegar em casa e comer um jantarzinho delicioso feito em poucos minutos? Se você é como a gente e ama unir praticidade com sabor, vai adorar nosso Quibe de Abóbora.
        </p>

        <div class="row">
          <div class="col-sm-6">
            <!-- O produto -->
          </div>
          <div class="col-sm-6">
            <!-- A empresa -->
          </div>
        </div>

        <!-- Produtos relacionados -->
      </div>
    </div>
  </div>
</section>
```

Ficou bem mais fácil de encontrar o que a gente procura! Para criar essas sessões nós usamos as partials. Para fazer isso em Rails, nós usamos o método `render`.

```ruby
<%= render 'product', product: product %>
```

O primeiro parâmetro do `render` é o caminho da partial. Por padrão, o nome do arquivo começa com um _underscore_ (_) e tem a extensão `.html.erb`. Nesse caso, dentro da pasta views teríamos que ter uma pasta `products` com o arquivo `_product.html.erb`. Teríamos, então, essas três partials:

_views/products/_product.html.erb_
```html
<p class="no-margin-top">O produto</p>
<div class="description-data">
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Id, placeat repudiandae! Facilis aspernatur quaerat earum asperiores nostrum totam minima consequuntur ipsum fuga voluptas esse enim nulla dolorum, eaque eligendi iste.
</div>
<span class="questionnaire-link-hint">Clique na resposta para encontrar os ingredientes</span>
```
_views/products/_company.html.erb_
```html
<p class="no-margin-top">A empresa</p>
<p class="description-data">
  <a href="/empresa/mr-veggy">Mr. Veggy</a>
</p>
<div class="description-data">
  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aspernatur totam dicta consequuntur ipsam qui commodi soluta doloremque, sed eius est. Ipsa provident velit, esse reprehenderit distinctio vero assumenda eveniet repudiandae.
</div>
```
_views/products/_related_products.html.erb_
```html
<div class="row">
  <p class="text-center">Produtos relacionados</p>
  <div class="col-xs-12 col-sm-3">
    <a href="/produto/hamburguer-de-ervilha">
      <img src="https://vdeveganca.s3.amazonaws.com/product/image/1/hamburguer-de-ervilha.jpeg">
      <span>Hambúrguer de ervilha</span>
    </a>
  </div>

  <div class="col-xs-12 col-sm-3">
    <a href="/produto/coxinha-de-jaca">
      <img src="https://vdeveganca.s3.amazonaws.com/product/image/2/coxinha-de-jaca.jpg">
      <span>Coxinha de jaca</span>
    </a>
  </div>
</div>
```

E nosso HTMl ficou bem menor:

```html
<section class="inner-section product">
  <div class="container">
    <div class="row margin-top-50">
      <div class="col-12">
        <h1>Quibe de abóbora</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-sm-12 col-md-8 col-md-push-4 product-details-container">
        <p class="no-margin-top">
          Quem não gosta de chegar em casa e comer um jantarzinho delicioso feito em poucos minutos? Se você é como a gente e ama unir praticidade com sabor, vai adorar nosso Quibe de Abóbora.
        </p>

        <div class="row">
          <div class="col-sm-6">
            <%= render 'product', product: @product %>
          </div>
          <div class="col-sm-6">
            <%= render 'company', company: @product.company %>
          </div>
        </div>

        <%= render '_related_products', product: @product %>
      </div>
    </div>
  </div>
</section>
```

Estou passando parâmetros para as partials mas, nos exemplos acima, não estou usando eles para nada. Isso porque o que fiz até agora em Rails foi apenas para explicar o conceito das partials, não quero me alongar muito no Rails, afinal de contas estamos aqui para falar de Phoenix, certo?

Acontece que as partials em Phoenix são bem parecidas com as de Rails, pelo que vi até agora.

O equivalente disso:

```ruby
<%= render 'product', product: @product %>
```

em Phoenix, é isso:

```elixir
<%= render "_product.html", assigns %>
```

Alguns pontos importantes:

1. O nome do arquivo passa a ser `_product.html.eex` e não mais `_product.html.erb`
2. O que em Rails nós chamamos de view é uma combinação do que, em Phoenix, chamamos de View e Template.
3. Ali onde eu usei `assigns`, estou enviando todos os dados do template para a partial. Eu poderia passar somente o que eu iria usar, como `product: @product`, por exemplo.
4. Em Rails, usamos o nome da partial sem o _underscore_ na chamada do método render. Em Phoenix (e em Elixir), as coisas são mais explícitas, por isso temos que incluir ele no nome: `_product.html` ao invés de `product.html`.
