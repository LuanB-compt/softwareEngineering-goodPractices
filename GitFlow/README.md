<h1 style="text-align:center">
    <b>GIT FLOW - Git Branching Model</b>
</h1>




<br>
<br>
<hr>
<br>
<br>




# <center>**INTRODUÇÃO**</center>

- ## **POR QUE SEGUIR UM SEGUIR UM GIT FLOW**
<p style="text-align:justify">
    Para todos que utilizam o Git como ferramenta de controle de versão para seus softwares, já devem ter observado as várias maneiras de como controlar branches de repositórios. É corriqueiro pessoas utilizarem apenas uma <i>branch</i> para fazer <i>commits</i> em projetos pessoais, o que não é errado, pois quando estamos trabalhando sozinhos é mais tranquilo de se controlar tudo em um branch só.
</p>
<p style="text-align:justify">
    Entretanto, o cenário se torna totalmente diferente e mais complexo quando estamos trabalhando com mais contribuidores em um projeto.
</p>
<pre>
    Em todo projeto real, é importantíssimo que se tenha controle total do que está sendo produzido por uma equipe de pessoas desenvolvedoras, onde, ao <b>mesmo tempo</b>, são feitas muitas coisas, como: implementação de novas funcionalidades, correção de falhas, lançamento de versões, etc. E é justamente aqui, que o Git Flow entra para nos ajudar, facilitando o desenvolvimento compartilhado de código com pessoas desenvolvedoras.
</pre>

<br>

- ## **QUAL MODELO IREMOS USAR**
<p style="text-align:justify">
    Publicado em 2010, pelo engenheiro de software holandês, Vincent Driessen, o objetivo do <i>Git Branching Model</i> era melhorar as organizações das <i>branches</i> dentro de repositórios e, desta forma, dar mais fluidez ao processo de desenvolvimento de novas funcionalidades, correções de bugs e lançamentos de versões.
</p>




<br>
<br>
<hr>
<br>
<br>




# <center>**GIT FLOW**</center>
<div style="text-align:center">
    <img src="./gitflow.jpg" height="1000px">
    <br>
    <p><b><i>Imagem prática do workflow do modelo</i></b></p>
</div>

<br>

- ## **BRANCHES PRINCIPAIS**
<p style="text-align:justify">
    O repositório contém duas <i>branches</i> principais com um 'tempo de vida infinito', a <code>main</code> e a <code>develop</code>. Quando o código-fonte na <i>branch</i> <code>develop</code> atinge um ponto estável e está pronto para uma nova <i>release</i>, todas as alterações devem ser fundidas de novo na <code>main</code> e depois receber uma tag com um número da versão.
</p>
<p style="text-align:justify">
    Ainda, as <i>branchs</i> principais <b>não</b> recebem <i>commits</i> diretamente! Apenas <i>merges</i> e <i>Pull Requests</i>.
</p>

<br>

### `main`
<p style="text-align:justify">
    Consideramos <code>origin/master</code> como a <i>branch</i> principal onde o código fonte de HEAD reflecte sempre um estado pronto para produção.
</p>

<br>
    
### `develop`
<p style="text-align:justify">
    Consideramos <code>origin/develop</code> como sendo a <i>branch</i> principal onde o código fonte de HEAD reflecte sempre um estado com as últimas alterações de desenvolvimento entregues para a próxima <i>release</i>.
</p>

<br>

- ## **BRANCHES AUXILIARES**
<p style="text-align:justify">
    Este modelo de desenvolvimento utiliza uma variedade de <i>branches</i> de apoio para ajudar o desenvolvimento paralelo entre os membros da equipe, facilitar o acompanhamento das <i>features</i>, preparar as <i>releases</i> em produção e ajudar a resolver rapidamente problemas de produção em tempo real. Ao contrário das <i>branches</i> principais, estas <i>branches</i> têm sempre um tempo de vida limitado.
</p>
<p style="text-align:justify">
    Estas <i>branches</i> recebem <i>commits</i> diretamente.
</p>

<br>

### `feature`
```
- Branch pai: develop
- Branch que recebe o merge: develop
- Name branch pattern: feat-{nome da funcionalidade}
```
<p style="text-align:justify">
    As <code>feature branches</code> são utilizados para desenvolver novas <i>features</i> para a próxima versão ou para uma versão futura distante. Ao iniciar o desenvolvimento de uma <i>feature</i>, a versão alvo na qual esta funcionalidade será incorporada pode ser desconhecida nesse momento. A essência de uma <i>feature branch</i> é que ele existe enquanto a <i>feature</i> estiver em desenvolvimento, mas eventualmente será fundido de volta a <code>develop</code> (para adicionar definitivamente a nova <i>feature</i> à próxima versão) ou descartado (no caso de uma experiência sem sucesso).
</p>

<br>

### `release`
```
- Branch pai: develop
- Branch que recebe o merge: main e develop
- Name branch pattern: release-{versão}
```
<p style="text-align:justify">
    As <code>release branches</code> apoiam a preparação de uma nova <i>release</i> de produção. Permitem que se ponham os pontos nos "i's" e se cruzem os "t's" de última hora. Além disso, permitem pequenas correcções de <i>bugs</i> e a preparação de meta-dados para uma <i>release</i> (número de versão, datas de <i>builds</i>, etc.). Ao fazer todo este trabalho numa <code>release branch</code>, a <code>develop</code> fica livre para receber <i>features</i> para a próxima grande <i>release</i>.
</p>
<p style="text-align:justify">
    O momento chave para ramificar uma nova <code>release branch</code> a partir da <code>develop</code> é quando o desenvolvimento (quase) reflete o estado desejado da nova <i>release</i>. Pelo menos todas as <i>features</i> que são direcionadas para a versão a ser construída devem ser mescladas na <code>develop</code> neste momento. Todas as <i>features</i> direcionadas para <i>releases</i> futuras não podem - têm de esperar até que a <code>release branch</code> seja ramificada.
</p>
<p style="text-align:justify">
    É exatamente no início de uma <code>release branch</code> que o próximo lançamento recebe um número de versão. Até esse momento, a <code>develop</code> reflecte as alterações para a "próxima <i>release</i>", mas não é claro se esse "próxima <i>release</i>" irá eventualmente tornar-se 0.3 ou 1.0, até que a <code>release branch</code> seja iniciada. Essa decisão é tomada no início da <code>release branch</code> e é levada pelas regras do projeto sobre o aumento do número de versões.
</p>

<br>

### `hotfix`
```
- Branch pai: main
- Branch que recebe o merge: main e develop
- Name branch pattern: hotfix-{nome da correção}
```
<p style="text-align:justify">
    Os <code>hotfix branches</code> são muito parecidos com as <code>release branches</code>, na medida em que também se destinam a preparar uma nova <i>release</i> de produção, embora não planejado. Eles surgem da necessidade de agir imediatamente sobre um estado indesejado de uma versão de produção ativa. Quando um <i>bug</i> crítico numa versão de produção tem de ser resolvido imediatamente, uma <code>hotfix branch</code> pode ser ramificado a partir da tag correspondente na <code>main</code> que marca a versão de produção.
</p>
<p style="text-align:justify">
    A essência é que o trabalho dos membros da equipe na <code>develop</code> pode continuar, enquanto outra pessoa está preparando uma correção rápida de produção.
</p>

<br>

- ## **COMMITS**
<p style="text-align:justify">
    Padrão de mensagem de commits.
</p>

### Tipos
- Created: ao criar novas funções, features, componentes, etc ...
- Updated: ao atualizar funçoes, features, componentes, etc ...
- Refactored: ao refatorar funções, features, componentes, etc ...
- Fixed: ao corrigir um bug.
- Doc: ao documentar (docstrings, entre outros).

<br>

### Mensagem
```
{Tipo} [{escopo}]: {mensagem}
```
<p style="text-align:justify">
    Os commits devem estar em inglês, com as mensagens utilizando os verbos no passado.
</p>

<br>




<br>
<br>
<hr>
<br>
<br>




# **REFERÊNCIAS**
- https://www.alura.com.br/artigos/git-flow-o-que-e-como-quando-utilizar
- https://nvie.com/posts/a-successful-git-branching-model/
- https://medium.com/linkapi-solutions/conventional-commits-pattern-3778d1a1e657

# **DÚVIDAS?**
- Luan Bruno Domingues de Oliveira