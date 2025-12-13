# PDIR Workflow Plugin

Plugin Claude Code para o método PDIR (Planejar, Dividir, Implementar, Revisar) - desenvolvimento estruturado com IA.

## Instalação

### Pré-requisitos

- **Claude Code CLI** instalado e funcionando
- **GitHub CLI** (`gh`) autenticado:
  ```bash
  gh auth status  # verificar
  gh auth login   # se necessário
  ```
- **Git** configurado com acesso ao repositório

### Instalar o Plugin

```bash
# 1. Adicionar o marketplace
/plugin marketplace add hmaurus/pdir-workflow-plugin

# 2. Instalar o plugin
/plugin install pdir-workflow@hmaurus
```

### Verificar Instalação

```bash
/help  # Os comandos /pdir-* devem aparecer na lista
```

## Comandos

| Comando | Descrição | Argumentos |
|---------|-----------|------------|
| `/pdir-criar-prd` | descrição → PRD.md | `[descrição]` |
| `/pdir-listar-grupos` | PRD → grupos/subgrupos | `[arquivo] [grupos\|subgrupos]` |
| `/pdir-listar-tarefas` | grupo → lista de tarefas | `[arquivo] [grupo]` |
| `/pdir-criar-issue` | tarefa → Issue GitHub | `[tarefa]` |
| `/pdir-implementar-tarefa` | Issue → branch + código | `[número-issue]` |
| `/pdir-commit` | commit + push | - |
| `/pdir-draft-pr` | cria Draft PR | - |
| `/pdir-ready-pr` | marca PR pronto | - |
| `/pdir-merge-tarefa` | merge + limpeza | - |

## Fluxo PDIR

```
PRD.md → Grupos → Tarefas → Issue → Implementar → Commit → PR → Merge
```

### Fluxo Visual

```
┌─────────────────────────────────────────────────────────────┐
│                    /pdir-criar-prd                          │
└─────────────────────────┬───────────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                        PRD.md                               │
└─────────────────────────┬───────────────────────────────────┘
                          │ /pdir-listar-grupos
                          ▼
┌─────────────────────────────────────────────────────────────┐
│              lista-grupos-PRD.md                            │
└─────────────────────────┬───────────────────────────────────┘
                          │ /pdir-listar-tarefas (por grupo)
                          ▼
┌─────────────────────────────────────────────────────────────┐
│              lista-tarefas-[grupo].md                       │
└─────────────────────────┬───────────────────────────────────┘
                          │ Para cada tarefa:
                          ▼
┌─────────────────────────────────────────────────────────────┐
│  /pdir-criar-issue                                          │
│  /pdir-implementar-tarefa [issue]                           │
│  /pdir-commit (1 ou mais vezes)                             │
│  /pdir-draft-pr                                             │
│  /pdir-ready-pr                                             │
│  /pdir-merge-tarefa                                         │
└─────────────────────────────────────────────────────────────┘
```

## Estrutura do Plugin

```
pdir-workflow-plugin/
├── .claude-plugin/
│   └── plugin.json              # Metadados
├── commands/
│   ├── pdir-criar-prd.md
│   ├── pdir-listar-grupos.md
│   ├── pdir-listar-tarefas.md
│   ├── pdir-criar-issue.md
│   ├── pdir-implementar-tarefa.md
│   ├── pdir-commit.md
│   ├── pdir-draft-pr.md
│   ├── pdir-ready-pr.md
│   └── pdir-merge-tarefa.md
└── README.md
```

## Troubleshooting

### Comandos não aparecem em /help

```bash
# Reinstalar o plugin
/plugin uninstall pdir-workflow@hmaurus
/plugin install pdir-workflow@hmaurus

# Ou reiniciar o Claude Code
exit
claude
```

### Erro "gh: command not found"

```bash
# Instalar GitHub CLI
# macOS
brew install gh

# Ubuntu/Debian
sudo apt install gh

# Depois autenticar
gh auth login
```

### Erro de permissão no GitHub

```bash
# Verificar autenticação
gh auth status

# Reautenticar se necessário
gh auth login --scopes repo,read:org
```

## Licença

MIT

---

**Autor:** Maurus Henriques - maurus@maurus.com.br
