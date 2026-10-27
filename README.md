# Marco — Portfólio

Portfólio pessoal de Marco (GitHub: xyz22x, repositório `xyz22x.github.io`) — HTML, CSS e JavaScript puros, sem build.

## Card do Discord

O card de perfil na seção **Contato** combina duas APIs públicas:

- [dstn.to](https://dstn.to) (`dcdn.dstn.to/profile/:id`) — perfil estático: banner, bio, badges. Testado: responde 200 com CORS aberto (`Access-Control-Allow-Origin: *`), sem chave e sem bot.
- [Lanyard](https://github.com/Phineas/lanyard) (`api.lanyard.rest`) — presença em tempo real por WebSocket: status, atividade, Spotify.

A resposta de perfil fica em `sessionStorage` por 5 minutos para economizar requisições.

### 1. Configuração no `index.html`

```js
const DISCORD_USER_ID = "1310038822612111481";
const DISCORD_BIO = "";
```

`DISCORD_USER_ID` já está preenchido com o ID real da conta. `DISCORD_BIO` é texto manual usado só se a API de perfil não entregar bio. Como obter o ID: Discord → Configurações → Avançado → Modo desenvolvedor → botão direito no seu nome → Copiar ID do usuário. O ID é público por natureza; nenhum token é usado.

### 2. Estado monitorado no Lanyard

A conta já está no servidor do Lanyard — `GET https://api.lanyard.rest/v1/users/1310038822612111481` responde `success: true`. Se parar de responder, entre de novo em https://discord.gg/lanyard.

### O que cada API fornece

| Campo | Fonte |
|---|---|
| Banner (imagem) e `banner_color` | dstn.to |
| Avatar | `cdn.discordapp.com` (hash de Lanyard ou dstn.to) |
| Nome de exibição e username | Lanyard; dstn.to como primeiro render |
| Biografia | dstn.to (fallback manual em `DISCORD_BIO`) |
| Badges do perfil | dstn.to (`cdn.discordapp.com/badge-icons`) |
| Presença (online/ausente/não perturbe/offline) | Lanyard, com dot colorido no avatar |
| Status personalizado | Lanyard (`activities[type=4]`) |
| Atividade atual + imagem | Lanyard (`activities`, `spotify`, `cdn.lanyard.net`) |

## Estética

- Fundo `#09090b`, superfícies `#111113` / `#18181b`
- Destaque roxo `#8b5cf6` com moderação
- Tipografia Inter, ícones em SVG inline (sprite `<symbol>`)
- Animações respeitam `prefers-reduced-motion`
