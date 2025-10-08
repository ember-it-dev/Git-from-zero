
# Guia de Comandos Essenciais do Git

Este guia explica de forma objetiva os comandos mais comuns do Git que você mencionou.

---

### `git init`

**O que faz:** Inicia um novo repositório Git em um diretório.

**Como usar:**
Navegue até a pasta do seu projeto e execute:
```bash
git init
```
Isso cria um subdiretório oculto chamado `.git`, que contém todos os arquivos necessários para o repositório.

---

### `git clone`

**O que faz:** Cria uma cópia local de um repositório remoto existente.

**Como usar:**
```bash
git clone <url_do_repositorio>
```
Exemplo:
```bash
git clone https://github.com/usuario/meu-projeto.git
```
Isso baixa o projeto para um novo diretório com o mesmo nome do repositório.

---

### `git add`

**O que faz:** Adiciona alterações do seu diretório de trabalho para a "Staging Area" (área de preparação). É o passo antes de "salvar" as alterações em um commit.

**Como usar:**
- Para adicionar um arquivo específico:
  ```bash
  git add nome_do_arquivo.txt
  ```
- Para adicionar todos os arquivos modificados e novos no diretório atual:
  ```bash
  git add .
  ```

---

### `git commit`

**O que faz:** Salva as alterações que estão na Staging Area em um "snapshot" permanente no histórico do repositório.

**Como usar:**
- O uso do flag `-m` permite que você adicione uma mensagem de commit diretamente na linha de comando.
  ```bash
  git commit -m "Sua mensagem descritiva aqui"
  ```
  **Boas práticas:** A mensagem deve ser clara e resumir o que foi alterado.

---

### `git config`

**O que faz:** Configura variáveis específicas do Git, como informações do usuário (nome, email) ou configurações do repositório.

**Como usar:**
- Para configurar seu nome de usuário globalmente:
  ```bash
  git config --global user.name "Seu Nome"
  ```
- Para configurar seu email globalmente:
  ```bash
  git config --global user.email "seu.email@exemplo.com"
  ```
A flag `--global` aplica a configuração a todos os seus repositórios. Se removida, a configuração se aplica apenas ao repositório atual.

---

### `git branch`

**O que faz:** Lista, cria ou deleta branches (ramos). Uma branch é uma linha de desenvolvimento independente.

**Como usar:**
- Para listar todas as branches locais:
  ```bash
  git branch
  ```
- Para criar uma nova branch:
  ```bash
  git branch <nome_da_nova_branch>
  ```
- Para deletar uma branch (use `-d` para um delete seguro ou `-D` para forçar):
  ```bash
  git branch -d <nome_da_branch>
  ```

---

### `git checkout`

**O que faz:** É um comando versátil usado principalmente para **trocar de branch** ou **restaurar arquivos** do diretório de trabalho.

**Como usar:**
- Para trocar para uma branch existente:
  ```bash
  git checkout <nome_da_branch>
  ```
- **`checkout -b` (ou `-B`):** Cria uma nova branch e já troca para ela. É um atalho para `git branch <nome>` seguido de `git checkout <nome>`.
  ```bash
  git checkout -b <nome_da_nova_branch>
  ```
  *Dica: `git checkout -B` força a criação ou recriação da branch se ela já existir.*

- **`checkout .`:** Descarta **todas** as alterações locais nos arquivos que ainda não foram adicionados à Staging Area, restaurando-os para a versão do último commit. **Use com cuidado, pois as alterações são perdidas.**
  ```bash
  git checkout .
  ```
- Para descartar alterações em um arquivo específico:
  ```bash
  git checkout -- <nome_do_arquivo>
  ```

---

### `git switch`

**O que faz:** É um comando mais moderno e seguro, introduzido para separar as funcionalidades do `git checkout`. Sua principal função é **trocar de branch**.

**Como usar:**
- Para trocar para uma branch existente:
  ```bash
  git switch <nome_da_branch>
  ```
- Para criar uma nova branch e trocar para ela (equivalente a `checkout -b`):
  ```bash
  git switch -c <nome_da_nova_branch>
  ```

**Por que usar `switch` em vez de `checkout`?**
O `git switch` tem um propósito único (trocar de branch), o que o torna menos propenso a erros do que o `git checkout`, que tem múltiplas funções. É a prática recomendada atualmente.
