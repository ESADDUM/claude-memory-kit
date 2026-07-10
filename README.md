# claude-memory-kit

Framework de **memória e contexto persistente** para quem trabalha com o Claude
(Claude Code no terminal, claude.ai/code, subagentes). Serve para **qualquer
profissão**: engenharia, medicina, advocacia, docência, contabilidade, arquitetura…

**O problema que resolve:** toda sessão nova de IA começa "fria" — ela não lembra o
que você decidiu ontem, re-explora suas pastas do zero, repete erros já corrigidos e
gasta tempo (e tokens) re-derivando contexto que você já pagou.

**A solução:** uma estrutura de arquivos em camadas que a IA lê no início de cada
sessão e atualiza no fim:

```
L3  PERMANENTE   CLAUDE.md + fichas de fontes (corpus/)   ← "como eu trabalho / o que eu sei"
L2  LEDGER       .claude/ESTADO.md (máx. 150 linhas)      ← "onde estamos / o que decidimos"
L1  HISTÓRICO    snapshots de sessão + índice             ← "o que aconteceu, com evidência"
ESTRUTURAL (opcional, só p/ código)  Graphify             ← "onde as coisas estão no código"
```

E um **contrato de fidelidade profissional** como regra nº 1 da persona: a IA nunca
inventa dado do seu domínio (dose, norma, jurisprudência, número) — ou está
fundamentado numa fonte conferida, ou fica marcado `[a confirmar]`.

---

## Como usar — escolha seu caminho

| Caminho | Para quem | Comece por |
|---|---|---|
| **1. Automático** (recomendado) | Quem quer que a própria IA instale tudo, entrevistando você | [PROMPT-PRONTO.md](PROMPT-PRONTO.md) |
| **2. Guiado** | Quem nunca usou o Claude no terminal — do zero, passo a passo | [INSTALACAO.md](INSTALACAO.md) |
| **3. Manual** | Quem já usa Claude Code e só quer os arquivos | copie a pasta [kit/](kit/) e siga o Quickstart abaixo |

## Quickstart (caminho manual)

1. Copie o conteúdo de `kit/` para a raiz da pasta do seu projeto
   (`CLAUDE.md`, `regras-locais.md`, `MEMORY.md` na raiz; `ESTADO.md` dentro de `.claude/`).
2. Substitua os placeholders (`<NOME>`, `<PROFISSÃO>`, `<REGISTRO>`, `<RAIZ>`, …) —
   ou deixe que a IA entreviste você usando o [PROMPT-PRONTO.md](PROMPT-PRONTO.md).
3. Preencha o bloco de conhecimento do `CLAUDE.md` **incrementalmente** — não precisa
   de tudo no dia 1; cada trabalho entregue alimenta uma seção.
4. Projeto de código-fonte? Veja a camada estrutural opcional em [docs/GRAPHIFY.md](docs/GRAPHIFY.md).
5. Valide com os testes T1–T3 de [docs/TESTES.md](docs/TESTES.md).

## Conteúdo do repositório

| Arquivo/pasta | O quê |
|---|---|
| [INSTALACAO.md](INSTALACAO.md) | Guia passo a passo humano — do "instalar o Claude Code" ao primeiro trabalho |
| [PROMPT-PRONTO.md](PROMPT-PRONTO.md) | Prompt único: cole na IA e ela instala e adapta tudo sozinha |
| [kit/](kit/) | Arquivos-semente genéricos com placeholders (persona, workflow, ledger, memória, ficha de fonte) |
| [docs/ARQUITETURA.md](docs/ARQUITETURA.md) | A decisão de arquitetura: as camadas, regras de promoção, protocolo de sessão |
| [docs/MAPA-ARQUIVOS.md](docs/MAPA-ARQUIVOS.md) | Papel exato de cada arquivo: quem escreve, quem lê, quando |
| [docs/ORIENTACOES-PARA-IA.md](docs/ORIENTACOES-PARA-IA.md) | Instruções para a IA que vai instalar e operar a estrutura |
| [docs/TESTES.md](docs/TESTES.md) | Testes T1–T7: como verificar que a estrutura está funcionando |
| [docs/GRAPHIFY.md](docs/GRAPHIFY.md) | Camada estrutural opcional para projetos de código (knowledge graph) |
| [templates/](templates/) | Template do ESTADO.md e bloco de protocolo de sessão para colar no CLAUDE.md |

## Princípios deste repositório

- Este repo versiona **apenas o framework** (guias, templates, arquivos-semente com
  placeholders).
- **Nunca commitar aqui:** `ESTADO.md` preenchidos, snapshots de sessão, dados de
  clientes/pacientes/processos, chaves, nomes reais — as instâncias vivem na pasta de
  projeto de cada pessoa.
- Ao adotar o kit, crie seus arquivos **na sua pasta de projeto**, nunca neste repo.
