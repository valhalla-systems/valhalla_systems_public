#### 👉 [Voltar ao README principal](../README.md)

# ⚡ Backend - Especificações Técnicas Detalhadas

O backend da Valhalla Systems é uma API RESTful desenvolvida em:

- Node.js
- Express 5
- TypeScript strict
- Prisma ORM
- MySQL

Arquitetado para suportar:

- Sistema institucional
- Área do Leitor (premium)
- Painel Admin
- Verificação de compra
- Proteção de assets
- Logs e auditoria
- Segurança em produção

---

## 🧱 Arquitetura Geral

### Estrutura por Camadas

```bash
controllers/
services/
routes/
middlewares/
utils/
lib/
jobs/
```

Separação clara:

- Controller → HTTP layer
- Service → regra de negócio
- Prisma → acesso a dados
- Middleware → segurança / rate limit / auth

---

## 🗃️ Banco de Dados (Prisma + MySQL)

### Provider

```bash
provider = "mysql"
```

### Principais Entidades

- Reader
- Admin
- Verification
- ReaderAsset
- ReaderProgress
- ReaderContentLog
- PasswordResetToken
- RefreshToken
- ContactMessage

---

## 🔐 Autenticação

### Reader

- Signup
- Login
- Refresh token rotativo
- Logout
- Session endpoint
- Reset de senha com token criptografado
- Política de senha forte

Tokens:

- Access token (curta duração)
- Refresh token (rotativo, invalidável)

Cookies:

- HTTPOnly
- Secure (produção)
- SameSite controlado

### Admin

- Login isolado
- Rate limit dedicado
- Token Bearer
- Escopo administrativo separado do Reader

---

## 📚 Sistema de Verificação de Compra

Fluxo:

1. Reader envia comprovante
2. Registro em Verification
3. OCR / Forense / Logs
4. Admin aprova ou rejeita
5. Reader passa a ter acesso premium

Status possíveis:

- PENDING
- APPROVED
- REJECTED

---

## 📖 Gating de Conteúdo Premium

Antes de qualquer conteúdo:

```bash
readerHasApprovedVerification(readerId)
```

Sem aprovação:

```bash
403 Access denied
```

---

🖼️ Assets Protegidos

Endpoint:

```bash
GET /api/reader/assets/:assetId
```

Proteções:

- ID opaco (anti-enumeração)
- Sanitização regex
- Autenticação obrigatória
- Verificação de ownership
- Cache-Control privado
- X-Content-Type-Options: nosniff
- Content-Disposition inline

Arquivos armazenados fora de pasta pública.

---

## 📊 Sistema de Logs

### 1️⃣ Request ID

Cada requisição recebe:

```bash
X-Request-Id
```

Permite rastreamento completo.

### 2️⃣ Logger estruturado

- Inclui:
- requestId
- IP
- rota
- userId (se autenticado)
- nível (info/warn/error/debug)

### 3️⃣ Logs de Conteúdo

ReaderContentLog:

- page view
- timestamps
- batch cleanup job automático

---

## 🔒 Segurança HTTP

### Helmet configurado com:

- CSP customizado
- frame-ancestors 'none'
- X-Frame-Options DENY
- noSniff
- Referrer-Policy
- Permissions-Policy

### HTTPS Enforcement

- Redirect HTTP → HTTPS
- HSTS ativo
- includeSubDomains
- Sem preload (fase estável inicial)

### Rate Limiting Segmentado

```bash
|       Escopo        |     Tipo      |
|---------------------|---------------|
| /api/reader/auth    | Auth limiter  |
| /api/admin/auth     | Auth limiter  |
| /api/admin          | Admin limiter |
| /api/reader/content | Soft limiter  |
```

Sem rate limit genérico no /api inteiro.

---

## 🔁 Refresh Token Rotativo

Ao usar refresh:

- Novo token é gerado
- Antigo é invalidado
- Se reutilizado → revogado

Protege contra replay.

---

## 🔐 Reset de Senha

- Token criptografado SHA-256
- Expiração 30 minutos
- Token single-use
- Invalida todos refresh tokens após reset

---

## 📡 Middlewares Globais

Ordem aplicada:

1. trust proxy
2. securityHeaders
3. CORS
4. express.json
5. cookieParser
6. rate limiters
7. requestId
8. captureIp
9. rotas
10. errorHandler

Ordem crítica para segurança.

---

## 🧠 Controle de IP

- request-ip
- GeoIP via MaxMind
- Dados armazenados na tabela ContactMessage

---

## 🛡️ Hardening Implementado

- Anti-clickjacking
- Anti-sniff
- CSP restritivo
- Headers redundantes defensivos
- Sanitização de req.params
- Strict TypeScript
- No any implícito
- noUncheckedIndexedAccess ativo

---

## ⚙️ TypeScript

Configuração:

- strict: true
- noUncheckedIndexedAccess: true
- strictNullChecks
- Tipos explícitos em middleware

---

## 🔄 Deploy (Render)

Build:

```bash
npm install
npx prisma generate
npm run build
```

Start:

```bash
node dist/server.js
```

---

## 📌 Estado Atual do Backend

✔ Autenticação segura

✔ Refresh rotativo

✔ Reset seguro

✔ Gating premium ativo

✔ Assets protegidos

✔ HTTPS enforced

✔ HSTS ativo

✔ Anti-iframe

✔ Logs rastreáveis

✔ Rate limit segmentado

✔ Strict TS sem erros

#### 👉 [Voltar ao README principal](../README.md)
