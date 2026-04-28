# ⏱ RiRavel Daily Stand-up

Timer de daily standup feito sob medida pro time RiRavel. Roda como painel flutuante por cima do Jira via bookmarklet — sem instalação, sem extensão, sem servidor.

## Features

- **Shuffle** — embaralha a ordem dos participantes a cada daily
- **Skip/Undo** — pule quem não vai participar (Bruna e Ivan skippados por padrão)
- **Timer configurável** — de 00:30 a 10:00 por pessoa, default 02:00
- **Drag & drop** — reordene manualmente antes de iniciar
- **Som** — tick nos últimos 10s + alerta quando o tempo acaba (mutável)
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

Arraste o botão **⏱ Standup** pra barra de favoritos do browser.

### 4. Use

1. Abra o **Jira** no board do RiRavel
2. Clique em **⏱ Standup** nos favoritos
3. O painel aparece no canto esquerdo
4. Arraste a barra do topo pra mover
5. **−** minimiza · **×** fecha · clique de novo = toggle

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
    img: "https://...",     // URL da foto (Atlassian avatar)
    sd: true,               // (opcional) skippado por padrão
    role: "PM"              // (opcional) cargo exibido quando skippado
  },
  // ...
];
```

### Editar tempo padrão

No mesmo arquivo, altere `DEFAULT_DUR`:

```javascript
const MIN = 30, MAX = 600, STEP = 30, DEFAULT_DUR = 120; // em segundos
```

## Quick Filters do Jira

O projeto inclui Quick Filters configurados no board do RiRavel pra mostrar tasks + reviews por pessoa na daily. Cada filtro usa:

```
assignee = {USER_ID} OR Reviewer = {USER_ID} OR "Reviewer 2" = {USER_ID}
```

## Stack

HTML + CSS + vanilla JS. Zero dependências, zero build, zero backend.

## License

MIT
