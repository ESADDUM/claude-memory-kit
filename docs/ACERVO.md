# Camada de acervo — o know-how destilado (redijo daqui)

> A camada de **corpus** (`corpus/derived/`) responde *"o que a fonte diz"* — leis, normas,
> diretrizes, verbatim, para **citar** com exatidão. Ela não escreve o seu documento.
> A camada de **acervo** responde *"como eu resolvo isto e com que palavras"* — o nexo do
> problema e os **trechos prontos** destilados dos seus próprios trabalhos anteriores, para
> **redigir** rápido e no seu estilo. Juntas, corpus + acervo é o que transforma "consultar
> a fonte" em "entregar a peça".
>
> Validada em produção antes de virar kit: um acervo por tipo de problema, com trechos
> extraídos de anos de trabalho real, cortou drasticamente o tempo de redação e a variação
> indevida entre documentos.

---

## Corpus × Acervo — dois eixos, não duas cópias

| | **`corpus/derived/`** | **`acervo/`** |
|---|---|---|
| Unidade (1 arquivo =) | uma **fonte** (lei, norma, diretriz, súmula) | um **problema/tema** de trabalho |
| Conteúdo | o que a fonte **literalmente diz**, verbatim, referência exata | o **nexo** (causal/argumentativo) + **trechos prontos** do seu acervo |
| Função | **cito daqui** — verdade externa ancorada | **redijo daqui** — como aplico + as palavras que eu escrevo |
| Origem do texto | transcrição da fonte oficial | destilação dos **seus** documentos já entregues |
| Como cresce | ao pesquisar fonte nova (ver `SEMEAR-CORPUS.md`) | ao entregar um trabalho repetível — vira trecho reusável |

O acervo **aponta para** o corpus: cada trecho que cita uma fonte remete à ficha
(`[[corpus/derived/FONTE-X]]`), nunca à memória. E os arquivos de acervo se **cruzam entre
si** (tema → nexo → tema relacionado) — essa malha de links é, na prática, um grafo de
conhecimento **mantido à mão como subproduto do trabalho**, sem ferramenta nenhuma.

## ⚠ A fronteira anti-alucinação da Camada B (a regra que a torna segura)

O acervo é onde uma IA "prestativa" mais tende a **inventar doutrina bem-escrita**. A regra
que impede isso:

- **Trecho pronto é COLHIDO, não gerado.** Cada bloco entre aspas na seção "trechos prontos"
  vem de um documento **que você realmente entregou** — a IA distila/organiza o que existe,
  ela **não é autora** de tese, conduta ou nexo novo. Se não há trecho real ainda, o campo
  fica `[a colher do acervo]`, não preenchido por plausibilidade.
- **Toda fonte citada dentro de um trecho continua valendo a regra do corpus:** número de
  artigo/item/julgado só se estiver na ficha correspondente; senão, `[a confirmar na fonte]`.
- **Nexo/causa segue o contrato de fidelidade** (ver `CLAUDE.md`): só o observado/documentado;
  hipótese marcada como hipótese.

Em uma frase: **a Camada A garante que a citação é verdadeira; a Camada B garante que a prosa
é sua, não inventada.**

## Estrutura de um arquivo de acervo

Indexar por **problema/tema**, não por tipo de documento. Um arquivo por tema recorrente do
seu domínio (ex.: advocacia — `consumidor-vicio-produto.md`, `trabalhista-verbas-rescisorias.md`;
medicina — `dor-toracica-conduta.md`; engenharia — `corrosao-armaduras.md`). Modelo pronto em
`acervo/EXEMPLO-TEMA.md`. Cada arquivo, tipicamente:

1. **Cabeçalho + links** para temas relacionados e para as fichas de corpus pertinentes.
2. **Situação típica / nexo** — a cadeia (causal ou argumentativa) que se repete no tema.
3. **Variações/estágios** — como o problema se apresenta (uma tabela ajuda).
4. **Fundamento** — ponteiros para as fichas de `corpus/derived/` (cito de lá).
5. **★ Trechos prontos (linguagem do acervo)** — os blocos reusáveis colhidos dos seus
   documentos. É o coração do arquivo.
6. **Solução/conduta/medida padrão** — o encaminhamento típico.
7. **Armadilhas** — o que costuma dar errado ou se confundir neste tema.

## Como construir (incremental, sem esforço concentrado)

Não é um projeto à parte — cresce como resíduo de trabalhar:

1. Terminou um documento que você vai repetir (uma peça, uma conduta, um laudo de um tipo
   comum)? **Recorte os 2–4 trechos reusáveis** dele para o arquivo de acervo do tema.
2. Marque a fonte de cada trecho com `[[corpus/derived/FONTE]]`; se a ficha ainda não existe,
   destile-a antes (ver `SEMEAR-CORPUS.md`).
3. Ligue o novo arquivo aos temas vizinhos com `[[links]]`.
4. Da próxima vez, o agente **redige a partir do trecho**, ajustando ao caso — em vez de
   escrever do zero e arriscar variar o que já estava certo.

> Assim como o corpus tem teto e destilação, o acervo se mantém **enxuto**: trecho que virou
> padrão consolidado sobe para as "Regras de formato" do `CLAUDE.md`; trecho obsoleto (cita
> fonte revogada, conduta superada) se corrige ou apaga na hora.

## Onde se encaixa nas camadas

O acervo é **L3 permanente**, irmão do corpus (ver `ARQUITETURA.md` §2). O warm-start de uma
sessão de redação passa a ser: `ESTADO.md` (o que está em andamento) + a ficha de corpus da
fonte + o arquivo de acervo do tema. Nenhuma infraestrutura nova — são arquivos Markdown na
pasta do projeto.

Verificação prática: [TESTES.md](TESTES.md).
