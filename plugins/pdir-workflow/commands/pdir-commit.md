---
description: Commit e push na branch atual (suporta WIP e Conventional Commits)
---

# PDIR: Commit

Sincroniza, commita e envia mudanças para origin.

## Instruções

### 1. Sincronizar e Verificar

Informações da branch:
- Branch atual: !`git branch --show-current`
- Status: !`git status --short`
- Diff: !`git diff --stat`

Verificar upstream (pode falhar se branch nova):
!`git rev-parse --abbrev-ref @{u}`

**Se o comando upstream retornou resultado:** execute `git pull --ff-only`
**Se o comando upstream falhou (branch nova):** pule o pull
**Se não houver mudanças:** Informar e encerrar.

### 2. Criar Commit

Formato: `tipo(escopo): descrição`

**Tipos:** `wip`, `feat`, `fix`, `docs`, `chore`, `refactor`, `style`, `test`, `perf`, `ci`, `build`

**Escopo:** área afetada (`auth`, `api`, `ui`, `db`, etc.) - **obrigatório**

```bash
git add -A

git commit -m "$(cat <<'EOF'
tipo(escopo): descrição

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
EOF
)"
```

### 3. Push

```bash
git push -u origin "$(git branch --show-current)"
```

### 4. Feedback Final

```
Commit realizado!

[hash] tipo(escopo): descrição
Branch: [branch]

Estado: nothing to commit, working tree clean
```

## Problemas Comuns

**Pre-commit modificou arquivos:**
```bash
git add -A && git commit --amend --no-edit && git push --force-with-lease
```

**Push rejeitado:**
```bash
git pull --rebase && git push
```
