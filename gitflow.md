# O Fluxo de Trabalho Gitflow: Organizando o Desenvolvimento

Este documento explica o Gitflow, um modelo de organização de branches no Git que ajuda equipes a manterem o código organizado, evitar conflitos e facilitar a manutenção do projeto.

---

### O Que é Gitflow?

Gitflow não é uma ferramenta, mas sim uma **estratégia** de como usar branches no Git. Ele define um fluxo de trabalho rigoroso, com papéis específicos para diferentes tipos de branches, o que é ideal para projetos com um ciclo de vida de lançamentos (releases) definido.

### As Branches Principais

O Gitflow utiliza duas branches "eternas" que servem como a espinha dorsal do projeto:

1.  **`main` (ou `master`)**
    - **Propósito:** Representa o código que está em **produção**. Tudo que está na `main` deve ser estável e funcional.
    - **Regra:** Ninguém faz commits diretamente na `main`. Ela só recebe merges de branches de `release` ou `hotfix`.
    - Cada commit na `main` é, essencialmente, uma nova versão do produto e deve ser "tagueada" (ex: `v1.0.1`).

2.  **`develop`**
    - **Propósito:** É a branch de **integração**. Ela contém o código com as funcionalidades mais recentes que serão incluídas na próxima release.
    - **Regra:** É a branch principal para o dia a dia do desenvolvimento. Todas as novas funcionalidades (feature branches) são mescladas nela.

### Branches de Suporte (Temporárias)

O trabalho real acontece em branches de suporte, que têm um ciclo de vida limitado:

#### 1. `feature/*` (Ex: `feature/login-system`)

- **Como começa:** Criada a partir da `develop`.
- **Propósito:** Desenvolver uma **nova funcionalidade** específica (uma *task*).
- **Fluxo:**
  1.  Para iniciar uma nova tarefa, você cria uma branch: `git switch -c feature/nome-da-task develop`.
  2.  Você trabalha, faz commits e desenvolve a funcionalidade de forma isolada.
  3.  Quando a funcionalidade está pronta, a branch `feature/*` é mesclada de volta na `develop`.
- **Benefício:** Isola o trabalho em andamento. Se uma feature quebrar, ela não afeta a `develop` nem o trabalho de outros desenvolvedores.

#### 2. `release/*` (Ex: `release/v1.2.0`)

- **Como começa:** Criada a partir da `develop` quando ela atinge um ponto estável para uma nova versão.
- **Propósito:** Preparar uma nova **release de produção**. Nesta branch, apenas correções de bugs de última hora e ajustes de documentação são permitidos.
- **Fluxo:**
  1.  Quando a `develop` está pronta para o lançamento, cria-se a branch `release/*`.
  2.  A equipe de QA (Quality Assurance) pode testar essa branch.
  3.  Após a aprovação, a `release/*` é mesclada **tanto na `main`** (para lançar em produção) **quanto na `develop`** (para garantir que as correções de última hora voltem para o fluxo de desenvolvimento).

#### 3. `hotfix/*` (Ex: `hotfix/fix-critical-bug`)

- **Como começa:** Criada a partir da `main`.
- **Propósito:** Corrigir um **bug crítico** que foi encontrado em produção e precisa de uma solução imediata.
- **Fluxo:**
  1.  Um bug é encontrado na `main`. Cria-se uma branch `hotfix/*` a partir da `main`.
  2.  O bug é corrigido e testado.
  3.  A branch `hotfix/*` é mesclada **tanto na `main`** (para corrigir a produção) **quanto na `develop`** (para que a correção não se perca no próximo ciclo).

---

### Pull Requests (PRs): A Chave da Colaboração

Um Pull Request (ou Merge Request) é o mecanismo para solicitar que sua branch (ex: `feature/login-system`) seja mesclada em outra (ex: `develop`).

**Como funciona no Gitflow:**

1.  Você termina sua `feature` e a envia para o repositório remoto (`git push`).
2.  Na plataforma (GitHub, GitLab, etc.), você abre um Pull Request da sua `feature/*` para a `develop`.
3.  **Code Review:** Outros desenvolvedores revisam seu código, sugerem melhorias e discutem a implementação.
4.  **Testes Automatizados:** O sistema de CI/CD pode rodar testes automaticamente para garantir que sua alteração não quebrou nada.
5.  Após a aprovação, a branch é mesclada na `develop`.

### Vantagens do Gitflow

1.  **Desenvolvimento Paralelo:** Vários desenvolvedores podem trabalhar em features diferentes ao mesmo tempo, sem interferir uns nos outros.
2.  **Menos Erros de Merge:** Como cada um trabalha na sua própria branch, os temidos "conflitos de merge" na `develop` são muito menos frequentes.
3.  **Facilidade de Rollback:** Se uma funcionalidade introduzida na `develop` causa problemas, é muito mais fácil reverter o merge do PR daquela feature específica sem afetar as outras.
4.  **Histórico Limpo e Organizado:** A `main` sempre contém um histórico linear de versões estáveis, facilitando a auditoria e a identificação de quando cada mudança entrou em produção.
5.  **Estabilidade:** O código em desenvolvimento (instável) fica separado do código de produção (estável), garantindo que a `main` esteja sempre pronta para ser implantada.
