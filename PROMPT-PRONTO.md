# Prompt pronto — a IA instala tudo sozinha

> **Como usar:** abra o Claude Code **na sua pasta-raiz de projeto** (com a pasta
> `kit/` já copiada para dentro dela — ver [INSTALACAO.md](INSTALACAO.md) Partes 2 e 3),
> copie **todo o bloco abaixo** e cole como primeira mensagem.
>
> Se o Claude não estiver aberto na pasta do projeto, acrescente na primeira linha:
> `A pasta-raiz do meu projeto é <caminho completo>.`

---

```
Estou montando minha estrutura de memória e trabalho no Claude, a partir do
claude-memory-kit (https://github.com/ESADDUM/claude-memory-kit). Os arquivos-semente
estão na pasta `kit/` dentro deste diretório (ou no caminho que eu indicar). São eles:

- CLAUDE.md            → persona profissional + contrato de fidelidade + regras de formato
- regras-locais.md     → workflow: organização de pastas, nomes, onde entregar, ordem
                         de consulta das fontes
- MEMORY.md            → índice da memória de longo prazo
- .claude/ESTADO.md    → ledger vivo do projeto (o que estou fazendo agora)
- corpus/derived/EXEMPLO-FICHA.md → modelo de ficha de fonte destilada

O que eu quero que você faça, NESTA ORDEM:

1. LEIA os 5 arquivos e me explique em 3-4 linhas como a estrutura funciona:
   para que serve cada camada e o que é o "contrato de fidelidade profissional".

2. Me ENTREVISTE, uma pergunta de cada vez, para adaptar o kit a mim. Pergunte
   pelo menos: (a) minha profissão e especialidade; (b) meu nome e registro
   profissional, se houver (OAB, CRM, CREA, CRC...); (c) os 2-4 tipos de documento
   que produzo com mais frequência (petição, laudo, prova, parecer, relatório...);
   (d) quais são minhas fontes de verdade, em ordem de prioridade (leis, normas,
   diretrizes, jurisprudência, manuais); (e) para quem escrevo (juiz, cliente leigo,
   aluno, síndico...) e o tom adequado; (f) qual o trabalho em andamento agora.
   NÃO invente nenhum dado meu — pergunte.

3. INSTALE: mova os arquivos do kit para os lugares certos (CLAUDE.md,
   regras-locais.md e MEMORY.md na raiz; ESTADO.md dentro de .claude/; a ficha em
   corpus/derived/), crie as pastas memory/ e corpus/derived/ se não existirem, e
   preencha TODOS os placeholders com as minhas respostas da entrevista.

4. ADAPTE o conteúdo à minha profissão: o "contrato de fidelidade" deve listar os
   dados do MEU domínio que você nunca pode inventar (ex.: advogado = número de
   processo, artigo de lei, ementa de julgado, prazo; médico = dose, ponto de corte,
   nome de estudo; engenheiro = número e item de norma, causa de anomalia). As
   "regras de formato" devem refletir os documentos que EU produzo, com a estrutura
   que eu descrever. O esqueleto de conhecimento do CLAUDE.md deve ter os grandes
   temas da minha especialidade, marcados [a preencher] — vamos alimentá-los
   incrementalmente a cada trabalho.

5. Me explique a REGRA MAIS IMPORTANTE em uma frase: por que você nunca vai
   preencher um dado técnico do meu domínio "de memória" — sempre de uma fonte
   conferida ou marcando [a confirmar].

6. Ao terminar: apague a pasta kit/ (os arquivos já estarão instalados), me diga
   qual é o "próximo passo" registrado no ESTADO.md, e me ensine a rotina de
   encerramento de sessão (atualizar o ESTADO.md ao fim de todo trabalho
   significativo).

Não comece a produzir nenhum documento ainda — só instale, adapte e me entreviste.
```

---

## Depois da instalação

A partir da segunda sessão, o fluxo é automático: a IA lê o `CLAUDE.md` (persona) e
o `.claude/ESTADO.md` (onde vocês pararam) e continua de onde parou. Sua única
disciplina é pedir a atualização do `ESTADO.md` ao encerrar cada trabalho — e cobrar
o contrato de fidelidade quando notar um dado sem fonte.
