---
layout: post
title:  "Perca o medo do terminal linux (parte 1)"
image: ''
date:   2020-05-15 19:01:30
tags:
- terminal
description: 'Como dar os primeiros passos para a produtividade no terminal'
categories:
- Terminal
---

<p class="music-read"><a href="https://www.youtube.com/watch?v=FGBhQbmPwH8&list=PL4C0F846412CF647F" target="_blank">Music for reading (YouTube)</a></p>

<img src="https://media.giphy.com/media/14ut8PhnIwzros/giphy.gif">

Olá Viajante, seja bem vindo. Se você caiu por aqui eu imagino que esteja querendo aprender sobre terminal linux, isso é ótimo, parabéns! Esse é um breve texto que eu escrevi (com a ajuda da minha mulher, bj amor) com o intuito de ser uma base para você que tem, assim como eu tinha, medo ou qualquer sentimento primitivo assim que abre a tela preta de um sistema linux. Meu objetivo não é ensinar tudo que o terminal pode oferecer, nem fazer um overview avançado do assunto, mas simplesmente te deixar mais confortável toda vez que precisar utilizá-la.

Abaixo, eu farei uma breve introdução a assuntos que eu acho relevantes antes de você começar de fato a hackear pelo terminal. Caso você julgue desnecessário, pule para a parte “comando básicos”. Fique a vontade e divirta-se.


## Linux

Se você está entrando na área de tecnologia, em algum momento você terá contato com distribuições baseadas em GNU/Linux. Nascidas da junção das ferramentas do Projeto [GNU](http://www.gnu.org/) e do Kernel Linux, normalmente referênciadas apenas como Linux. Esses são Sistemas Operacionais completos, como os famosos Microsoft Windows e Apple MacOS, feitos com base de [código aberto e livre](http://www.gnu.org/philosophy/free-sw.html). 

Esses sistemas são conhecidos por serem estáveis, seguros e totalmente configuráveis. Por isso distribuições baseadas em Kernel Linux são utilizadas em grande parte dos servidores ao redor do mundo para servir os sistemas que utilizamos diariamente. Toda a administração do sistema operacional é normalmente feita através de instruções passadas por uma interface de texto, seja um arquivo salvo com as instruções, outro software de administração ou em tempo real passadas por um humano.

<img src="https://upload.wikimedia.org/wikipedia/commons/c/c9/Gnulinux.svg">


## Shell

Para facilitar a interação humana com o sistema operacional, foram criadas as ferramentas nomeadas de shell (casca), que permitem a instrução de tarefas através de comandos pré-escritos e traduzidos para a interpretação da máquina. Hoje em dia normalmente essa interface é composta de telas, janelas e menus renderizados em um monitor de alta resolução, mas claro que nem sempre foi assim. 

Inicialmente os comandos precisavam ser passados via uma interface de linha de comando, que recebem comandos e parâmetros e realizam um script de operações com os valores passados, normalmente dando um retorno ao usuário. Esses programas são conhecidos como comand-line interfaces (CLI). Outros programas, classificados como text-based user interface (TUI), utilizavam apenas o formato texto para gerar menu visuais para o usuário interagir.

Os sistemas baseados em [Unix](https://pt.wikipedia.org/wiki/Unix) criaram diversas ferramentas nesses modelos, deixando o shell baseado em texto muito poderoso. Tudo isso foi importado e aprimorado nas distribuições GNU/Linux, fazendo com o que esse recurso se tornasse uma das estrelas do sistema.

<img src="https://images.fineartamerica.com/images-medium-large/sea-shell-by-the-sea-shore-paulette-thomas.jpg">

Hoje em dia o principal shell utilizado em distribuições Linux é o “bash” acrônimo para [Bourne Again SHell](https://www.gnu.org/software/bash/), ele será o foco dos comando e recursos apresentados aqui por sua popularidade, no entanto, são compatíveis caso você use outros shells como fish, zsh, entre outros.

Assim que você abre o bash, ele irá te mostrar o seu prompt inicial, algo parecido com isso: “nome@maquina:~$”. Esse texto é chamado de PS1, e é composto por algumas informações. São elas:

Nome do usuário logado concatenado com o nome do computador separados pelo símbolo “@”, conhecido por nós como “arroba”. Não faz muito sentido pensando nesse símbolo com esse nome, no entanto uma curiosidade legal é que em inglês esse símbolo é conhecido como “at”, que quer dizer “em”. Dessa forma, o que o prompt quer dizer é que o usuário X está logado “em” Y. Da mesma forma como são referenciados os endereços de email. 

Depois, temos mais um separador, nesse caso os dois pontos, e o diretório atual que estamos logados, Como a home do usuário é uma pasta bastante utilizada, nesse caso temos a variável “\~” que tem o valor dela alterado para a home do usuário corrente pelo sistema assim que logamos. Por isso vemos o “~” depois dos dois pontos.

Por fim, o caractere “$” significa que o usuário logado não tem privilégios de administrador do sistema, caso tivesse, esse caractere seria substituído por “#”.


## Terminal Emulator

Normalmente não queremos apenas um shell baseado em texto para usar no dia-a-dia, então estaremos quase sempre em um sistema com ambiente interface gráfica, também chamados de Desktop Environments. 

Por isso, para acessar o shell precisamos de um programa auxiliar capaz de criar essa ponte entre interface gráfica e o shell (de texto) do sistema. Nessa categoria temos os Terminal Emulators, comumente chamados apenas de Terminal.


## Comandos Básicos

Todo Desktop Environments disponibiliza no mínimo um Terminal Emulator que normalmente é encontrado facilmente por uma pesquisa por “Terminal” no sistema e tendem a ter atalhos de teclado para abri-los rapidamente, como CTRL + ALT + T no Ubuntu.

É possível inclusive, rodar emuladores de terminal linux no Windows, utilizando programas como CygWin, MobaXterm ou Cmder. 

Para computadores MacOS esse recurso é nativo, já que o sistema operacional da Apple é de uma família de sistemas baseados em Unix, o BSD.

Ao abrir o Terminal, normalmente ele te localizará no diretório chamado “home”, a pasta principal do usuário logado e trará um prompt, onde é possível começar a digitar seus primeiros comandos. 

A estrutura de um comando normalmente é: nome do comando, flags e argumentos. Separados por espaço. 

Como exemplo, usaremos a estrutura abaixo:

```bash
ls -l /home
```

Onde “ls” é o comando que estamos chamando, “-l” é a flag que altera ou adiciona funcionamento a este comando e “/home” é o argumento para o processamento do ls, nesse caso, o diretório home, que fica na raíz do sistema, referenciada como barra "/".

Após essa “breve” introdução, vamos começar a utilizar nossos primeiros comandos.

### Olá Mundo

Dizem que ao iniciar com qualquer nova tecnologia, por questão de sorte, a primeira coisa a se fazer é escrever "hello world" na tela do computador. Mesmo sendo uma bobagem, é uma ótima oportunidade para falar do nosso primeiro comando, o "echo".

O comando "echo" retornará o que for passado para ele como input, ou seja, ele literalmente funciona como o eco acustico.

Então, para começarmos com o pé direito, vamos escrever nosso "hello world".

```bash
echo hello world
```

Devidamente benzidos, vamos em frente.


### ls, mkdir, cd e pwd

Esses são alguns comandos básicos para navegação no terminal. Vou tentar deixar algumas dicas para buscá-los na memória até que vire memória muscular por repetição.

“ls” serve para visualizar os arquivos dentro de um diretório. Lembrar de “LiSt” (Listar).

Mostra o conteúdo de um diretório
```bash
ls
```

Mostra o conteúdo de um diretório inclusive arquivos ocultos
```bash
ls -a
```

As flags podem ser acumuladas para resultados diferentes:

Mesmo resultado anterior porém em “formato longo” (com mais informações):
```bash
ls -la
```

Mesmo resultado anterior porém com tamanhos dos arquivos em formato mais legível
```bash
ls -lah
```

O comando “mkdir” cria um novo diretório (pasta no windows). Lembrar de “MaKe DIRectory” (Criar Diretório).

“cd” muda o diretório em uso. Lembrar de “Change Directory” (Mudar Diretório).

“pwd” serve para mostrar o diretório atual em uso. Lembrar de “Print Working Directory” (algo como “Imprimir Diretório em Uso”).

Criar e acessar um novo diretório
```bash
mkdir meu_diretorio
cd meu_diretorio
```

“cd” sem argumentos volta para a pasta home
```bash
cd
pwd
```

Algo legal sobre diretórios em linux é que todos eles têm por padrão 2 “atalhos” inclusos em sua criação. O primeiro deles faz referência ao próprio diretório, e é representado por um ponto “.”, já o segundo faz referência ao diretório anterior ao que estamos (um nível acima) e é representado por dois pontos “..”. 

Com isso em mente, temos formas bem mais simples quando precisamos referenciar esses diretórios em nossos comandos. Será comum você ver comandos que utilizam as formas “comando .” ou “comando ..”.

Ver que esses arquivos de fato existem em nosso novo diretório
```bash
cd meu_diretorio
ls -la
```

Ir para o diretório acima
```bash
cd ..
```

Ir diretamente para uma pasta
```bash
cd ~/meu_diretorio
```

Um ótimo recurso dos shells atuais é o auto-complete utilizado normalmente com a tecla TAB. Isso quer dizer que ao escrever apenas uma parte do texto e pressionar a tecla TAB uma vez, se o conteúdo escrito representar apenas um arquivo, diretório ou comando em seu shell, ele completará automaticamente o restante da palavra para você. 

Caso haja ambiguidade, não será completado nada, porém, você poderá apertar TAB uma segunda vez para listar quais as opções filtradas pelo início que foi digitado. É legal se acostumar rapidamente a utilizar esse recurso, pois ele irá aumentar significativamente a velocidade com que você chegará ao seu objetivo dentro do terminal.


## Arquivos e Editores de Texto

Arquivos de texto são de extrema importância sejam eles código, configurações, dados ou qualquer tipo de informação. É importante saber criá-los, extrair rapidamente informações e manuseá-los conforme nossa necessidade. Nesta sessão vamos ver as principais ferramentas para trabalhar com arquivos de texto dentro do terminal.

### touch

O comando “touch” atualiza a data de edição de um arquivo, porém, caso esse arquivo não exista, ele será criado. Isso nos ajuda a criar novos arquivos em branco quando necessário. No entanto, a grande maioria dos comandos de edição de texto também criam o arquivo caso não seja encontrado nada com o nome especificado, fazendo do touch um comando pouco utilizado.

Exemplo:

Criar novo arquvio no diretório atual
```bash
touch todo.txt
```

Cria-lo em outro diretório também é possível passando o caminho completo
```bash
touch ~/todo.txt
```

### nano

Nano é um editor de texto básico, vem por padrão instalado em basicamente todos os shells atuais. É focado em simplicidade e já vem com uma tela de ajuda junto em sua interface com uma série de comandos. É um ótimo lugar para começar. 

Para abrir um arquivo, basta chamar o comando “nano” e passar o caminho do arquivo a ser aberto:

Abrir um arquivo para edição
```bash
nano todo.txt
```

A maior parte dos atalhos no nano aparecerão com o caractere “^” na frente, que representa a tecla “Ctrl”, por exemplo os comandos Salvar “^O” (Ctrl+O) e Sair “^X” (Ctrl+X).

### vim

“vim” é o editor de texto mais utilizado no mundo linux, ele tem um universo de possibilidades com seus comandos, atalhos, macros, modos, buffers, e outras coisas que merecem um conteúdo a parte. Mas para começarmos vamos apenas criar um arquivo e editar seu conteúdo.

Antes de partir para o editor, temos que entender que o vim tem alguns modos, os principais são: O modo “Normal” que é onde grande parte da “mágica” ocorre e é o modo inicial quando abrimos um arquivo, o modo “Visual” onde podemos fazer seleção do texto mostrado na tela e o modo de “Inserção” que serve para editar o conteúdo do arquivo.

Para entrar em modo de Inserção aperte "i" no modo normal, e para voltar ao modo normal de qualquer modo aperte "Esc".


Abrir um arquivo com o vim (se não existir, será criado ao salvar)
```bash
vim todo.txt
```

Para editar o arquivo, primeiro acesse o modo de inserção com a tecla "i". Faça as alterações que desejar e volte ao modo normal com a tecla "Esc". No modo Normal vários comandos podem ser chamados, os principais são:

Sair do editor
```bash
:q
```

Caso você tenha editado o arquivo como fizemos acima, o vim irá reclamar se você tentar sair sem salvar. Caso você tenha certeza que não queer o conteúdo alterado, você precisará deixar explicido que quer sair sem salvar.

Forçar saída (sem salvar):
```bash
:q!
```

Volte ao arquivo e faça novamente a alteração. Dessa vez, faremos nossa edição ser salva. Aqui temos várias opções:

Apenas salvar
```bash
:w
```

Salvar e sair
```bash
:wq
```

Outra forma de salvar e sair
```bash
:x
```


### cat, head, tail, wc

O comando ”cat” imprime o conteúdo de um ou mais arquivos de texto na tela. Lembrar de “conCATenate” (pois mais de um arquivo pode ser passado como parâmetro, separando-os por espaço) ou “CATch”. Existe também o “tac” que faz a mesma coisa, porém lê o arquivo invertendo a ordem as linhas (cat… tac… pegou a piada ? ha!).

Mostrar conteúdo
```bash
cat todo.txt
```

Cuidado com arquivos grandes, eles serão inteiramente carregados em memória e bloqueiam seu terminal com o output do comando enquanto não terminar de escrever o conteúdo na tela, o que pode demorar bastante tempo. Ctrl+C é seu amigo nessas horas, esse atalho manda um comando de “terminar” para o programa atualmente rodando.

Em arquivos grandes não queremos imprimir o tamanho total do arquivo em todos os momentos, às vezes apenas dar uma “espiada” em parte do conteúdo, para isso temos os comandos “head” e “tail”.

“head” imprime o início ou a “cabeça” de um arquivo, da mesma forma “tail” imprime o final ou a “cauda” desses.

<img src="https://pbs.twimg.com/media/EJrbGinXUAEBPgG?format=jpg&name=medium">

head e tail por padrão mostram 10 linhas
```bash
head todo.txt
tail todo.txt
```

A flag “-n” muda o valor padrão de linhas visualizadas
```bash
tail -n1 todo.txt
```


“wc” é usado para contar coisas dentro de um arquivo ou uma saída de texto. Podem ser linhas, caracteres, palavras, entre outros. Lembrar de “Word Count”.

Contar as linhas do arquivo
```bash
wc -l todo.txt
```


### cp, mv e rm

“cp” faz a cópia do conteúdo de um arquivo para outro, sem segredo. Lembrar de “CoPy”.

Criar a cópia de um arquivo (primeiro argumento origem, segundo o destino)
```bash
cp todo.txt todo2.txt
ls
```


“mv” pode ser usado tanto para mover arquivos de uma pasta para outra, quanto para renomeá-los, movendo para a mesma pasta com outro nome. Lembrar de “MoVe”.

Renomear um arquivo
```bash
mv todo2.txt todo_backup.txt
```

Mover um arquivo para outra pasta
```bash
mv todo_backup.txt ~
```

“rm” serve para remover arquivos e diretórios. Tome todo o cuidado ao usar um rm pois com privilégios de administrador o estrago pode ser grande. Lembrar de “ReMove”.

Excluir um arquivo
```bash
rm todo.txt
```

Para diretórios, é necessário que o mesmo esteja vazio ou usando a flag “-r” (recursivo)
```bash
cd ~
rm -r meu_diretorio
```

### history

Um comando muito útil durante o aprendizado com terminal é o “history” (Histórico), que mostra os últimos comandos usados pelo usuário logado. Uma dica interessante é que você pode chamar novamente um comando do seu histórico sabendo em qual linha ele está, utilizando o caractere “!” e o número da linha. Isso pode ser de grande ajuda quando você tiver feito comandos mais complexos e precisar deles novamente.

Visualizar histórico
```bash
history
```

Exemplo de Saída:
1    mkdir meu_diretorio
2    cd meu_diretorio
3    pwd

Chamar o comando pwd novamente
```bash
!3
```


### Ajuda

Isso é tudo pessoal! Porém, não deixe de se aprimorar nas artes místicas do terminal. Nativamente o shell tem opções para ajudar a usuário a entender como um comando é utilizado:

Texto de ajuda do comando
```bash
ls --help
```

Manual do comando (“q” para sair da página)
```bash
man ls
```

Como última alternativa, nosso amigo de todas as horas: [Google](www.google.com.br)

Caso ache algum comando que não entenda, uma ferramenta legal para dividi-lo em partes e entender o que está acontecendo é o explainshell.com. Basicamente essa ferramenta lê todo o comando e mostra o que cada parte está fazendo.

### Fontes para Estudar
[Guia Foca](https://guiafoca.org/cgs/guia/iniciante/index.html)

[Advanced Bash-Scripting Guide](https://www.tldp.org/LDP/abs/html/basic.html)

[2-Minute Linux Tips by Sandra Henry-Stocker](https://www.youtube.com/playlist?list=PL7D2RMSmRO9J8OTpjFECi8DJiTQdd4hua)
