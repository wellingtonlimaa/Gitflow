# GitFlow

O GitFlow é um modelo de organização de branches no Git que simplifica o controle de projetos de software. Ele estabelece uma estrutura definida para o fluxo de trabalho, criando branches para fases distintas do ciclo de vida do software, como funcionalidades, lançamentos e correções.

## Branches

- **Master:** Representa a versão de produção do software.
- **Develop:** É onde o desenvolvimento ativo ocorre e todas as funcionalidades são integradas.
- **Feature:** Branches para desenvolver novas funcionalidades.
- **Release:** Branches para preparar versões para lançamento.
- **Hotfix:** Branches para corrigir bugs críticos em produção.
- **Bugfix:** Branches para corrigir bugs em release branches.

## Tags

Tags são rótulos vinculados a commits, indicando pontos cruciais na história do repositório. Geralmente, são usadas para marcar versões de software, como lançamentos estáveis.

## Fluxo Passo a Passo

** Lembre-se de já ter uma branch principal base, como a master, pois a branch develop irá utilizá-la como base. **

### 1. Criar ou Mudar para Branch develop

Caso você já tenha a Branch develop:

```bash
1. git checkout develop
2. #adicione alguns commits caso seja necessário utilizando git add e git commit -m "tipo(escopo): mensagem"
3. git push origin develop
```

Caso você não tenha a Branch develop:

```bash
1. git checkout -b develop
2. #adicione alguns commits caso seja necessário utilizando git add e git commit -m "tipo(escopo): mensagem"
3. git push origin develop
```

### 2. Criar e Mudar para uma Nova Branch de Feature (Funcionalidade):

```bash
1. git checkout -b feature/autenticar-usuario
2. git add autenticar-usuario.js
3. git commit -m "feat: Autenticar Usuário"
4. git push origin feature/autenticar-usuario
```

### 3. Mesclar Feature Branch na Branch develop:
```bash
1. git checkout develop
2. git merge feature/autenticar-usuario
3. git push origin develop
4. git branch -d feature/autenticar-usuario #deletar a branch local (opcional)
5. git push origin --delete feature/autenticar-usuario #deletar a branch remota (opcional)
```

### 4. Criar e Mudar para uma Nova Branch de Release;

```bash
1. git checkout -b release/1.0.0
2. git push origin release/1.0.0
```

### 5. Testes deverão ser feitos na Branch release/1.0.0 (caso haja um bugfix);

```bash
1. git checkout release/1.0.0
2. git checkout -b bugfix/timeout-error
3. git add .
4. git commit -m "fix(bugfix): Corrigido error de timeout ao tentar autenticar usuário"
5. git push origin bugfix/timeout-error
6. git checkout release/1.0.0
7. git merge bugfix/timeout-error
8. git push origin release/1.0.0
```

### 6. Mesclar Release em master e develop;

```bash
1. git checkout master
2. git merge release/1.0.0
3. git push origin master

4. git checkout develop
5. git merge release/1.0.0
6. git push origin develop
7. git branch -d release/1.0.0 #deletar a branch local (opcional)
8. git push origin --delete release/1.0.0 #deletar a branch remota (opcional)

```

### 7. Criar uma Tag para a Versão Lançada;

```bash
1. git checkout master
2. git tag -a v1.0.0 -m "Versão 1.0.0 - Funcionalidade de Autenticação de Usuários"
3. git push origin v1.0.0

4. git tag
5. git show v1.0.0
```

### 8. Correção de Bug em Produção: Criar e Mudar para Nova Branch Hotfix

```bash
1. git checkout master
2. git checkout -b hotfix/usuario-desativando
3. git add .
4. git commit -m "fix(hotfix): Corrige o bug de usuário desativando automaticamente"
4. git push origin hotfix/usuario-desativando
5. git checkout master
6. git merge hotfix/usuario-desativando
7. git push origin master
8. git tag -a v1.0.1 -m "Corrige bug: Usuário Desativando"
9. git push origin v1.0.1
10. git tag
11. git show v1.0.1
12. git checkout develop
13. git merge hotfix/usuario-desativando
14. git push origin develop
15. git branch -d hotfix/usuario-desativando #deletar a branch local (opcional)
16. git push origin --delete hotfix/usuario-desativando #deletar a branch remota (opcional)
```

## Links Adicionais

- [Video - GitFlow na prática](https://youtu.be/xC7frT2JPGE)