# Orientações para a IA — instalar e operar esta estrutura

> Este documento é dirigido **à IA** (Claude ou outro agente) que vai instalar o kit
> para um usuário e operá-lo nas sessões seguintes. Se você é a IA lendo isto: estas
> são suas instruções de trabalho.

---

## Fase 1 — Instalação (primeira sessão)

1. **Confirme a pasta-raiz** com o usuário antes de criar qualquer coisa. Nunca
   assuma o diretório atual sem confirmar.
2. **Leia os 5 arquivos do kit** (`kit/`) e explique ao usuário, em 3-4 linhas, o
   papel de cada camada e o que é o contrato de fidelidade profissional.
3. **Entreviste antes de preencher — uma pergunta por vez.** Você precisa descobrir:
   - profissão, especialidade e registro profissional (se houver);
   - os 2-4 tipos de documento mais produzidos e a estrutura de cada um;
   - as fontes de verdade do domínio, em ordem de prioridade;
   - o público leitor e o tom adequado;
   - o trabalho em andamento agora (alimenta o primeiro ESTADO.md).
   **Nunca invente dado do usuário.** Placeholder sem resposta fica como está.
4. **Instale nos lugares certos:** `CLAUDE.md`, `regras-locais.md`, `MEMORY.md` na
   raiz; `ESTADO.md` em `.claude/`; ficha-exemplo em `corpus/derived/`; criar
   `memory/` vazia. Depois remova a pasta `kit/` (com confirmação do usuário).
5. **Adapte o contrato de fidelidade ao domínio:** liste explicitamente os dados que
   você nunca preencherá de memória naquela profissão. Exemplos por área:
   - **Advocacia:** artigo/parágrafo de lei, número e ementa de julgado, súmula,
     prazo processual, valor de alçada, jurisprudência "dominante".
   - **Medicina:** dose, posologia, ponto de corte, meta terapêutica, nome/ano de
     estudo, classe de recomendação/nível de evidência.
   - **Engenharia:** número e item de norma, causa de anomalia não observada,
     resistência/dimensão de projeto, responsabilidade técnica.
   - **Contabilidade/fiscal:** alíquota, prazo de obrigação, dispositivo legal,
     enquadramento.
   - **Docência:** fato/citação de fonte acadêmica, dado histórico/numérico, autoria.
6. **Explique ao usuário a regra nº 1** em uma frase e **ensine a rotina de
   encerramento** (atualizar ESTADO.md ao fim de todo trabalho significativo).
7. **Não produza nenhum documento de trabalho na sessão de instalação** — só instale,
   adapte e registre o próximo passo no ESTADO.md.

## Fase 2 — Operação (todas as sessões seguintes)

### Ao iniciar

1. Ler `CLAUDE.md` + `regras-locais.md` (persona e workflow).
2. Ler `.claude/ESTADO.md` **antes de explorar pastas** — ele diz onde o trabalho
   parou e qual o próximo passo.
3. Carregar fichas de `corpus/derived/` **sob demanda** (só a pertinente ao tema).

### Durante o trabalho

- **Contrato de fidelidade sempre ativo:** dado técnico do domínio ou vem de ficha
  do corpus / fonte conferida na sessão, ou sai como `[a confirmar]`. Nunca por
  plausibilidade. Preferir omitir a citar errado.
- **Não invente dado do caso** (nome, data, número, valor). Campo sem informação
  fica vazio ou vira pergunta.
- **Pesquisou fonte nova importante?** Proponha destilá-la numa ficha em
  `corpus/derived/` antes de encerrar.
- **Subagente?** Inclua o CONTEÚDO do ESTADO.md no prompt (não só o caminho).

### Ao encerrar trabalho significativo

1. Atualizar o delta no `.claude/ESTADO.md`: data, status dos trabalhos, decisões
   novas, **próximo passo exato** (uma frase acionável).
2. Respeitar o teto de 150 linhas: para entrar algo, algo sai ou é promovido.
3. Falha nova nesta sessão → "Lições ativas" (formato: causa → regra prática).
4. Lição repetida 2× ou crítica → promover ao `CLAUDE.md` (redigida como regra
   operacional, não como narrativa) e remover do ESTADO.md.
5. Preferência estável do usuário descoberta na sessão → arquivo em `memory/` +
   linha no `MEMORY.md`.

## O que NUNCA fazer

- Preencher dado técnico ou dado do usuário por suposição.
- Deixar o ESTADO.md passar de 150 linhas ou desatualizado após sessão significativa.
- Copiar para o projeto do usuário conteúdo de outra pessoa (exemplos com nomes,
  caminhos de outra máquina, casos de terceiros).
- Reabrir decisões listadas em "Decisões vigentes" sem o usuário pedir.
