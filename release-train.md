# Estratégia de Release Train

## O que é o Release Train e seus benefícios

O Release Train é uma abordagem de entrega contínua que estabelece um ciclo previsível e regular de releases. 
Ao invés de lançar features individuais quando prontas, estabelecemos um cronograma fixo de "trens" que partem em datas 
predeterminadas, independente de quais features estarão a bordo.

## Benefícios:

- Previsibilidade: Todas as partes interessadas conhecem antecipadamente as datas de release, permitindo melhor planejamento.
- Redução de complexidade: A integração contínua de código diminui conflitos de merge e facilita a identificação precoce de problemas.
- Colaboração: Times diferentes sincronizam seu trabalho de acordo com o calendário de releases.
- Gerenciamento de risco: Features incompletas não atrasam todo o trem, apenas "perdem o trem" e aguardam o próximo.

## Fluxo detalhado das releases

### Estrutura de Branches

Nosso fluxo de trabalho utiliza as seguintes branches:

- main: Branch principal que contém código estável e pronto para produção.
- release/x.y.z: Branch de release criada no início de cada sprint.
- feature/nome-da-feature: Branches onde novas features são desenvolvidas.
- hotfix/x.y.z: Branch para correções urgentes que precisam ir para produção imediatamente.

### Ciclo de Vida de uma Release

**1) Início da Sprint: Criação da Release Branch**

No primeiro dia da sprint, uma nova branch release/x.y é criada a partir da main.

O versionamento segue o padrão semântico (X = major, Y = minor).

A release branch é imediatamente protegida, exigindo PRs revisados para qualquer alteração.

Esta branch contém todas as features que serão incluídas na próxima release.

**2) Durante a Sprint: Desenvolvimento de Features**

Desenvolvedores criam branches feature/nome-da-feature a partir da branch main.

Desenvolvimento e commits ocorrem nas branches de feature.

Todos os commits devem seguir o padrão Conventional Commits.

Testes de integração são executados nas branches de feature.

Quando a feature está pronta para teste, um PR é aberto para a branch de release atual.

**3) Integração na Release Branch**

PRs só podem ser abertos para a release branch quando a feature estiver em fase de testes.

O código deve passar em todos os testes automatizados.

É necessária pelo menos uma aprovação de revisão de código.

Uma vez aprovado, o código é mesclado na release branch.

**4) Preparação para Release**

Quando a data da release se aproxima, todas as features integradas na release branch são testadas em conjunto.

QA realiza testes finais na release branch.

Se bugs forem encontrados, são corrigidos diretamente na release branch.

Documentação é atualizada, incluindo notas de release.

**5) Dia da Release**

A release branch é mesclada na main via Pull Request.

Uma tag é criada na main com o número da versão.

Os artefatos de release são gerados a partir da tag.

A release é implantada em produção.

**6) Pós-Release**

As notas de release são publicadas.

O status da release é atualizado no Calendário de Releases.

Features que não conseguiram entrar nessa release são repriorizadas para a próxima.

### Processo de Hotfix

Se um bug crítico for identificado em produção, uma branch hotfix/x.y.z (com o patch na versão) é criada a partir da main.

A correção é implementada na branch de hotfix.

Após testes e aprovação, a branch de hotfix é mesclada tanto na main quanto na release branch atual.

Uma nova tag é criada na main (incrementando o número de patch).

Uma nova build é gerada e implantada em produção.

### Critérios Importantes

- Nunca fazer merge diretamente na main: Todo código deve passar pelo processo de PR e revisão.
- Criação de releases no início da sprint: Garante visibilidade e planejamento desde o começo.
- Testes obrigatórios antes de PRs: Features devem estar em fase de testes para integração.
- Features incompletas não atrasam o trem: Se uma feature não estiver pronta, ela aguarda o próximo trem.
- Versionamento semântico: Seguimos estritamente o padrão X.Y.Z para versões.
- Proteção de branches: Tanto main quanto release são protegidas e exigem aprovação de PRs.
- Conventional Commits: Todos os commits devem seguir o padrão Conventional Commits para facilitar a geração automática de changelogs e versionamento.

### Padrão Conventional Commits
Todos os commits devem seguir o padrão Conventional Commits:

- feat: Nova funcionalidade
- fix: Correção de bug
- docs: Alterações na documentação
- style: Formatação, ponto e vírgula ausentes, etc; sem alteração de código
- refactor: Refatoração de código
- test: Adição de testes, refatoração de testes; sem alteração de código de produção
- chore: Atualizações de tarefas de build, configurações, etc; sem alteração de código de produção
- perf: Alterações que melhoram o desempenho

**Exemplos:**

- feat: adiciona nova funcionalidade de login
- fix: corrige cálculo de datas no relatório
- docs: atualiza README com instruções de instalação
- refactor(autenticação): simplifica lógica de validação de tokens

Isso facilita a geração automática de changelogs e o versionamento semântico do projeto.

Este documento será revisado e atualizado trimestralmente para refletir melhorias no processo.
