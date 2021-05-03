---
layout: post
title:  "Perca o medo do terminal linux (parte 2)"
image: 'https://media.giphy.com/media/cW1PvoyY7YCAw/giphy.gif'
date:   2020-07-20 20:01:30
tags:
- terminal
description: 'Continuando nossa aventura pelo terminal'
categories:
- Terminal
---

<p class="music-read"><a href="https://youtu.be/O4fbxCJ_obQ" target="_blank">Music for reading (YouTube)</a></p>

Olá Viajante, seja bem vindo. Legal ter você de volta a essa aventura. Se você pegou o bonde andando e está querendo aprender mais sobre o terminal linux, pode ler a [primeira parte](https://undersfx.github.io/terminal-parte-1/) onde eu dou um contexto geral e falo o básico sobre o assunto.

Nessa parte eu gostaria de mostrar alguns comandos adicionais e principalmente falar de operadores de controle e de redirecionamento. Esses conceitos farão sua habilidade no  terminal atingir o próximo nível. Então, bora upar junto ?!

<img src="https://media.giphy.com/media/jy1SW46Ovt3CLIsbo6/giphy.gif">

Como vamos falar de comando de filtragem, transformação e visualização de texto, será necessário termos um arquivo de tamanho razoável para visualizarmos os resultados. Nos meus exemplos abaixo, eu usarei o arquivo chamado “alice.txt”, que terá o conteúdo do livro “Alice's Adventures in Wonderland” de Lewis Carroll, que é disponível gratuitamente na internet através do Projeto Gutenberg. Se quiser utilizar o mesmo arquivo, ele está disponível [aqui](https://www.gutenberg.org/files/28885/28885.txt). Caso não conheça esse projeto, fica a dica, é um acervo de conteúdo com mais de 60 mil livros “open source”. :)

Como somos ninjas do terminal, ou pelo menos estamos no caminho para isso, vamos baixar o livro e salvar num arquivo local usando o terminal. Conseguimos isso com o comando abaixo:

```bash
curl https://www.gutenberg.org/files/28885/28885.txt > alice.txt
```

O comando curl é uma ferramenta de transferência de dados para vários protocolos, entre eles HTTP e HTTPS. Então conseguimos acessar o conteúdo do arquivo hospedado publicamente na internet apenas passando sua URL. O restante do comando serve para escrever a saída do comando “curl” em um arquivo chamado “alice.txt”. Mas calma, isso fará mais sentido quando falarmos sobre operadores ao decorrer do texto.

Caso o terminal retorne algo como `curl: command not found`, provavelmente você não tem o curl instalado. Nesse caso você pode abrir o link para o documento no navegador e copiar o conteúdo para criar o arquivo "normalmente".

Para saber se deu certo você pode olhar o conteúdo do arquivo com um dos comandos que mostrei na primeira parte. Eu usarei o “wc” para saber quantas linhas tem meu arquivo “alice.txt”

```bash
wc -l alice.txt
```

Se a saída for um número diferentes de zero (no nosso caso 4052) o comando trouxe todo o conteúdo de deveria de maneira correta.

Agora vamos começar a brincar com esses dados.


## grep

O comando “grep” funciona como um filtro. Ele recebe um padrão como parâmetro (que pode ser uma string, uma expressão regular ou até outro arquivo) e retorna todas as linhas que coincidirem com esse padrão dentro do conteúdo que foi passado a ele, como um arquivo ou o output de outro comando. Isso é extremamente útil quando trabalhamos com blocos grandes de texto, pois o retorno é rápido e eficaz. Isso ajuda a filtrarmos informações importantes de um log gigantesco, por exemplo.

Filtrar padrão “alice” dentro do arquivos “alice.txt”

```bash
grep alice alice.txt
```

Nossa primeira pesquisa não retorna nenhuma linha, o que é estranho. No entanto se pesquisarmos por “Alice” (com maiúscula no início) temos um resultado diferente:

```bash
grep Alice alice.txt
```

Isso acontece pois o grep é “case sensitive”, ou seja, letras maiúsculas e minúsculas são consideradas diferentes. Para alterar esse comportamento podemos utilizar a flag “-i”:

```bash
grep -i alice alice.txt
```

Outras flags bem úteis são:

Retorno inverso (todas as linhas que _não_ tem o padrão) pode ser obtido passado o padrão com a flag “-v”:

```bash
grep -iv alice alice.txt
```

Visualizar o número de incidências daquele padrão no arquivo com “-c”:

```bash
grep -ic alice alice.txt
```

Visualizar o número das linhas em que o padrão aparece com “-n”:

```bash
grep -in alice alice.txt
```

Limitar o número de itens que serão retornados com “-m”:

```bash
grep -im 10 alice alice.txt
```

Para usar expressões regulares como padrão, é preciso passar “-E”: 

```bash
grep -iE "(alice|rabbit)" alice.txt
```

No exemplo acima, usei um padrão básico que procura por “alice” ou “rabbit”. 

Expressão Regular, chamada também de RegEx, é uma linguagem formal para identificar cadeias de caracteres, isso quer dizer que você escreve uma regra que vai bater apenas com a parte que você quer de um texto. Regex são um canivete suíço para qualquer trabalho com texto, facilitando a procura e filtragem. 

Várias ferramentas aceitam pesquisa por regex, como Sublime, Notepad++, Vim, entre outras. É uma ótima ferramenta para incluir em seu arsenal. Se tiver interesse no assunto, uma ótima fonte de dados é o site do grande [Aurélio Jargas](https://aurelio.net/regex/).


## awk

“awk” não é só um comando, é uma linguagem de escaneamento e processamento de dados dentro do terminal. Aqui vou mostrar algumas funções bem úteis para transformar o conteúdo que precisamos. Mas é uma outra recomendação de estudo caso você tenha esse tipo de trabalho em seu fluxo.

Podemos ter um resultado semelhante ao grep utilizando apenas um padrão regex para pesquisa:

```bash
awk '/Alice/' alice.txt
```

awk por padrão divide cada linha do texto do input por espaço e quebra em variáveis nomeadas $1, $2, $3… a linha toda é salva em $0. 

Dessa forma, se quisermos a primeira palavra de cada linha do nosso livro.

```bash
awk '{print $1}' alice.txt
```

A variável $NF é um atalho para total de campos reconhecidos. Se usado como índice consequentemente retornará a última variável armazenada. Nesse caso, pegamos 

```bash
awk '{print $NF}' alice.txt
```

Para usar um separador customizado (diferente do espaço) precisamos passar uma string para a flag “-F”. Essa opção é ótima quando está se trabalhando com logs de máquina bem formatados e com o mesmo número de campos. Você passa o separador que seu log utiliza e tem cada parâmetro salvo em uma variável para uso.

Por exemplo, vamos usar vírgula como separador:

```bash
awk -F',' '{print $1}' alice.txt
```

Como disse, awk é uma linguagem, então print é só uma das dezenas de funções que podemos utilizar. Outro comando útil que podemos usar é “length”, para filtrar o tamanho da string ou da linha. 

Por exemplo, para pegarmos apenas as linhas com mais de 42 caracteres:

```bash
awk 'length ($0)>42' alice.txt
```

Eu já acho tanto grep quanto awk ferramentas incríveis, porém, ambos brilham ainda mais quando combinados com outras ferramentas do terminal como o “pipe” que falarei mais a frente na sessão de operadores (calma, está chegando).


## more e less

“more” imprime o arquivo desejado até que a tela fique cheia e abre um modo de navegação para o restante do conteúdo. Os comandos básicos para controlar a navegação são: <enter> desce uma linha, <espaço> desce uma página e <q> sai do modo navegação.

Paginar nosso arquivo alice.txt

```bash
more alice.txt
```

“less” tem uma função fundamentalmente igual ao do “more”, no entanto ele faz muito mais, permitindo ir e voltar entre a visualização, pesquisar por padrão regex usando “/” entre outros comandos (vale a pena ler a documentação, use “man less”). Os comandos more e less são mais usados após redirecionamentos (tá chegando, eu juro), mas também podem ser chamados normalmente para um arquivo.

Para abrir a visualização less para o arquivo

```bash
less alice.txt
```


# Operadores de Redirecionamento e Controle

Esse é um dos assuntos mais legais quando o assunto é terminal, porém….. antes de falar dele é importante sabermos alguns outros conceitos para facilitar o entendimento. Os primeiros que vou abordar são input e output de um comando.


## input e output

Em resumo, input é todo o conteúdo passado para o comando que você chama no terminal, como um arquivo ou uma string e output tudo que o resultado do comando quer retornar para o usuário, que normalmente é algum texto na tela.

Como exemplo, vamos analisar o seguinte comando: grep exemplo.com log.txt

grep é o “comando” que chama o binário que está em “/bin/grep” e passa como argumento para esse programa a string “exemplo.com” e o caminho do arquivo log.txt que será lido e seu conteúdo processado. Posteriormente será colocado na tela todas as linhas que baterem com o padrão “exemplo.com” dentro do arquivo. Esse é o output desse comando.

(Se quiser saber mais como funciona a “chamada” dos comandos, dê uma lida sobre a variável de ambiente PATH. Como é um assunto também mais complexo, não abordarei dessa vez.)


## stdin, stdout e stderr

A chamada do comando e seus argumentos normalmente vão vir do usuário digitando no próprio terminal através de uma interface como o teclado. Essa entrada de dados é chamada de “stdin” (de “Standard Input”).

Tudo que esse comando retornar no caso de sucesso será escrito no “stdout” (de “Standard Output”) e nos casos de falhas, será usado o “stderr” (de “Standard Error”).

Os dois últimos por padrão serão impressos no terminal. Mas como são apenas file descriptors, esse comportamento pode ser alterado ou redirecionado como veremos abaixo.

Aliás, por falar em file descriptors, é importante pelo menos conhecê-los para não boiar no assunto de redirecionamento.


# File descriptors

File descriptors são uma abstração para acesso a um arquivo ou recursos de input/output no sistema como pipes e sockets, e são representados por um número inteiro não negativo.

O fluxo de dados lidos do stdin e escritos no stdout e stderr são administrados pelo sistema através dos file descriptors reservados 0, 1 e 2 respectivamente. Isso quer dizer que quando existe um input de um comando através do stdin, ele é escrito no file descriptor 0 para ser “traduzido” e após executar seus procedimentos ele escreverá o resultado nos files descriptors 1 ou 2 de acordo com o resultado.

Aqui começa a brincadeira. Os operadores de controle e redirecionamento mudam como essas entradas e saídas funcionam para dar maiores poderes aos nossos comandos. Vamos lá!

<img src="https://media.giphy.com/media/FqdGGgugkC4Xm/giphy.gif">


# Operadores de Redirecionamento

## “<”, “>” e “>>”

Caracteres que representam uma instrução ao bash são chamados de tokens. Os três que vamos conhecer inicialmente são bastante utilizados no dia-a-dia. “<” serve para redirecionar um recurso para o input de um comando:

Exemplo:

```bash
head < alice.txt
```

Nesse caso, o sistema abre o arquivo “alice.txt” e passa como input para o comando “head” que [já aprendemos o que faz](https://undersfx.github.io/terminal-parte-1/).

“>” e “>>” ambos servem para redirecionar o conteúdo de saída de um comando (output) para um arquivo.

A diferença é que “>” é considerado uma instrução de “Write” enquanto “>>” é uma instrução de “Append”. Isso quer dizer que “>” fará com que um arquivo seja criado caso não exista e sobrescrito (seu conteúdo será apagado) caso já exista. Já o “>>” criará o arquivo da mesma forma caso não exista, porém se o mesmo já existir irá concatenar o conteúdo ao final dos dados atuais do arquivo.

Não existe melhor ou pior, tudo depende do que você quer fazer no momento.

Exemplos:

Para criar novo arquivo apenas com as linhas que contêm “Alice” dentro do arquivo alice.txt, usamos:

```bash
head alice.txt > cabeca.txt
```

Temos o mesmo funcionamento utilizando “>>” (caso “rabo.txt” não exista, claro):

```bash
tail alice.txt > rabo.txt
```

Concatenar dados de dois arquivos é possível fazendo o “append” de um ao outro:

```bash
cat rabo.txt >> cabeca.txt
```

## Redirecionando file descriptors diferentes

O token “>” por padrão redireciona apenas o conteúdo do “stdout” do comando. Podemos testar esse comportamento com o comando abaixo:

```bash
ls alice.txt rabbit.txt
```

O resultado será algo parecido com:

```bash
ls: cannot access 'rabbit.txt': No such file or directory
alice.txt
```

Como não temos um arquivo chamado “rabbit.txt” nossa saída terá um retorno de erro enviado ao “stderr” e uma informação de sucesso enviada ao “stdout” (o nome do arquivo encontrado com o padrão “alice.txt”)

Como já sabemos podemos redirecionar o retorno do comando para um arquivo com “>”, então vamos criar um arquivo chamado “resultado.txt”:

```bash
ls alice.txt rabbit.txt > resultado.txt
```
Nesse momento, confirmamos visualmente duas coisas. Que a mensagem de erro continua sendo mostrada na tela (stderr) e que o output do comando é salvo no arquivo resultado (stdout).

```bash
cat resultado.txt
```

Para alterarmos esse comportamento, deixamos explícito o file descriptor a ser utilizado na para escrita com o número do mesmo antes do token “>”:

```bash
ls alice.txt rabbit.txt 1> resultado.txt 2> erro.txt
```

Como o comportamento padrão do token “>” é pegar o output, não é necessário utilizar “1>”, funcionando também dessa forma:

```bash
ls alice.txt rabbit.txt > resultado.txt 2> erro.txt
```

Dessa vez não veremos nada na tela pois direcionamos todas as saídas para outros file descriptors (nossos arquivos criados no momento da execução) que não são o stdout.


## “>&”

Caso quisermos que o mesmo arquivo receba tanto stdout quando stderr, podemos utilizar o token “>&”:

```bash
ls alice.txt rabbit.txt >& resultado_e_erro.txt
```

Esse token é uma forma resumida de “2>&1”, que informa ao bash que você irá redirecionar o stderr (file descriptor 2) para o stdout (file descriptor 1) tratando tudo apenas como output e escrevendo no arquivo “resultado.txt”.


## Perigos de construção com “>”

Em algum momento, você pode chegar a uma construção de linha de comando onde você quer “atualizar” o conteúdo de um arquivo e você o usa tanto em input quanto output. Algo como o comando abaixo:

```bash
comando arquivo.txt > arquivo.txt
```

É importante saber que essa construção não irá funcionar, e pior que isso, irá apagar o conteúdo de “arquivo.txt”. 

Isso acontece porque a abertura dos arquivos é feita _antes_ da execução do comando. Isso quer dizer que o arquivo será primeiro aberto para escrita e como ele já existe será “truncado” para tamanho zero, perdendo seu conteúdo. Após isso o comando será executado utilizando o conteúdo do arquivo, que neste momento não existe mais, resultando em um resultado não esperado e normalmente em branco também que será por fim escrito e salvo no arquivo aberto.

Para não cair nessa cilada ~bino~ utilize outro arquivo temporário e faça a remoção do mesmo após a execução ou substitua renomeando o arquivo temporário:

```bash
comando arquivo.txt > tmp.txt
mv tmp.txt arquivo.txt
```

Para dar um spoiler do nosso próximo assunto, com a ajuda de um operador lógico de controle “E” (AND), podemos fazer isso na mesma linha:
```bash
comando arquivo.txt > tmp.txt && mv tmp.txt arquivo.txt
```

# Operadores de Controle

## “|” (Pipe)

O pipe é certamente o operador de controle mais utilizado no terminal linux. Seu efeito serve para “ligar” o output de um comando como input de outro. Simples.

“Pipe” quer dizer algo como “tubo” ou “tubulação”, imagine que estamos criando uma tubulação entre a saída do comando anterior com a entrada do próximo comando. Dessa forma, você pode fazer um filtro de uma informação em um arquivo com grep, por exemplo, e na mesma linha de comando tratar essa informação com awk, filtrar novamente com outro grep, contar com wc, fazendo tudo que seja necessário para tirar a informação que deseja.

Exemplo:

Quantas incidências de ‘foo’ eu tenho no arquivo ‘bar.txt’

```bash
grep foo bar.txt | wc -l
```

Dessa forma, o resultado da expressão “grep foo bar.txt” que seria colocado no stdout é direcionado para o input do comando “wc -l” que espera com um fluxo de texto vindo do stdin e faz a contagem de suas linhas.

## “&&” e “\|\|”

Os caracteres “&&” e “\|\|” formam os operadores lógicos E (AND) e OU (OR) respectivamente. Normalmente em shell script são utilizados para fazer declarações com comparações. No entanto, podem ser utilizados no terminal para encadear comandos quando queremos controle sobre o que vai ser executado em caso de falha ou sucesso.

De acordo com o POSIX, o comando retornará um código de saída (ou “exit code”) ao sistema sempre que terminar sua execução. Esse código é um número de 0 a 255, onde 0 é o indicador de sucesso e os demais números são notificações de diferentes erros.

Pela característica de serem [operadores de curto-circuito](https://pt.wikipedia.org/wiki/Avalia%C3%A7%C3%A3o_de_curto-circuito), a avaliação será feita da esquerda para a direita e os comandos adicionais serão executados apenas se o primeiro argumento não for suficiente para determinar o valor da expressão.

Por exemplo, numa condição E (AND) a segunda condição só será verificada caso a primeira seja verdadeira, pois caso contrário, apenas com o primeiro valor já sabemos que o resultado da condição será falso. 

Da mesma forma, numa condição OU (OR) a segunda condição só será verificada caso a primeira seja falsa, pois caso contrário, já sabemos que o resultado da operação será verdadeiro.

Usando isso ao nosso favor para criar comandos compostos, quando quisermos que o segundo comando execute apenas na certeza que o primeiro funcionou, utilizamos “&&”:

```bash
wc -l alice.txt && echo 'Deu certo!'
```

Da mesma forma, quando quisermos que o segundo comando rode apenas em caso de falha do primeiro, utilizamos “\|\|”:

```bash
wc -l rabbit.txt || echo 'Deu ruim =('
```


## “&”

Por usar o mesmo caractere encontrado no operador E (AND), podemos confundir com um funcionamento parecido. No entanto, esse operador serve para rodar um comando em “background”. Isso quer dizer que o mesmo não irá bloquear a entrada de novos comandos no terminal até sua finalização.

Um bom exemplo é o comando “sleep” que aguarda uma quantidade de tempo e retorna um status de sucesso após esse período. Se fizermos uma composição com sleep e outro comando podemos ver como o terminal é bloqueado enquanto o sleep está executando:

```bash
sleep 10 && wc -l alice.txt
```

Se utilizarmos o operador ao final do comando, é retornado o código do trabalho criado para esse processo (chamado de PID) e posteriormente o retorno é colocado em nossa tela.

```bash
sleep 10 && wc -l alice.txt &
```

Esse é um ótimo operador quando precisamos ficar monitorando algo no sistema ou precisamos que um script rode em segundo plano enquanto usamos o terminal.


# Finalmentes

Bom pessoal, isso é tudo por hoje. 

Acredito que com todos esses conceitos e comandos, vocês poderão criar suas próprias composições que respondem questões tecnicamente complexas mais rapidamente.

Se quiserem saber mais sobre redirecionamentos e operadores da linha de comando recomendo fortemente uma lida [nesse resumão](https://unix.stackexchange.com/questions/159513/what-are-the-shells-control-and-redirection-operators/159514#159514) feito pelo usuário “terdon” no stackoverflow.

Se quiser mergulhar ainda mais fundo, recomendo esse tabelão com todos os [caracteres especiais](https://www.tldp.org/LDP/abs/html/special-chars.html) e o que eles fazem.

### Agradecimentos
Revisão por [Emily Faccin](https://github.com/emilyfaccin)
