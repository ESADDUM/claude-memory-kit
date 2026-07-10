# Graphify — camada estrutural (opcional, só para projetos de código)

> Knowledge graph do código para o Claude Code: em vez de explorar arquivo por
> arquivo, a IA consulta um **mapa** — quem chama quem, o que quebra se mudar X.
> Só faz sentido para repositórios de **código-fonte**. Para bases de prosa
> (documentos, fichas, leis), use o padrão router do kit (índice + leitura sob
> demanda) — grafo não se aplica.

**Fontes verificadas (2026-06-11):**
- Repo canônico: https://github.com/safishamsi/graphify (MIT)
- Site oficial: https://graphify.net
- ⚠ **Pacote PyPI: `graphifyy` (DUPLO y).** `pip install graphify` (um y) instala um
  pacote NÃO relacionado. Existem forks não-oficiais no GitHub — usar só o repo acima.
- Economia real esperada: entre ~2,5× e as dezenas de × anunciadas, conforme o tipo
  de pergunta.

---

## Como funciona

**Pass 1 (grátis, sem LLM):** Tree-sitter (25+ linguagens) extrai classes, funções,
imports e call graphs — análise estática determinística.
**Pass 2 (sem API):** transcreve vídeos/áudios do repo localmente (faster-whisper).
**Pass 3 (usa LLM):** analisa docs/PDFs/imagens e agrega ao grafo.

Saídas: `graphify-out/graph.json` (dado bruto consultado nas queries — caminhos
relativos, **portátil, pode ser commitado** para o time/nuvem usar sem regenerar),
`GRAPH_REPORT.md` (god nodes + resumo — entra no warm-start) e `graph.html`
(visualização para humanos).

## Instalação

```bash
uv tool install graphifyy      # ou: pipx install graphifyy
graphify install               # registra a skill /graphify no Claude Code
graphify --version             # confirmar
```

Depois, dentro do repositório, no Claude Code: `/graphify .`

## Comandos principais

| Comando | O que faz |
|---|---|
| `/graphify .` | Gera/atualiza o grafo do diretório atual |
| `graphify query "pergunta"` | Consulta o grafo |
| `graphify explain "símbolo"` | Explica um símbolo com contexto do grafo |
| `graphify affected "símbolo"` | Impacto reverso: o que depende disso |
| `graphify hook install` | Auto-rebuild (só Pass 1, grátis) após cada git commit |
| `graphify claude install` | Hook always-on: toda busca consulta o grafo (ver ressalva abaixo) |

## Lições validadas em produção

- **Pipeline 100% gratuito** (sem API key, mesmo com repo cheio de docs):
  `graphify update . --no-cluster` (Pass 1/AST) → `graphify cluster-only . --no-label`.
  Atenção: `graphify extract .` puro EXIGE API key se houver docs/imagens no repo.
- **Consultar por nome de SÍMBOLO, não por caminho de arquivo.**
  `graphify explain "minhaFuncao"` ✅ · `graphify explain "src/lib/arquivo.ts"` ❌
  (retorna "No node matching" mesmo com o nó presente).
- **Commitar `graph.json` + `GRAPH_REPORT.md`** — é isso que dá o mapa a sessões na
  nuvem e ao time, sem a ferramenta instalada.
- **Não ativar o hook always-on de imediato:** ele adiciona latência/custo a TODA
  busca, inclusive as triviais. Usar sob demanda por ~1 semana e só então decidir.
- Instrução de instalação vinda de vídeo/terceiros → **verificar repo/PyPI antes**
  (o caso `graphify` vs `graphifyy` provou o risco).

## Integração com o kit

- Warm-start de sessão em repo de código = `.claude/ESTADO.md` + `GRAPH_REPORT.md`
  (≈4k tokens no total).
- Bloco a acrescentar no "Protocolo de sessão" do CLAUDE.md do repo:

```markdown
- **Pergunta estrutural** ("quem usa X?", "o que quebra se?", "onde está definido?"):
  rode `graphify query "<pergunta>"` ANTES de explorar arquivos manualmente.
- Após mudanças estruturais grandes sem commit: o grafo pode estar defasado —
  confie no código, não no grafo, até o próximo commit.
```

- Subagentes em repo com grafo: incluir no prompt, além do ESTADO.md, a seção de
  god nodes do `GRAPH_REPORT.md` (não o graph.json inteiro).

Verificação: testes T5–T7 em [TESTES.md](TESTES.md).
