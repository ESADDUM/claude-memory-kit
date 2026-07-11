# Guia de instalação — passo a passo (do zero)

> Para quem **nunca usou o Claude no terminal**. Ao final você terá o Claude Code
> instalado, uma pasta de projeto organizada e a estrutura de memória funcionando —
> adaptada à sua profissão.
>
> Tempo estimado: 30–45 minutos. Não precisa saber programar.

---

## Parte 1 — Instalar o Claude Code

### 1.1 Criar a conta

1. Acesse https://claude.ai e crie uma conta (ou entre na existente).
2. O Claude Code funciona melhor com um plano pago (Pro ou superior) — o plano
   gratuito tem limites baixos para trabalho profissional.

### 1.2 Instalar

**Windows:** abra o *PowerShell* (menu Iniciar → digite "PowerShell") e rode:

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Mac/Linux:** abra o *Terminal* e rode:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Depois **feche e reabra o terminal**.

### 1.3 Primeiro login

No terminal, digite:

```
claude
```

Na primeira vez ele abre o navegador para você autorizar com sua conta. Autorize e
volte ao terminal. Para sair do Claude a qualquer momento: digite `/exit`.

> **Dica:** dentro do Claude, comandos que começam com `/` são comandos do programa
> (ex.: `/model` escolhe o modelo, `/exit` sai). Todo o resto que você digitar é
> conversa com a IA.

---

## Parte 2 — Criar a pasta do projeto

A estrutura de memória vive numa **pasta-raiz** que concentra seu trabalho com a IA.
Escolha um lugar estável (fora de Downloads, de preferência fora de pastas
sincronizadas tipo OneDrive/Drive, que às vezes travam arquivos).

**Windows (PowerShell):**

```powershell
mkdir C:\MeuProjeto
cd C:\MeuProjeto
```

**Mac/Linux:**

```bash
mkdir ~/MeuProjeto
cd ~/MeuProjeto
```

> Troque `MeuProjeto` por um nome real: `Advocacia`, `Consultorio`, `Pericias`,
> `Aulas`… Uma pasta-raiz por área de trabalho.

---

## Parte 3 — Baixar o kit

**Opção A — sem git:** na página do repositório no GitHub, clique em
**Code → Download ZIP**, extraia, e copie a pasta `kit/` para dentro da sua
pasta-raiz.

**Opção B — com git:**

```
git clone https://github.com/ESADDUM/claude-memory-kit.git
```

e copie a pasta `kit/` do clone para a sua pasta-raiz.

Ao final, sua pasta deve estar assim:

```
MeuProjeto/
└── kit/
    ├── CLAUDE.md
    ├── regras-locais.md
    ├── MEMORY.md
    ├── .claude/ESTADO.md
    └── corpus/derived/EXEMPLO-FICHA.md
```

---

## Parte 4 — Deixar a IA instalar (recomendado)

1. No terminal, **dentro da sua pasta-raiz** (`cd C:\MeuProjeto`), abra o Claude:
   `claude`
2. (Opcional) digite `/model` e escolha o modelo mais capaz disponível no seu plano —
   a instalação envolve decisões de adaptação à sua profissão.
3. Abra o arquivo [PROMPT-PRONTO.md](PROMPT-PRONTO.md) deste repositório, copie o
   prompt inteiro e cole no Claude.
4. A IA vai: ler o kit → explicar a estrutura → mover os arquivos para os lugares
   certos → **entrevistar você** (nome, profissão, registro profissional, tipos de
   trabalho, fontes de referência) → adaptar a persona e o contrato de fidelidade ao
   seu domínio.

Responda a entrevista com calma — o que você disser ali vira a "personalidade
profissional" permanente da sua IA.

### Instalação manual (alternativa)

Se preferir fazer você mesmo: mova os arquivos de `kit/` para a raiz
(`CLAUDE.md`, `regras-locais.md`, `MEMORY.md`; `ESTADO.md` dentro de `.claude/`;
a ficha-exemplo em `corpus/derived/`), crie a pasta vazia `memory/`, e edite os
placeholders `<...>` de cada arquivo. O papel de cada arquivo está em
[docs/MAPA-ARQUIVOS.md](docs/MAPA-ARQUIVOS.md).

---

## Parte 5 — Verificar que funcionou

Feche o Claude (`/exit`), abra de novo (`claude`) e pergunte:

> "Qual o estado atual do projeto e o próximo passo?"

**Esperado:** a IA responde lendo o `.claude/ESTADO.md` (uma leitura só), sem sair
explorando pastas. Se ela explorar tudo do zero, veja o teste T1 em
[docs/TESTES.md](docs/TESTES.md).

---

## Parte 6 — Rotina de uso (o hábito que faz o sistema funcionar)

- **Ao abrir uma sessão:** a IA lê o `ESTADO.md` e já sabe onde vocês pararam.
- **Ao encerrar um trabalho significativo:** peça — *"atualize o ESTADO.md com o que
  fizemos e o próximo passo"*. É isso que faz a próxima sessão começar quente.
- **Quando a IA errar algo do seu domínio:** corrija e peça — *"registre essa lição
  no ESTADO.md"*. Se o mesmo erro se repetir, peça para promover a regra ao
  `CLAUDE.md` (vira permanente).
- **Quando pesquisar uma fonte importante** (norma, diretriz, lei, jurisprudência):
  peça para destilar numa ficha em `corpus/derived/` — o próximo trabalho cita da
  ficha, não "de memória".
- **Quando a sessão ficar muito longa (ou lenta/cara):** encerrar e recomeçar é
  técnica, não perda. Peça — *"atualize o ESTADO.md com um handoff completo do ponto
  em que estamos"* — feche a sessão e abra uma nova: ela retoma quente lendo só o
  ESTADO.md, sem arrastar o peso da conversa antiga.
- **De vez em quando, faça a faxina:** peça — *"verifique se as lições e memórias
  ainda citam coisas que existem; corrija ou apague as obsoletas"*. Memória velha e
  errada é pior que memória nenhuma.

A regra mais importante de todas está no `CLAUDE.md`: **a IA nunca preenche dado
técnico do seu domínio por plausibilidade** — ou vem de fonte conferida, ou fica
`[a confirmar]`. Errado com confiança é o pior resultado possível para um
profissional.
