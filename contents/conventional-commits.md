## Conventional Commits Pattern

Os commits são pontos na linha do tempo de um projeto. Quando documentados propriamente nos mostram quem alterou, quando, em qual contexto e qual tipo de alteração foi feita. Diante disso, vamos conhecer o [**Conventional Commits Pattern**](https://www.conventionalcommits.org/en/v1.0.0/).

O Conventional Commits é uma convenção simples de mensagens de _commit_, que segue um conjunto de regras e que ajuda os projetos a terem um histórico de _commit_ explícito e bem estruturado.

Há vários benefícios (além dos já citados anteriormente) em utilizar esse tipo de convenção, como por exemplo, poder automatizar a criação de CHANGELOGs, facilitar a entrada de novos Devs no projeto, assim como poder gerar relatórios e conseguir entender onde está se concentrando as horas do projeto (em refatoração de código, criação de features, mudança de estilos, ambiente de desenvolvimento, entre outros).

### Como utilizar

As regras são muito simples, como demonstrado abaixo temos um tipo de commit (_type_), o escopo/contexto do commit (_scope_) e o assunto/mensagem do commit (_subject_), mas adiante irei detalhar cada um.

```bash
  !type(?scope): !subject
  <?body>
  <?footer>
```

Dessa maneira, `!` indica os atributos obrigatórios e `?` indica os atributos não obrigatórios.

### Subject: Imperativo ao invés de pretérito (modo passado)

Escrevendo **subjects** utilizando o imperativo nós estamos dizendo à nossa equipe o **que fará o _commit_ se aplicado**.

No [artigo](https://chris.beams.io/posts/git-commit/#imperative) de Chris Beams ele diz um pouco mais sobre a escolha do imperativo e traz uma grande notação, ao qual, todo subject deve se enquadrar:

> “If applied, this commit will `<message>`”

Em português: “Se aplicado, esse commit irá `<mensagem>`”. Se pensarmos no exemplo representado acima, o resultado seria:

> “**If applied, this commit will change the markup**”, o que faz muito mais sentido do que: “_If applied, this commit will changed the markup_”

### Type: Quais são os tipos de commit

O _type_ é responsável por nos dizer qual o tipo de alteração ou iteração está sendo feita, das regras da convenção, temos os seguintes tipos:

- `test`: indica qualquer tipo de criação ou alteração de códigos de teste.
- - **Exemplo**: Criação de testes unitários.
- `feat`: indica o desenvolvimento de uma nova feature ao projeto.
- - **Exemplo**: Acréscimo de um serviço, funcionalidade, endpoint, etc.
- `refactor`: usado quando houver uma refatoração de código que não tenha qualquer tipo de impacto na lógica/regras de negócio do sistema.
- - **Exemplo**: Mudanças de código após um code review.
- `style`: empregado quando há mudanças de formatação e estilo do código que **não alteram** o sistema de nenhuma forma.
- - **Exemplo**: Mudar o _style-guide_, mudar de convenção _lint_, arrumar indentações, remover espaços em brancos, remover comentários, etc.
- `fix`: utilizado quando há correção de erros que estão gerando bugs no sistema.
- - **Exemplo**: Aplicar tratativa para uma função que não está tendo o comportamento esperado e retornando erro.
- `chore`: indica mudanças no projeto que não afetem o sistema ou arquivos de testes. São mudanças de desenvolvimento.
- - **Exemplo**: Mudar regras do _eslint_, adicionar _prettier_, adicionar mais extensões de arquivos ao ._gitignore_
- `docs`: usado quando há mudanças na documentação do projeto.
- - **Exemplo**: adicionar informações na documentação da API, mudar o README, etc.
- `build`: utilizada para indicar mudanças que afetam o processo de **build** do projeto ou dependências externas.
- - **Exemplo**: webpack, adicionar/remover dependências do npm, etc.
- `perf`: indica uma alteração que melhorou a performance do sistema.
- - **Exemplo**: alterar _forEach_ por _while_, melhorar a query ao banco, etc.
- `ci`: utilizada para mudanças nos arquivos de configuração de **CI**.
- - **Exemplo**: Circle, Travis, BrowserStack, etc.
- `revert`: indica a reverão de um commit anterior.

```bash
git commit -m "test: add test for create product automation"
git commit -m "feat: implement tracking product service"
git commit -m "refactor: change return log pattern"
git commit -m "style: change function param for objects"
git commit -m "fix: remove getPayment() wrong attribute"
git commit -m "chore: add no-undef rule in eslintrc.json"
git commit -m "docs: add technologies list in readme"
git commit -m "style: remove all blank spaces"
git commit -m "perf: change looping for parallel execution"
git commit -m "build: remove moment.js dependency"
git commit -m "build: add date-fns npm dependency"
git commit -m "revert: back to a215868 commit"
```

Assim, conseguimos de forma simples e direta ver qual tipo de mudança está ocorrendo, melhorando bastante a visibilidade e alinhamento com a equipe.

Observações:

- Só pode ser utilizado um type por _commit_;
- O _type_ é **obrigatório**;
- Caso esteja indeciso sobre qual _type_ usar, provavelmente trata-se de uma grande mudança e é possível separar esse _commit_ em dois ou mais _commits_;
- A diferença entre `build` e `chore` pode ser um tanto quanto sutil e pode gerar confusão, por isso devemos ficar atentos quanto ao tipo correto. No caso do Node.js por exemplo, podemos pensar que quando há uma adição/alteração de certa dependência de desenvolvimento presente em `devDependencies`, utilizamos o `chore`. Já para alterações/adições de dependências comuns aos projeto, e que haja impacto direto e real sobre o sistema, utilizamos o `build`.

### Scope: contextualizando o commit

Nesse ponto — e seguindo as convenções passadas — conseguimos entender o tipo de alteração que foi realizada no commit (_commit type_) e entender com clareza o que o commit irá trazer se aplicado (_commit subject_).

Entretanto, até aonde essa mudança pode afetar ?

Em repositórios enormes, como _monorepos_, ou projetos com várias _features_ e mudanças paralelas, não fica bastante claro até onde a mudança que irá chegar pode alterar. Para isso, podemos utilizar o escopo(_scope_) do _commit_.

```bash
git commit -m 'feat(UserService): add /getAppointments endpoint'
```

Mesmo o scope **não sendo obrigatório**, ele pode ser utilizado para contextualizar o _commit_ e trazer menos responsabilidade para a _subject_, uma vez que dispondo do tipo de _commit_ e o contexto que foi aplicado, a mensagem deve ser o mais breve e concisa possível. **Lembrando que o _scope_ deve ser inserido no commit entre parênteses.**

Além disso, no caso do _scope_ é possível adicionarmos múltiplos valores, como por exemplo: Caso houvesse uma refatoração de código em um repositório com versões mobile, web e desktop. A qual afeta o contexto mobile e web, poderíamos escrever o _commit_ da seguinte maneira:

```bash
git commit -m 'refactor(web/mobile): change createUser() logs'
```

> Os escopos devem ser separados com `/` , `\` ou `,`.

_" é importante dizer que o *Conventional Commit* e suas especificações devem ser seguidas e respeitadas. Entretanto, não é um modelo ao qual se adequa a todo tipo de projeto e empresa."_
