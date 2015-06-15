# R-pacotes-rautu

Criação de pacotes para o R: uma rápida introdução



## Motivação

Como já dizia [John M. Chambers][] quando criou a linguagem S
(predecessora do R), o objetivo da linguagen é

> "... to turn ideas into software, quickly and faithfully."

Se você já explorou um pouco mais do que o potencial básico do R,
certamente já criou sua própria função (ou várias funções) para fazer
alguma tarefa específica. A ideia é que se você tiver que realizar uma
tarefa muitas vezes, então deve criar uma função para fazer isso.

A criação de um pacote do R pode ter duas motivações principais:

* Agrupar e manter uma série de funções criadas por você e que são
basicamente de uso próprio ou rotineiro.
* Compartilhar funções de novos métodos e/ou implementações que você
  tenha criado e queira disponibilizar para outras pessoas usarem.

Não raramente, um pacote de uso pessoal acaba se tornando útil para
outras pessoas e o autor disponibiliza para uso geral. O importante é
então saber como transformar suas funções em um pacote. E mais
importante ainda é saber como fazer isso se preocupando apenas com as
funções, ao invés de se preocupar com todo o processo de criação do
pacote.

A criação de um pacote no R pode ser feita de duas formas:

* Tradicional: usando os comandos padrões do R para criação de pacotes,
  como `R CMD build` para criar e `R CMD check` para conferir o pacote,
  ambos executados através de um terminal e não de uma sessão do R.
* Moderna: usando o pacote `devtools`, que possui funções para criar e
  conferir o pacote (inclusive para testar e documentar as funções) de
  dentro de uma sessão do R.

A maneira tradicional de criar pacotes no R é um pouco mais trabalhosa,
pois cada vez que você quiser checar se seu pacote está funcionando, é
necessário ir para um terminal e rodar os comandos por fora do R. Além
disso, se você quiser testar seu pacote após a instalação, será
necessário instalar de fato o pacote e carregá-lo com `library()`. O
grande problema é que durante o desenvolvimento de um pacote, esses
passos geralmente são repetidos muitas vezes, o que torna todo o
processo muito demorado.

O pacote `devtools` facilita todo esse processo, pois você pode
construir, checar, documentar (e conferir a documentação) de dentro da
própria sessão do R que você está desenvolvendo o pacote. Além disso
esse pacote também permite que, com uma função, você simule a instalação
do seu pacote na mesma sessão R, evitando ter que instalar e desinstalar
para testes todas as vezes.

Um outro aspecto fundamental de todo pacote é a sua documentação. Da
maneira tradicional, é necessário criar os arquivos `.Rd` e escrever
usando uma linguagem muito parecida com o LaTeX. Toda vez que você
quiser editar a documentação é necessário abrir esses arquivos e
modificá-los nesse formato. Para facilitar ainda mais a vida dos
programadores, existe o pacote `roxygen2`, que possibilita escrever a
documentação dentro da própria função `.R`, integrando código e
documentação em um único arquivo, e facilitando a edição das páginas de
ajuda. 

O pacote `roxygen2` pode ser utilizado também na abordagem tradicional
de criação de pacotes, eliminando uma etapa trabalhosa que é a de criar
os arquivos de documentação. No entanto, podemos usar todo o potencial
do `devtools` e do `roxygen2` juntos, e nos preocuparmos apenas com o
design das funções e não com todo o processo de criação do pacote em
si.

## Estrutura de um pacote

Basicamente um pacote do R é uma convenção para organizar e padronizar a
distribuição de funções extras do R. Todo pacote é composto
*obrigatoriamente* por apenas dois diretórios e dois arquivos de meta
dados:

* `R/`: um diretório contendo as funções em arquivos `*.R` (ex.:
  `foo.R`).
* `man/`: um diretório contendo a documentação (páginas de ajuda) de
  cada função do diretório acima. Os arquivos de documentação do R
  terminam com a extensão `.Rd` (ex.: `foo.Rd`).
* `DESCRIPTION`: um arquivo texto contendo as informações sobre o seu
  pacote: autor, licença, outros pacotes dependentes, ...
* `NAMESPACE`: um arquivo texto que informa quais funções do seu pacote
  serão exportadas, ou seja, aquelas que estarão disponíveis para o
  usuário, e quais funções são importadas de outros pacotes dos quais o
  seu depende.

Outros componentes que não são obrigatórios, mas podem estar presentes
no pacote são (nenhum deles serão abordados aqui):

* `tests/`: um diretório contendo scripts com testes unitários, rodados
  durante a criação do pacote, para testar se existe algum resultado não
  esperado sendo retornado por alguma de suas funções.
* `vignettes/`: um diretório que contém uma ou mais *vignettes*, que
  traduzidas literalmente são como "vinhetas", pequenos (ou mesmo
  grandes) textos que explicam com mais detalhes como os usuários podem
  usar as funções de seu pacote.
* `data/`: um diretório contendo arquivos de dados (normalmente em
  formato binário e comprimido do R, `.rda`), que podem ser usados como
  exemplos para aplicação das funções do pacote.

Abaixo serão especificados os detalhes para a criação de cada um dos
componentes obrigatórios descritos acima.

## `DESCRIPTION`: Caracterização do pacote

Caso você queira começar um pacote do início, as opções são: 1) criar
todos os componentes (diretórios e arquivos) manualmente e ir
alimentando com conteúdo, ou 2) usar a função `create()` do pacote
`devtools` para criar um "esqueleto" inicial com os arquivos e
diretórios fundamentais de um pacote. Portanto:


```r
library(devtools)
create("meupacote", rstudio = FALSE)
```

```
Creating package meupacote in .
No DESCRIPTION found. Creating with values:
```

```
Package: meupacote
Title: What the Package Does (one line, title case)
Version: 0.0.0.9000
Authors@R: person("First", "Last", email = "first.last@example.com", role = c("aut", "cre"))
Description: What the package does (one paragraph)
Depends: R (>= 3.2.0)
License: What license is it under?
LazyData: true
```

Como pode ser observado na saída acima, esse comando cria um diretório
chamado `meupacote`, e já cria um arquivo `DESCRIPTION` com o conteúdo
acima.

## `R/`: Funções

Se você já possui um diretório `R/` contendo apenas funções do R
(arquivos `.R`), então a maior parte do problema já está
resolvido. Basta seguir o restante do texto para ver como criar os
outros componentes do pacote.

## `man`: Documentação



## `NAMESPACE`: Organização



[John M. Chambers]: http://statweb.stanford.edu/~jmc4/
