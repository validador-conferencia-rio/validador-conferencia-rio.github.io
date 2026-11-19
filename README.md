# Validador de Ingressos

Check-in por QR code com sincronização em tempo real entre vários celulares (Firebase Realtime Database), hospedado no GitHub Pages.

- A base de participantes **não fica no GitHub**: o admin carrega o Excel pelo app e ela vai para o Firebase, protegida por login.
- Cada entrada é gravada por **transação**: se dois aparelhos lerem o mesmo QR ao mesmo tempo, só um libera e o outro mostra "JÁ ENTROU".
- Se a internet cair, o aparelho continua validando pelo cache local e sincroniza quando voltar (o indicador fica vermelho).

## 1. Firebase (5 min, plano gratuito)

1. https://console.firebase.google.com → **Adicionar projeto** (pode desativar o Analytics).
2. **Build → Realtime Database → Criar banco de dados** → local `us-central1` → modo bloqueado.
3. Aba **Regras** → cole o conteúdo de `database.rules.json` (troque `admin@validador.app` pelo e-mail admin) → Publicar.
4. **Build → Authentication → Começar → E-mail/senha → Ativar**.
5. Aba **Users → Adicionar usuário**: crie o admin (ex.: `admin@validador.app`) e um login da equipe (ex.: `portaria@evento.com`).
6. **Configurações do projeto (engrenagem) → Seus apps → Web (</>)** → registre o app → copie o `firebaseConfig`.
7. Cole o `firebaseConfig` e o `adminEmail` em `config.js`.
8. Authentication → **Settings → Domínios autorizados** → adicione `SEU_USUARIO.github.io`.

## 2. GitHub Pages

1. Crie um repositório (ex.: `validador`) e suba todos os arquivos desta pasta.
2. **Settings → Pages → Source: Deploy from a branch → main / root** → Save.
3. Endereço: `https://SEU_USUARIO.github.io/validador/`

## 3. No dia

- Admin entra, aba **Admin**, carrega o Excel do Sympla.
- Equipe entra com o login da portaria e um nome por aparelho (ex.: "Portaria 2 - Ana").
- Aba **Entradas** mostra tudo em tempo real e exporta CSV.

Sem `config.js` preenchido o app roda em **modo demo** (sincroniza só entre abas do mesmo navegador).
