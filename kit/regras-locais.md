# Regras locais — workflow de <NOME/PROFISSÃO>

> Complementa `CLAUDE.md`. A persona traz o conhecimento e o formato; este arquivo traz o
> **workflow**: onde ficam os trabalhos, como nomear, onde entregar, e a ordem de consulta
> das fontes. Preencher os `<placeholders>` e ajustar à sua realidade.

---

## 1. Organização de pastas

Raiz do projeto: `<RAIZ>`. Estrutura sugerida (adaptar os nomes ao domínio):

```
<RAIZ>/
├── CLAUDE.md                 # persona + conhecimento + formato (não mexer sem intenção)
├── regras-locais.md          # este arquivo
├── MEMORY.md                 # índice da memória de longo prazo
├── memory/                   # memórias (user/feedback/project/reference)
├── .claude/
│   └── ESTADO.md             # ledger vivo do projeto
├── corpus/
│   └── derived/              # fichas destiladas de fontes (leis, normas, diretrizes)
├── <trabalhos>/              # ex.: casos/ | processos/ | disciplinas/ | pericias/
│   └── <um-trabalho>/        # UMA PASTA POR TRABALHO (caso, processo, turma, laudo)
│       ├── briefing.md       # o que é, quem pediu, prazo
│       ├── documentos/       # material recebido
│       └── entregas/         # versões finais produzidas
└── modelos/                  # modelos reutilizáveis validados
```

- **Uma pasta por trabalho.** Casos, processos, provas e laudos não se misturam.
- **Modelos são ativo permanente:** todo documento validado que pode ser reusado vai
  para `modelos/` com uma nota do que ele resolve.

## 2. Convenção de nomes

- Trabalhos: `<tipo>_<identificador>_<AAAA-MM-DD>.md`
  (ex.: `peticao_processo-0001234_2026-07-10.md`, `laudo_ed-central_2026-07-10.md`)
- Fichas de corpus: `<FONTE>-<TEMA>-<ANO>.md` (ex.: `LEI-8666-LICITACOES-1993.md`,
  `NBR-6118-ESTRUTURAS-2023.md`, `SBC-IC-2022.md`)
- Datas sempre em `AAAA-MM-DD` (ordena sozinho).

## 3. Onde entregar (regra de saída)

- Entregável final **sempre** dentro de `entregas/` da pasta do próprio trabalho.
  A origem pode ser qualquer lugar; a entrega sobrepõe. **Nunca deixar a versão final
  espalhada** fora da pasta do trabalho.
- Anexos que acompanham a entrega (planilhas, gabaritos, memoriais) ficam no mesmo
  diretório, com sufixo descritivo.

## 4. Prioridade de consulta (fonte da verdade)

Ao precisar de um dado técnico/citação, consultar **nesta ordem** e nunca inventar:

1. `corpus/derived/` — ficha destilada da fonte (quando existir). **Citar daqui.**
2. <Fonte primária oficial vigente — ex.: lei/código atualizado, norma técnica, diretriz>.
3. <Fonte secundária confiável — ex.: doutrina de referência, manual institucional>.
4. Se nada disso resolver: marcar **[a confirmar]** e perguntar ao titular.
   Nunca fechar com dado chutado.

> Ao pesquisar algo importante que ainda não está no corpus, **destilar a fonte numa
> ficha** em `corpus/derived/` — assim o próximo trabalho já reusa (não repesquisar do zero).
>
> Para semear de uma vez as fichas das fontes mais recorrentes do seu domínio usando IA
> (sem risco de citação inventada), ver `docs/SEMEAR-CORPUS.md`.

## 5. Checklist antes de entregar

- <Adaptar por tipo de documento — 4 a 6 verificações objetivas. Ex.:>
- Todo dado técnico conferido na fonte ou marcado `[a confirmar]`.
- Fontes citadas com especificidade (artigo/item/seção, não só o nome da lei/norma).
- Nenhum dado do caso inventado (datas, números, nomes, valores).
- Estrutura conforme as regras de formato do `CLAUDE.md`.
- <Verificação específica do domínio — ex.: prazos conferidos; unidades e dimensões;
  gabarito fecha com o enunciado>.

## 6. Higiene do ledger

- Atualizar `.claude/ESTADO.md` ao fim de todo trabalho significativo (≤150 linhas).
- Lição que se repetir 2× ou for crítica → promover para `CLAUDE.md` e remover do ESTADO.md.
- Preferências estáveis do titular → memória de longo prazo (`memory/` + linha no
  `MEMORY.md`), não no ESTADO.
