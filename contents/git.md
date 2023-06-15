## Principais comandos do Git

Git é um sistema de controle de versão para rastrear alterações em arquivos de computador e coordenar o trabalho nesses arquivos entre várias pessoas.

Aqui vamos aprender de forma direta as principais funcionalidades e comandos para o dia a dia.

### Instalação e Configuração inicial

Instalação usando como exemplo sistemas Linux ubuntu/debian.

```bash
# Para obter a versão estável mais recente
$ apt-get install git
```

Configurar **user** e **email** é importante porque cada commit usa esta informação, e ela é 'carimbada' de forma imutável nos commits que você criar.

```bash
# configura o usuário pode ser global ou local
$ git config --global user.name "Jorge Nascimento"

# configuração do email pode ser global ou local
$ git config --global user.email "nascimento.dev.io@gmail.com"

# listando configurações
$ git config --list

# cria apelidos a comandos do git
$ git config --global alias.s status -s
```

### Iniciando um repositório

Um novo sub diretório chamado **.git** é criado e contém todos os arquivos necessários de seu repositório.

```bash
# acesse o diretório do projeto
$ cd path/to/directory

# inicializa um novo repositório
$ git init
```

### Realizando clone de projetos remotos

O Git recebe uma cópia completa de praticamente todos os dados que o servidor possui. Cada versão de cada arquivo no histórico do projeto é obtida por padrão quando você executa `git clone`.

```bash
# realiza o download do projeto remoto em um diretório com nome do projeto
$ git clone <repo-url> or <ssh-url>
```

### Verificando os Status de Seus Arquivos

A principal ferramenta que você vai usar para determinar quais arquivos estão em qual estado é o comando `git status`.

```bash
# lista o status sem filtros
$ git status

# lista os arquivo de forma resumida ( com legendas )
$ git status -s or git status --short
```

### Adicionando arquivos para serem 'commitados'

A partir desse momentos seus arquivos estão sendo monitorados, e ja pode utilizar o comando `commit` e grava o `snapshot`.

```bash
# adicionando arquivos ao staged/index
$ git add <file> or $ git add .
```

## Visualizando Suas Alterações Dentro e Fora do Stage

Se o comando git status for vago demais para você — você quer saber exatamente o que você alterou, não apenas quais arquivos foram alterados — você pode usar o comando `git diff`.

```bash
# Para ver o que você alterou mas ainda não mandou para o stage.
$ git diff

# Compara as alterações que estão no seu stage com o seu último commit
$ git diff --staged
```

## Fazendo Commit das Suas Alterações

Agora que sua área de stage está preparada do jeito que você quer, você pode fazer `commit` das suas alterações.

```bash
# cria o commit e insere a mensagem diretamente na linha de comando
$ git commit -m <mensagem>

# adiciona as alterações e ja cria o commit
$ git commit -am <mensagem>
```

### Desfazendo as coisas

Para remover um arquivo do Git, você tem que removê-lo dos seus arquivos rastreados (mais precisamente, removê-lo da sua área de stage) e então fazer um commit.

```bash
# remove o arquivo
$ git rm <file>

# remove o arquivo mesmo que esteja em staged
$ git rm -f <file>
```

### commit --amend

Se você quiser refazer o ultimo commit porque nao possuía os arquivos que voce gostaria ou queira apenas mudar a mensagem, execute o commit novamente usando a opção `--amend`:

```bash
$ git commit --amend -m 'new message'
```

### reset

O `git reset` remove arquivo da stage area retornando-os para estado anterior, pode também retornar o estado para um determinado commit com opções de flags `--soft` `--mixed` e `--hard`.

```bash
$ git reset HEAD <file> or git reset <file>

$ git reset <flag> HEAD~1 or git reset <flag> <hash>
```

### checkout

Para reverter as modificações de um arquivo voltando a ser como era quando foi realizado o último commit, use o `git checkout`.

```bash
$ git checkout -- <file>
```

### revert

O `git revert` basicamente desfazer tudo aquilo que foi feito dentro de um determinado **commit** (ou dentro de um intervalo de commits), o git cria um novo commit que registra o que foi desfeito.

```bash
$ git revert <hash> or git revert HEAD~
```

## Vendo o histórico de Commits

O `git log` é o comando que lista cada **commit** com o seu **checksum SHA-1**, o **nome** e **email do autor**, **data de inserção**, e a **mensagem do commit**.

> O git log possui opções para formatação de saida desse comando.

````bash
# comando com saida padrão
$ git log

# comando com saida formatada
 git log --pretty=format:'%C(blue)%h %C(red)%d %C(cyan)%s - %C(yellow)%cn, %C(white)%cr' ```
````

## Trabalhando de Forma Remota

Para colaborar com qualquer projeto Git, você precisará saber como gerenciar seus repositórios remotos.

### remote

```bash
# lista os nomes abreviados de cada repositório remoto
$ git remote

# adicionar um novo repositório git remoto
$ git remote add <shortname> <url>

# mostra informações sobre um servidor remoto em particular
$ git remote show <shortname remote>

# renomeia o nome do repositório remoto
$ git remote rename origin repo-remote

# remove referencia de servidor remoto
$ git remote remove repo-remote
```

## Buscando e Empurrando dados dos seus Repositórios Remotos

Para obter dados de seus projetos remotos, você pode executar o comando `fetch`:

### fetch

```bash
$ git fetch <remote-name>
```

> É importante notar que o comando `git fetch` só baixa os dados para o seu repositório local - ele não é automaticamente mesclado.

### pull

O `git pull` comumente busca os dados do servidor de onde você originalmente clonou e automaticamente tenta mesclá-lo dentro do código que você está atualmente trabalhando.

### push

Este comando funciona apenas se você clonou de um servidor ao qual você tem acesso de escrita (write-access) e se ninguém mais utilizou o comando push nesse meio-tempo.

```bash
$ git push origin main
```

## Branches no Git

Um branch no Git é simplesmente um ponteiro móvel para um commits. O nome do branch padrão no Git é **main**. Conforme você começa a fazer commits, você recebe um branch **main** que aponta para o último commit que você fez. Cada vez que você faz um novo commit, ele avança automaticamente.

```bash
# lista a(s) branch(s)
$ git branch

# cria um branch com nome testing
$ git branch testing

# alterna para o branch testing
$ git checkout testing

# remove uma branch
$ git branch -d <branch name>
```

Apos realizar commit's em outra branch voce diverge do commit parent erm ambas as branchs, voce pode visualizar isso através do comando `git log` `--oneline --decorate --graph --all`.

## Mesclagem Básica

Para realizar a mesclagem das branchs utilizamos o comando `git merge`. O git merge atualiza a branch atual com as alterações da branch especificada e cria um novo commit resultante dessa união.

```bash
# na branch main, uni as alterações realizadas na testing
git merge testing
```

A união dessas alterações pode resultar em conflito, isso ocorre quando alterações sao realizadas no mesmo arquivo e na mesma linha entre as branch.

> Para resolver conflitos e necessário escolher qual mudança ira fica no arquivo final seguido de `git add` no arquivo.
