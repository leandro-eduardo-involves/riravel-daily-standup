# ⏱ RiRavel Daily Stand-up

Timer de daily stand-up feito sob medida pro time RiRavel. Roda como painel flutuante por cima do Jira via bookmarklet — sem instalação, sem extensão, sem servidor.

## Features

- **Shuffle** — embaralha a ordem dos participantes a cada daily
- **Skip/Undo** — pule quem não vai participar (Bruna e Ivan skippados por padrão)
- **Timer configurável** — de 00:30 a 10:00 por pessoa, default 02:00
- **Drag & drop** — reordene manualmente antes de iniciar
- **Som** — tick nos últimos 10s + alerta quando o tempo acaba (mutável)
- **Quick Filters automáticos** — ao iniciar o turno de cada membro, aplica o Quick Filter correspondente no Jira automaticamente
- **Dark/Light mode** — toggle com preferência salva no localStorage
- **Fotos do Jira** — avatares do Atlassian direto nos cards
- **Bookmarklet** — abre como sidebar flutuante sobre o Jira, arrastável e redimensionável

## Setup

### 1. Clone o repo

```bash
git clone https://github.com/leandro-eduardo-involves/riravel-daily-standup.git
```

### 2. Ative o GitHub Pages

Settings → Pages → Source: **Deploy from a branch** → Branch: **main** → Save

### 3. Configure o bookmarklet

Acesse: `https://leandro-eduardo-involves.github.io/riravel-daily-standup/setup.html`

Arraste o botão **Stand-up** pra barra de favoritos do browser.

### 4. Use

1. Abra o **Jira** no board do RiRavel
2. Clique em **Stand-up** nos favoritos
3. O painel aparece no canto esquerdo
4. **×** fecha · clique de novo no bookmark pra reabrir

## Quick Filters

Ao clicar em **Start**, o timer aplica automaticamente o Quick Filter do membro atual no board do Jira. Ao avançar com **Next**, desmarca o anterior e marca o próximo. Ao finalizar ou resetar, limpa todos os filtros.

Para funcionar, o board do Jira precisa ter Quick Filters configurados com os nomes dos membros. Cada filtro usa:

```
assignee = {USER_ID} OR Reviewer = {USER_ID} OR "Reviewer 2" = {USER_ID}
```

Se os filtros não forem encontrados ao iniciar, o timer exibe um aviso.

## Estrutura

```
├── index.html    # Timer (standalone + iframe)
├── setup.html    # Página de setup do bookmarklet
└── README.md
```

## Customização

### Editar membros do time

No `index.html`, edite o array `T` no início do `<script>`:

```javascript
const T = [
  {
    n: "Nome Completo",     // nome exibido
    i: "NC",                // iniciais (fallback sem foto)
    c: "#3A7BE8",           // cor do avatar
    qf: 1220,              // ID do Quick Filter no Jira
    img: "https://...",     // URL da foto (Atlassian avatar)
    sd: true                // (opcional) skippado por padrão
  },
  // ...
];
```

### Editar tempo padrão

No mesmo arquivo, altere as constantes:

```javascript
const MIN = 30, MAX = 600, STEP = 30; // em segundos
let dur = 120; // default 02:00
```

### Board URL

Atualize a URL do board se necessário:

```javascript
const BOARD_URL = "https://involves.atlassian.net/jira/software/c/projects/RIR/boards/413";
```

## Stack

HTML + CSS + vanilla JS. Zero dependências, zero build, zero backend.

## License

MIT
