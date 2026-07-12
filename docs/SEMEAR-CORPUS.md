# Semear o corpus com IA — sem ela inventar citação

> O `corpus/derived/` cresce naturalmente trabalho a trabalho (regras-locais §4).
> Mas há um atalho legítimo: **pedir à IA que semeie de uma vez as fichas das
> fontes mais recorrentes do seu domínio** (as 3–6 leis/normas/diretrizes que
> você cita toda semana). O risco óbvio: a IA "lembra" do texto da fonte e
> transcreve de memória — com artigo trocado, número plausível, redação antiga.
> Este protocolo elimina esse risco. Testado em produção (11/07/2026) semeando
> 4 fichas jurídicas de uma vez.

---

## A regra de ouro do semeio

**Trecho verbatim e número de artigo/item/seção só entram na ficha se vierem de
uma página que a IA BUSCOU NA MESMA SESSÃO** (busca web / fetch da fonte).
Memória de treino do modelo NUNCA é fonte — nem para "completar" um parágrafo
que a página cortou.

O que a IA não conseguir confirmar na página buscada vira, no lugar do dado:

```
[a confirmar: <exatamente o que falta e onde conferir>]
```

Nunca número plausível silencioso. O `[a confirmar]` visível é sucesso do
protocolo, não falha — ele diz ao titular exatamente o que conferir depois.

## O prompt de semeio (esqueleto)

Para cada lote de fichas, o pedido à IA deve conter:

1. **A regra de ouro acima, verbatim** — é ela que muda o comportamento.
2. **A lista de fichas** com, para cada uma: nome do arquivo na convenção
   `<FONTE>-<TEMA>-<ANO>.md`, o que capturar verbatim (quais artigos/itens/
   seções) e 1-2 linhas de "para que serve no meu trabalho" (a IA usa isso na
   seção de implicações — sem inventar detalhes além do que você deu).
3. **As fontes preferidas por ordem** (site oficial primeiro; espelho
   institucional confiável se o oficial bloquear — registrando qual foi usado).
4. **O formato**: apontar para `corpus/derived/EXEMPLO-FICHA.md` como modelo.
5. **Rastro obrigatório**: toda ficha termina com a URL realmente consultada +
   "Conferida em: <data>".
6. **Salvar cada ficha em disco assim que concluída** (se a sessão cair no
   meio, o que ficou pronto não se perde).
7. **Relatório final**: por ficha, a URL usada + a lista do que ficou
   `[a confirmar]` (se algo ficou).

## O que esperar na prática (caso real)

No semeio de 11/07/2026 (4 fichas jurídicas — lei, decisão de tribunal
superior, resolução, súmulas):

- **Sites oficiais bloqueiam acesso automatizado com frequência** (conexão
  derrubada, HTTP 403). O protocolo degradou correto: a IA usou espelhos
  institucionais (portal da Câmara, base do tribunal, diário oficial
  eletrônico), registrou a URL de cada um e marcou `[a confirmar na fonte
  primária]` no que só saiu de fonte secundária.
- 1 das 4 fichas saiu completa da fonte primária, sem lacunas; as outras 3
  vieram com 1-2 marcadores `[a confirmar]` cada — todos apontando exatamente
  o que conferir. **Zero citação inventada.**
- A conferência posterior dos `[a confirmar]` é tarefa curta e mecânica do
  titular (abrir a fonte oficial e bater o texto) — muito mais barata que
  auditar uma ficha inteira atrás de alucinação escondida.

## Depois do semeio

- Resolver os `[a confirmar]` contra a fonte primária quando ela estiver
  acessível, substituindo pelo verbatim e registrando a data (o próprio
  EXEMPLO-FICHA.md já prevê esse histórico).
- Daí em diante vale a regra normal: pesquisou fonte nova importante num
  trabalho → destila a ficha na hora (regras-locais §4).
