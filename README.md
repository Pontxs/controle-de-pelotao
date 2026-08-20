# 🪖 Controle de Pelotão

Aplicativo web para gerenciamento operacional diário de um pelotão, desenvolvido como projeto pessoal por um oficial do Exército Brasileiro cursando Engenharia de Software.

HTML CSS JavaScript PWA localStorage

## Sobre o projeto

Um progressive web app (PWA) construído para substituir planilhas de Excel no controle diário de um pelotão de fuzileiros do Exército Brasileiro. O objetivo foi criar uma ferramenta leve, com capacidade offline, que se instala como um app mobile, sem dependência de servidor, banco de dados ou framework externo.

O projeto inteiro vive em um único arquivo HTML, o que facilita a distribuição e o uso em ambientes com conectividade limitada.

**Aviso de privacidade:** o app não tem backend, todos os dados inseridos ficam apenas no localStorage do dispositivo do usuário e nunca são enviados a nenhum servidor. Os dados de exemplo incluídos no código são fictícios, gerados apenas para demonstrar a interface.

## Funcionalidades

| Módulo | Descrição |
| --- | --- |
| Dashboard | KPIs em tempo real, atrasos acumulados, dispensas médicas, punições e fatos observados do mês. Rankings automáticos por categoria. |
| Cadastro de Militares | Registro completo dos militares com dados funcionais e de perfil. |
| Atrasos | Registro de ocorrências com contagem por soldado. |
| Punições | Registro formal com tipo, período e autoridade que aplicou. |
| Dispensas Médicas | Acompanhamento de idas ao médico e afastamentos, com ou sem dispensa do serviço. |
| Fatos Observados | Fatos positivos (FO+) e negativos (FO−) para avaliação de desempenho. |
| Aniversários | Calendário do pelotão organizado por mês, com contagem regressiva para o próximo. |

## Stack

O projeto foi construído intencionalmente sem frameworks para reforçar os fundamentos de desenvolvimento web:

- **HTML semântico:** estrutura SPA com múltiplas "páginas" via `display: none / block`
- **CSS puro:** custom properties, grid responsivo, tema militar dark
- **JavaScript vanilla:** manipulação de DOM, métodos de array (`.map()`, `.filter()`, `.reduce()`), template literals
- **localStorage:** persistência de sessão sem backend
- **PWA:** manifest, service worker e cache offline gerados inline via `Blob` + `URL.createObjectURL()`
- **Mobile-first:** navegação por bottom nav bar, inputs com `font-size: 16px` para evitar zoom no iOS

## Arquitetura

O app segue um padrão simples e deliberado de dados → renderização → ação:

```
Estado (arrays em memória)
    ↓  salvo em
localStorage
    ↓  lido por
renderX()  →  injeta HTML via innerHTML
    ↑
addX() / rm()  ←  eventos do usuário (onclick)
```

Não há two-way binding, virtual DOM ou gerenciamento de estado externo. Cada mudança de dado chama diretamente a função de render correspondente.

## Como usar

### Opção 1: direto no navegador

```bash
# Clona o repositório
git clone https://github.com/Pontxs/controle-de-pelotao.git

# Abre o arquivo
open index.html
```

### Opção 2: deploy como PWA (recomendado)

1. Sobe o `index.html` em qualquer host estático (Netlify, GitHub Pages, Vercel)
2. Acessa pelo celular
3. Android: o Chrome mostra banner automático de instalação
4. iOS: Safari, Compartilhar, "Adicionar à Tela de Início"

Depois de instalado, funciona offline e os dados ficam no localStorage do dispositivo.

## Estrutura do arquivo

```
index.html
├── <head>
│   ├── Meta tags PWA (viewport, theme-color, apple-mobile-web-app)
│   └── Google Fonts (Rajdhani, IBM Plex Mono, Inter)
│
├── <style>          CSS completo (~200 linhas)
│   ├── Variáveis de cor (:root)
│   ├── Layout (header, bottom-nav, main)
│   ├── Componentes (card, form-grid, table, badge, toast)
│   └── Responsividade (@media max-width: 480px)
│
├── <main>           7 páginas como divs
│   ├── #page-dash   Dashboard com KPIs e rankings
│   ├── #page-cad    Cadastro de militares
│   ├── #page-at     Atrasos
│   ├── #page-pun    Punições
│   ├── #page-disp   Dispensas médicas e idas ao médico
│   ├── #page-dest   Fatos observados (FO+ / FO−)
│   └── #page-aniv   Aniversários
│
├── <nav>            Bottom navigation bar (7 botões)
│
└── <script>         Lógica completa (~300 linhas)
    ├── Dados padrão (arrays seed, fictícios)
    ├── Funções de persistência (ld / sv / svAll)
    ├── Helpers (fmt, daysUntil, nextId, toast)
    ├── Navegação (showPage, showTab)
    ├── Renders (renderDash, renderCad, renderAt...)
    ├── Ações (addCad, addAt, addPun, addDisp, addFO, rm)
    └── Setup PWA (manifest, service worker, banner de instalação)
```

## Decisões de projeto

**Por que arquivo único?** O app precisa funcionar em ambientes militares com conectividade instável. Um único arquivo HTML é trivial de compartilhar via WhatsApp, pen drive ou QR code, sem processo de instalação e sem dependência de npm.

**Por que sem framework?** O projeto também serve como exercício prático de fundamentos de JS e DOM, junto com a graduação em Engenharia de Software. Frameworks seriam camada desnecessária de abstração para esse escopo.

**Por que localStorage em vez de banco de dados?** Infraestrutura zero. O app é para uso pessoal do comandante de pelotão, não há necessidade de sincronização entre múltiplos usuários. Para um cenário multiusuário, o próximo passo natural seria substituir o localStorage por chamadas a uma API REST apoiada em SQLite ou PostgreSQL.

## Autor

**Bruno Pontes da Rosa**

Oficial do Exército Brasileiro

Engenharia de Software (PUCRS)

GitHub

Construído para uso operacional real. Os dados seed incluídos no repositório são fictícios e servem apenas para demonstrar a interface.
