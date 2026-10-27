# xyz22.github.io

Portfólio pessoal de xyz22 — HTML, CSS e JavaScript puros, sem build.

## Configurar o card do Discord (Lanyard)

O card de perfil na seção **Contato** sincroniza a presença do Discord em tempo real pelo [Lanyard](https://github.com/Phineas/lanyard).

### 1. Definir o ID numérico da conta

Em `index.html`, dentro da tag `<script>` no fim do arquivo:

```js
const DISCORD_USER_ID = "";
```

Substitua por seu ID numérico do Discord, entre aspas:

```js
const DISCORD_USER_ID = "94490510688792576";
```

Como obter o ID: Discord → Configurações → Avançado → ativar **Modo desenvolvedor** → clique com o botão direito no seu nome de usuário → **Copiar ID do usuário**.

O ID é público por natureza (aparece em qualquer perfil), então não é segredo — não há problema em deixá-lo no código de um site estático. Nenhum token ou credencial é usado ou necessário.

Enquanto o ID estiver vazio, o card exibe o estado manual: nome, `@2024.s`, avatar de letra e o indicador "indisponível", e o botão copia o identificador `2024.s`.

### 2. Ativar o monitoramento no Lanyard

O Lanyard só expõe a presença de contas **presentes no servidor oficial dele**:

1. Entre em https://discord.gg/lanyard
2. Confirme em `https://api.lanyard.rest/v1/users/SEU_ID` — se responder `{"success":true,"data":{...}}`, o monitoramento está ativo
3. Resposta `404` significa que a conta não está monitorada: entre no servidor e teste de novo

### 3. Como verificar a integração

- Pill verde **"tempo real"** no card = WebSocket conectado e recebendo `PRESENCE_UPDATE`
- Linha **"atualizado às hh:mm:ss"** = última presença recebida
- Pill **"indisponível"** = sem conexão com o serviço ou conta não monitorada

### O que a integração fornece e o que não fornece

| Campo | Fonte |
|---|---|
| Nome de exibição e username | Lanyard (`discord_user`) |
| Avatar | `cdn.discordapp.com` a partir do hash do Lanyard |
| Presença (online/ausente/não perturbe/offline) | Lanyard |
| Status personalizado | Lanyard (`activities[type=4]`) |
| Atividade atual + imagem | Lanyard (`activities`, `spotify`, `cdn.lanyard.net`) |
| Banner | Não existe no payload do Lanyard — fallback visual em CSS |
| Biografia | Não existe no payload do Lanyard — texto manual no HTML |

## Estética

- Fundo `#09090b`, superfícies `#111113` / `#18181b`
- Destaque roxo `#8b5cf6` com moderação
- Tipografia Inter, ícones em SVG inline (sprite `<symbol>`)
- Animações respeitam `prefers-reduced-motion`
