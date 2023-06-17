## Padronizando mensagens de Commits - Conventional Commits

O [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) é uma convenção simples de mensagens de commit, que segue um conjunto de regras e que ajuda os projetos a terem um histórico de commit explícito e bem estruturado.

Existem ferramentas que nos ajudam a utilizar essa convenção validando as mensagens de commits que é o caso do [commitlint](https://commitlint.js.org/#/) e o mais utilizado para configurar ações junto aos **git hooks** é o [husky](https://typicode.github.io/husky/).

### Husky

Husky é um pacote npm que “torna os Git hooks fáceis”.

Quando você inicializa o Git (a ferramenta de controle de versão com a qual você provavelmente está familiarizado) em um projeto, ele vem automaticamente com um recurso chamado hooks.

Se você for até a raiz de um projeto inicializado com Git e digitar:

```bash
ls .git/hooks
```

Você verá uma lista de ganchos de exemplo, como `pre-push`, `pre-rebase`, `pre-commit` e assim por diante. Esta é uma maneira de escrevermos algum código de plugin para executar alguma lógica antes de realizar a ação do Git.

Com o Husky, podemos garantir que, para um novo desenvolvedor trabalhando em nossa base de código :

- Hooks são criados localmente.
- Hooks são executados quando o comando Git é chamado.
- Aplicar uma regra que define como alguém pode contribuir para o projeto.

### Configurando o Husky

Para realizar a configuração no modo automático, `husky-init` é um único comando para inicializar rapidamente um projeto com husky.

```bash
npx husky-init && npm install
```

Ele vai:

1. Adicionar script `prepare` ao `package.json`.
2. Cria um `hook pre-commit ` de amostra que você possa editar (por padrão, **npm test** será executado quando você confirmar).
3. Configurar o caminho dos hooks do Git

> Guias de [configurações](https://typicode.github.io/husky/guide.html) do husky.

### Adicionando o commmitlint ao projeto

O Commitlint verifica se a mensagem do commit, nesse caso verificar se segue o padrão do **Conventional Commit**.

1. Instalação do `commit lint` e `config-conventional`.

```bash
npm install -g @commitlint/cli @commitlint/config-conventional
```

2. Criação do arquivo de configuração `commitlint.config.js` e adicionando o padrão a ser utilizado.

```bash
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

> Referencia de configurações do [commitlint.config.js](https://commitlint.js.org/#/reference-configuration)

3. Para adicionar o hook `commit-msg` com o commitlint, use `husky add`.

```bash
npx husky add .husky/commit-msg  'npx --no -- commitlint --edit ${1}'
```

Vamos a um exemplo de erro para mensagem fora do padrão.

```bash
git commit -am 'bad message'
⧗   input: bad message
✖   subject may not be empty [subject-empty]
✖   type may not be empty [type-empty]

✖   found 2 problems, 0 warnings
ⓘ   Get help: https://github.com/conventional-changelog/commitlint/#what-is-commitlint

husky - commit-msg hook exited with code 1 (error)
```

> Conheça o Conventional Commits Pattern

Existem outras ferramentas para auxiliar a manter padronizações tais como [commitizen](https://commitizen-tools.github.io/commitizen/), [lint-staged](https://github.com/okonet/lint-staged) entre outras.
