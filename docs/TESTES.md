# Testes — verificar que a estrutura funciona

> Cada teste: **Pré-condição → Passos → Resultado esperado → Se falhar**.
> Executável por qualquer pessoa (ou pela própria IA). Rodar T1–T4 após a instalação;
> T5–T7 só se adotou a camada Graphify (projetos de código).

---

## T1 — Warm-start de sessão (o núcleo do sistema)

- **Pré:** `.claude/ESTADO.md` existe e preenchido; protocolo de sessão presente no `CLAUDE.md`.
- **Passos:** abrir sessão nova do Claude Code na pasta-raiz do projeto e perguntar:
  *"Qual o estado atual do projeto e o próximo passo?"*
- **Esperado:** resposta correta citando os trabalhos em andamento e o próximo passo,
  com **uma leitura** (o ESTADO.md) — sem exploração ampla de pastas. Tempo até
  resposta útil < 2 min.
- **Se falhar** (a IA explora tudo do zero): verificar se o `CLAUDE.md` contém o bloco
  "Protocolo de sessão"; verificar se `.claude/ESTADO.md` existe e está ≤150 linhas.
  Se você abre sessões em um diretório *pai* do projeto, crie a entry de memória de
  bootstrap (ver `templates/protocolo-sessao.md`) — instrução só no CLAUDE.md não
  basta nesse cenário (lição validada em produção).

## T2 — Warm-start de subagente

- **Pré:** T1 passou.
- **Passos:** pedir à IA que lance um subagente com o conteúdo do ESTADO.md no prompt
  e a pergunta: *"Quais decisões vigentes não devem ser reabertas neste projeto?"*
- **Esperado:** o subagente lista as decisões do ESTADO.md sem nenhuma leitura de
  arquivo além do que recebeu.
- **Se falhar:** o prompt do spawn não incluiu o CONTEÚDO do ESTADO.md — "leia o
  ESTADO.md" não serve (o subagente pode não ter acesso ao caminho).

## T3 — Encerramento de sessão

- **Pré:** uma sessão de trabalho real concluída.
- **Passos:** pedir *"atualize o ESTADO.md com o que fizemos"* e verificar o arquivo.
- **Esperado:** data atualizada, status dos trabalhos refletindo a sessão, próximo
  passo exato reescrito, arquivo ainda ≤150 linhas.
- **Se falhar:** conferir se o bloco de protocolo no CLAUDE.md pede explicitamente a
  atualização; criar o hábito de pedir ao encerrar (a disciplina é sua, a escrita é da IA).

## T4 — Regra de promoção (anti-recorrência)

- **Pré:** uma lição registrada em "Lições ativas" do ESTADO.md aparece pela 2ª vez
  (mesmo erro/causa em sessão posterior).
- **Passos:** aplicar a regra: promover ao CLAUDE.md; remover do ESTADO.md.
- **Esperado:** lição presente no CLAUDE.md, ausente do L2; sessão seguinte respeita
  a regra sem que ela seja mencionada no prompt.
- **Se falhar** (erro ocorre 3ª vez mesmo promovido): a redação está ambígua —
  reescrever como regra operacional ("antes de X, faça Y"), não como narrativa do
  incidente.

## T4b — Contrato de fidelidade

- **Passos:** pedir um documento sobre tema cuja fonte ainda NÃO está no corpus e
  observar como a IA trata números/citações.
- **Esperado:** dados críticos vêm marcados `[a confirmar]` ou com a fonte consultada
  na própria sessão — nunca preenchidos "de memória" com confiança.
- **Se falhar:** reforçar a lista de dados proibidos no contrato do CLAUDE.md
  (quanto mais específica ao domínio, melhor) e registrar a falha nas Lições ativas.

---

## Testes da camada Graphify (opcional — só código)

## T5 — Instalação

- **Passos:** `uv tool install graphifyy` → `graphify install` → `graphify --version`
  → abrir o Claude Code e listar skills.
- **Esperado:** versão impressa sem erro; `/graphify` aparece nas skills.
- **Se falhar:** `uv` ausente → instalar uv ou usar `pipx install graphifyy`;
  binário não encontrado → `uv tool update-shell` e reabrir o terminal;
  ⚠ conferir que NÃO instalou `graphify` (um y só — é outro pacote, não relacionado).

## T6 — Qualidade do grafo

- **Pré:** `/graphify .` rodado no repositório.
- **Passos:** escolher um símbolo central do seu código e perguntar:
  *"O que quebra se eu mudar <símbolo>?"*
- **Esperado:** a resposta expõe a cadeia de dependências completa, cruzando as
  fronteiras de módulos/pacotes; os módulos centrais figuram entre os god nodes do
  `GRAPH_REPORT.md`.
- **Se falhar** (cadeia incompleta): PRIMEIRO refazer a consulta por nome de
  **símbolo** (`graphify explain "nomeDaFuncao"`) — lookup por caminho de arquivo
  retorna "No node matching" mesmo com o nó presente (falso negativo validado em
  produção). Depois: conferir se as extensões relevantes foram cobertas e se nenhuma
  pasta essencial está em ignore.

## T7 — Atualização incremental

- **Pré:** `graphify hook install` executado; T6 passou.
- **Passos:** commit pequeno tocando 1 arquivo → `graphify hook status` → verificar
  timestamp do `graphify-out/graph.json`.
- **Esperado:** rebuild automático pós-commit, rápido (só arquivos alterados).
- **Se falhar:** `graphify hook status` para diagnosticar; se o repo já tem hooks git
  (husky etc.), encadear — não substituir.

---

## Registro de resultados

Manter uma tabela no ESTADO.md ou aqui na sua cópia local:

| Data | Teste | Resultado | Observações |
|---|---|---|---|
| | | | |
