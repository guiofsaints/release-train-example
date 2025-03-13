# Guia de Contribuição

Este documento descreve o processo de contribuição para o projeto, incluindo o fluxo de trabalho com branches, critérios de aceitação de código e o processo de release train que seguimos.

## Visão Geral do Fluxo de Trabalho

Nosso projeto segue um modelo de Release Train, com releases regulares e previsíveis. Utilizamos o seguinte fluxo de branches:

- `main` - Branch principal que contém apenas código estável e pronto para produção
- `release/x.y.z` - Branch de release criada no início de cada sprint
- `feature/nome-da-feature` - Branches de feature onde o desenvolvimento ocorre
- `hotfix/x.y.z` - Branches para correções urgentes em produção

## Como Contribuir

### 1. Criando uma Branch de Feature

Todas as novas features devem ser desenvolvidas em branches dedicadas, sempre criadas a partir da branch `main`:

```bash
# Certifique-se de estar na branch main atualizada
git checkout main
git pull

# Crie sua branch de feature
git checkout -b feature/nome-da-feature
```

Nomeie sua branch seguindo o padrão `feature/nome-descritivo-da-feature`.

### 2. Desenvolvimento e Commits

Durante o desenvolvimento:

- Faça commits frequentes com mensagens claras e descritivas, seguindo o padrão **Conventional Commits**.
- Mantenha sua branch atualizada com a main regularmente:

```bash
git checkout feature/nome-da-feature
git pull origin main
```

- Escreva testes unitários e de integração para seu código.
- Certifique-se de que seu código segue os padrões de estilo do projeto.

#### Conventional Commits

Todos os commits **DEVEM** seguir o padrão Conventional Commits:

```
<tipo>[escopo opcional]: <descrição>

[corpo opcional]

[rodapé(s) opcional(is)]
```

**Tipos de commit**:
- **feat**: Nova funcionalidade
- **fix**: Correção de bug
- **docs**: Alterações na documentação
- **style**: Formatação, ponto e vírgula ausentes, etc; sem alteração de código
- **refactor**: Refatoração de código
- **test**: Adição de testes, refatoração de testes; sem alteração de código de produção
- **chore**: Atualizações de tarefas de build, configurações, etc; sem alteração de código de produção
- **perf**: Alterações que melhoram o desempenho
- **ci**: Alterações em configurações de CI/CD

**Exemplos**:
```
feat(auth): adiciona suporte para login com Google
fix: corrige cálculo de datas no relatório mensal
docs: atualiza README com comandos de instalação
refactor(payments): simplifica lógica de processamento
test(api): adiciona testes para novos endpoints
```

Este padrão é **obrigatório** e será verificado por hooks de pre-commit. Commits que não seguirem o padrão serão rejeitados.

### 3. Preparando para Integração

Antes de abrir um PR para a branch de release:

- Execute todos os testes localmente para garantir que estão passando.
- Revise seu próprio código para identificar possíveis melhorias.
- Certifique-se de que sua feature está completa ou em um estado que permita testes.

### 4. Abrindo um Pull Request

Quando sua feature estiver pronta para testes:

1. Abra um Pull Request para a branch de release atual (`release/x.y.z`).
2. Preencha o template do PR com todas as informações necessárias.
3. Atribua revisores adequados.
4. Vincule as issues relacionadas ao PR.

**Importante:** PRs só podem ser abertos para a branch de release quando a feature estiver em fase de testes.

### 5. Revisão e Integração

- Responda prontamente aos comentários de revisão.
- Faça as alterações solicitadas pelos revisores.
- Após aprovação, seu código será mesclado na branch de release.

## Critérios para Aceitação de Features

Para que um Pull Request seja aceito, ele deve atender aos seguintes critérios:

1. **Qualidade de Código**:
   - Passar em todos os testes automatizados (unitários, integração, e2e)
   - Seguir os padrões de codificação do projeto
   - Não introduzir dívida técnica sem documentação

2. **Revisão**:
   - Ter pelo menos uma aprovação de um revisor designado
   - Todas as solicitações de alteração devem ser resolvidas

3. **Documentação**:
   - Código bem documentado com comentários onde necessário
   - README ou documentação atualizada, se aplicável

4. **Testabilidade**:
   - Testes automatizados escritos para a nova funcionalidade
   - Cobertura de testes adequada

5. **Integridade**:
   - Não quebrar funcionalidades existentes
   - Não causar regressão em outros módulos

6. **Conventional Commits**:
   - Todos os commits devem seguir o padrão Conventional Commits
   - O título do PR também deve seguir o padrão Conventional Commits

## Processo de Release Train

### Criação de Release Branch

No início de cada sprint, uma nova branch de release é criada (se ainda não existir):

```bash
# Certifique-se de estar na branch main atualizada
git checkout main
git pull

# Crie a branch de release com versionamento semântico
git checkout -b release/x.y.z
git push -u origin release/x.y.z
```

Onde:
- **x**: Versão major (mudanças incompatíveis com versões anteriores)
- **y**: Versão minor (novas funcionalidades compatíveis com versões anteriores)
- **z**: Versão patch (correção de bugs compatíveis com versões anteriores)

### Processo para Hotfixes

Quando um bug crítico é identificado em produção:

1. Crie uma branch de hotfix a partir da `main`:

```bash
git checkout main
git pull
git checkout -b hotfix/x.y.z
```

2. Implemente a correção e faça commit (seguindo o padrão Conventional Commits com tipo `fix:`).
3. Abra um PR para a branch `main`.
4. Após aprovação e merge, crie também um PR para a branch de release atual.
5. Após os merges, crie uma tag com a nova versão:

```bash
git checkout main
git pull
git tag -a vx.y.z -m "Hotfix x.y.z: breve descrição"
git push origin vx.y.z
```

## Documentação Adicional

Para mais informações sobre nosso processo de desenvolvimento, consulte:

- [Estratégia de Release Train](https://confluence.empresa.com/projeto/estrategia-release-train)
- [Calendário de Releases](https://confluence.empresa.com/projeto/calendario-releases)
- [Guia de Estilo de Código](https://confluence.empresa.com/projeto/guia-estilo-codigo)
- [Guia de Conventional Commits](https://www.conventionalcommits.org/)

## Dúvidas e Suporte

Se você tiver dúvidas sobre o processo de contribuição, entre em contato com o líder técnico do projeto ou abra uma issue com a tag "dúvida".

---

Agradecemos por contribuir para o nosso projeto!
