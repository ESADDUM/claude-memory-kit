# Bloco "Protocolo de sessão" — colar no CLAUDE.md de cada projeto

> O `kit/CLAUDE.md` já traz este bloco embutido. Use este template quando quiser
> adicionar o protocolo a um projeto que já tem CLAUDE.md próprio.
> Substituir `<repo de código?>` conforme o projeto tenha ou não Graphify ativo.

```markdown
## Protocolo de sessão (memória)

- **Ao iniciar:** leia `.claude/ESTADO.md` antes de explorar pastas ou código.
  <Se repo com Graphify:> Para perguntas estruturais ("quem usa X?", "o que quebra
  se?"), consulte `GRAPH_REPORT.md` / rode `graphify query` antes de abrir arquivos.
- **Ao encerrar trabalho significativo:** atualize o delta em `.claude/ESTADO.md`
  (máx. 150 linhas — para entrar algo, algo sai ou é promovido para este CLAUDE.md).
- **Subagentes:** inclua o CONTEÚDO de `.claude/ESTADO.md` no prompt do spawn
  (não apenas o caminho). <Se Graphify:> inclua também os god nodes do GRAPH_REPORT.md.
- **Lições:** falha nova → "Lições ativas" do ESTADO.md; lição repetida 2× ou crítica →
  promover para este CLAUDE.md e remover do ESTADO.md.
```

---

# Entry de memória — para quem abre sessões fora da pasta do projeto

> ⚠ **O bloco acima é necessário mas não suficiente** quando a sessão é aberta em um
> diretório *pai* do projeto (ex.: `C:\` em vez de `C:\MeuProjeto`): o agente entra
> no fluxo de busca em memória antes de processar instruções do CLAUDE.md, ignora o
> protocolo e explora pastas do zero (lição validada em produção — teste T1).
>
> **Canal confiável para bootstrap entre diretórios = memória nativa com caminho absoluto.**
> Se você sempre abre o Claude dentro da pasta do projeto, pule esta seção.

Crie o arquivo abaixo em `~/.claude/projects/<hash-do-dir>/memory/project_<nome>_bootstrap.md`:

```markdown
---
name: project-<nome>-bootstrap
description: "Estado e ESTADO.md do projeto <Nome> — ler antes de explorar pastas"
metadata:
  type: project
---

## Regra de acesso (OBRIGATÓRIA)

Ao receber qualquer pergunta sobre estado, status ou próximo passo do projeto **<Nome>**,
leia `<caminho-absoluto>/.claude/ESTADO.md` como primeira ação — antes de qualquer
busca em pastas ou arquivos.

**Why:** exploração de pastas reconstrói contexto do zero; o ESTADO.md é o ledger vivo
mantido atualizado ao fim de cada sessão.

**How to apply:** primeira ação = Read do ESTADO.md. Só explorar pastas se o ESTADO.md
não responder a pergunta.
```

Adicione uma linha no `MEMORY.md` do mesmo diretório:

```
- [Bootstrap <Nome>](project_<nome>_bootstrap.md) — <Nome>=`<caminho-absoluto>/.claude/ESTADO.md` · Ler ANTES de explorar pastas
```

> Para encontrar o hash do diretório da sessão, abra o Claude Code no diretório em
> questão e veja qual pasta em `~/.claude/projects/` tem data recente.
> Windows: `Get-ChildItem "$env:USERPROFILE\.claude\projects" | Sort-Object LastWriteTime -Desc | Select-Object -First 5`
