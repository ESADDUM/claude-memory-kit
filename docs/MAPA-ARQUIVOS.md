# Mapa de arquivos — papel exato de cada peça

> Referência única para qualquer agente (humano ou IA) saber **o que cada arquivo é,
> quem escreve nele, quem lê, e quando**. `<RAIZ>` = a pasta-raiz do seu projeto.

---

## Na raiz do projeto

| Arquivo | Papel | Escreve | Lê |
|---|---|---|---|
| `CLAUDE.md` | Persona profissional + contrato de fidelidade + conhecimento do domínio + regras de formato. **Muda raramente** — recebe lições promovidas (confirmadas 2× ou críticas) | o titular (ou a IA, com aprovação) | a IA, no início de TODA sessão (automático) |
| `regras-locais.md` | Workflow: organização de pastas, convenção de nomes, onde entregar, ordem de consulta das fontes | o titular | a IA, no início da sessão |
| `MEMORY.md` | Índice da memória de longo prazo — uma linha por memória, sem conteúdo | a IA, ao criar cada memória | a IA, para decidir qual memória abrir |
| `memory/*.md` | Memórias individuais (tipos: user / feedback / project / reference) | a IA | a IA, sob demanda via índice |

## Em `.claude/`

| Arquivo | Papel | Escreve | Lê |
|---|---|---|---|
| `.claude/ESTADO.md` | **Ledger vivo do projeto (L2)** — máx. 150 linhas: trabalhos em andamento, decisões vigentes, lições ativas, próximo passo exato | a IA, no fim de toda sessão significativa | todo início de sessão + todo prompt de subagente (conteúdo integral) |

⚠ O ESTADO.md preenchido **contém dados do seu trabalho** (casos, clientes, prazos) —
vive na SUA pasta de projeto, nunca em repositório compartilhado do kit.

## Em `corpus/`

| Arquivo | Papel | Escreve | Lê |
|---|---|---|---|
| `corpus/derived/<FONTE>-<TEMA>-<ANO>.md` | Ficha destilada de uma fonte (lei, norma, diretriz, julgado) — trechos críticos **verbatim** + referência exata | a IA, ao pesquisar a fonte (conferido pelo titular) | a IA, sempre que precisar citar o tema — **cita da ficha, não de memória** |

Nunca carregar a fonte bruta inteira (PDFs grandes) na sessão — só as fichas.

## Pastas de trabalho

| Pasta | Papel |
|---|---|
| `<trabalhos>/<um-trabalho>/` | Uma pasta por caso/processo/prova/laudo: briefing, documentos recebidos, `entregas/` |
| `modelos/` | Documentos validados reutilizáveis |

## Camada estrutural (opcional — só projetos de código)

| Arquivo | Papel |
|---|---|
| `graphify-out/graph.json` | Grafo do código consultado nas queries (portátil, pode ser versionado) |
| `GRAPH_REPORT.md` | Resumo do grafo (nós centrais) — entra no warm-start e em prompts de subagente |

Detalhes: [GRAPHIFY.md](GRAPHIFY.md).

## Fluxo resumido de uma sessão

```
INÍCIO   → IA lê CLAUDE.md (automático) + .claude/ESTADO.md
TRABALHO → dado técnico? consultar corpus/derived/ → fonte oficial → [a confirmar]
         → subagente? prompt inclui o CONTEÚDO do ESTADO.md
FIM      → atualizar o delta no ESTADO.md (≤150 linhas)
         → lição confirmada 2×? promover ao CLAUDE.md e remover do ESTADO.md
```
