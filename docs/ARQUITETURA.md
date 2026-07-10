# Arquitetura — Memória em camadas (Pirâmide de Contexto)

> A decisão de arquitetura por trás do kit: por que as camadas existem, como a
> informação sobe de uma para a outra, e o protocolo de sessão que faz tudo girar.
> Validada em produção em projetos reais (engenharia de laudos, desenvolvimento de
> software e orquestração de agentes) antes de ser generalizada neste kit.

---

## 1. O problema

Sem estrutura, o conhecimento entre sessões de IA fica fragmentado:

- Cada sessão nova começa **fria**: re-explora pastas, relê documentos, re-deriva
  decisões já tomadas — pagando de novo em tempo e tokens.
- Lições aprendidas (um erro corrigido, uma preferência sua) **evaporam** ao fechar
  a sessão e o erro se repete semanas depois.
- Subagentes e sessões na nuvem nascem sem nenhum contexto do que já foi feito.
- O que a IA "lembra" fica espalhado em lugares que não conversam entre si.

## 2. A decisão: camadas com pipeline de destilação

```
L3  PERMANENTE   CLAUDE.md + corpus/derived/ (fichas)   ← muda raramente, destilado 2×
L2  LEDGER       .claude/ESTADO.md  (≤150 linhas)       ← atualizado a cada sessão
L1  HISTÓRICO    snapshots de sessão + índice           ← registro bruto, com evidência
```

- **L1 — Histórico de sessões** (opcional, para quem quer rastro completo): ao fim de
  cada sessão significativa, um snapshot do que funcionou/falhou/foi decidido, com um
  índice por projeto. Retenção: destilar as lições e apagar após ~30 dias.
- **L2 — Ledger do projeto** (o coração do sistema): `<raiz>/.claude/ESTADO.md`,
  máximo **150 linhas**. Estado vivo: trabalhos em andamento, decisões vigentes,
  lições ativas, **próximo passo exato**. Template em `templates/ESTADO-template.md`.
- **L3 — Permanente:** o `CLAUDE.md` (persona + contrato de fidelidade + regras de
  formato) e as fichas de fonte em `corpus/derived/` (padrão *router*: carrega só o
  índice/ficha pertinente, nunca a base inteira).

### Regras de promoção (o pipeline)

1. Falha/descoberta ocorre 1× → registro no histórico (L1) ou direto nas
   "Lições ativas" do ESTADO.md.
2. Lição que mudaria o comportamento da próxima sessão → entra em "Lições ativas" do L2.
3. Lição confirmada 2+ vezes, **ou crítica** (prejuízo real, dado errado entregue) →
   promove ao L3 (CLAUDE.md) e **sai do L2**.
4. O teto de 150 linhas do L2 força a destilação: para entrar algo, algo sai
   (apaga ou promove).

> Redação de lição promovida: regra operacional ("antes de X, faça Y"), nunca
> narrativa do incidente. Regra ambígua é regra que falha na 3ª vez.

### Protocolo de sessão

- **Início:** ler `<raiz>/.claude/ESTADO.md` (≈2k tokens) em vez de re-explorar tudo.
- **Fim:** atualizar o delta no ESTADO.md (+ snapshot L1, se adotado).

### Subagentes (warm-start barato)

Nunca lançar subagente frio. O prompt do subagente inclui:
1. O **conteúdo** do ESTADO.md (≤150 linhas, custo fixo pequeno) — não apenas o
   caminho, porque o subagente pode não ter acesso a ele;
2. **Ponteiros** (não conteúdo) para o L3 relevante — ex.: "tema X → leia a ficha
   `corpus/derived/FONTE-X.md`".

### Sessões na nuvem (claude.ai/code)

Nenhuma infraestrutura extra: como o L2 fica **dentro da pasta/repositório do
projeto**, qualquer agente que abre o projeto ganha o mesmo warm-start.
Pré-requisito: ESTADO.md presente e citado no CLAUDE.md do projeto.

## 3. Lição validada — bootstrap entre diretórios

**Sintoma:** quando a sessão é aberta num diretório *pai* do projeto (ex.: `C:\` em
vez de `C:\MeuProjeto`), a IA pode entrar no fluxo de exploração antes de processar
o CLAUDE.md do projeto — e ignorar o protocolo.

**Lição (validada em produção):**

> **O canal confiável para bootstrap entre diretórios é a memória nativa do Claude
> Code, não o CLAUDE.md.** Uma entrada na project memory com o **caminho absoluto**
> do ESTADO.md dispara a leitura antes de qualquer exploração de pastas.

Como criar essa entrada: ver `templates/protocolo-sessao.md` (seção "Entry de
memória"). Se você sempre abre o Claude dentro da pasta do projeto, isso é
dispensável.

## 4. Camada estrutural — Graphify (opcional, só para código)

As camadas acima cobrem memória **episódica** (o que aconteceu, o que foi decidido).
Para projetos de **código-fonte**, o [Graphify](GRAPHIFY.md) adiciona a camada
**estrutural**: um knowledge graph do código (quem chama quem, o que quebra se mudar
X), eliminando a exploração arquivo-a-arquivo. Warm-start completo = ESTADO.md
(episódico) + GRAPH_REPORT.md (estrutural) ≈ 4k tokens.

Não se aplica a bases de prosa (documentos, fichas) — para essas, o padrão router
(índice + leitura sob demanda) resolve melhor.

## 5. Critérios de sucesso

- Sessão nova em projeto conhecido começa a produzir em < 2 min, sem re-exploração.
- Nenhuma lição registrada se repete como erro 3 semanas depois.
- Um agente na nuvem consegue continuar o trabalho do terminal lendo só a pasta do
  projeto.
- Nenhum dado técnico entregue sem fonte ou sem `[a confirmar]`.

Verificação prática: [TESTES.md](TESTES.md).
