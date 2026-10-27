# Marco — Portfólio

Portfólio pessoal de Marco (GitHub: xyz22x, repositório `xyz22x.github.io`) — HTML, CSS e JavaScript puros, sem build.

## Card do Discord

O card de perfil na seção **Contato** é estático, alimentado pela API pública [dstn.to](https://dstn.to) (`dcdn.dstn.to/profile/:id`):

- Avatar e banner (`banner_color` quando não há imagem)
- Nome de exibição e username reais do Discord
- Badges do perfil (`cdn.discordapp.com/badge-icons`)
- Biografia

Testado: responde 200 com CORS aberto (`Access-Control-Allow-Origin: *`), sem chave, sem bot, sem token. A resposta fica em `sessionStorage` por 5 minutos para economizar requisições. Sem presença em tempo real — o card não mostra status online/offline.

### Configuração no `index.html`

```js
const DISCORD_USER_ID = "1310038822612111481";
const DISCORD_BIO = "";
```

`DISCORD_USER_ID` já está preenchido com o ID real da conta. `DISCORD_BIO` é texto manual usado só se a API não entregar bio. Como obter o ID: Discord → Configurações → Avançado → Modo desenvolvedor → botão direito no seu nome → Copiar ID do usuário. O ID é público por natureza; nenhum token é usado.

## Estética

- Fundo `#09090b`, superfícies `#111113` / `#18181b`
- Destaque roxo `#8b5cf6` com moderação
- Tipografia Inter, ícones em SVG inline (sprite `<symbol>`)
- Animações respeitam `prefers-reduced-motion`
