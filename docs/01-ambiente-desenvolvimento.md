#### 👉 [Voltar ao README principal](../README.md)

# 🧪 Ambiente de Desenvolvimento

Este documento descreve o ambiente técnico utilizado para desenvolvimento do sistema Valhalla Systems, incluindo padrões adotados, ferramentas e práticas.

## 🖥️ Plataforma Local

```bash
|        Item         |     Versão     |
|---------------------|----------------|
| Sistema Operacional | Windows 10 Pro |
| Node.js             | 22.x           |
| npm                 | 11.x           |
| Docker              | 29.x           |
| Git                 | 2.48+          |
| IDE                 | VSCode         |
```

## 📦 Estrutura do Projeto

Monorepo organizado em:

```bash
Valhalla_Systems/
  backend/
  frontend/
  docs/
```

Separação clara entre:

- API (backend)
- SPA (frontend)
- Documentação técnica

### Versionamento e Colaboração

- **Git**: 2.48.1.windows.1
- **GitHub**: Repositório remoto e controle de versão
- **Branch Principal**: `main`

### Testes de API

- **Postman Desktop**: 11.72.9
- **Uso**: Testes manuais das rotas da API REST
- **Coleções**: Configuradas para endpoints de contato e autenticação

### Containerização

- **Docker Desktop**: 29.0.1
- **Docker Compose**: Para orquestração de múltiplos serviços
- **MySQL**: 8.0 via imagem Docker oficial

## 📋 Verificações do Sistema

```bash
# Verificar versões instaladas
node -v
# v22.14.0

npm -v
# 11.6.3

docker --version
# Docker version 29.0.1, build eedd969

git --version
# git version 2.48.1.windows.1
```

---

## ⚙️ Configuração Backend

### Execução Local

```bash
cd backend
npm install
npm run dev
```

Servidor disponível em:

```bash
http://localhost:5000
```

### Banco de Dados Local (Docker)

```bash
docker-compose up -d mysql
```

Porta local:

```bash
localhost:3307
```

Prisma configurado para:

```bash
mysql://root:senha@localhost:3307/db_valhalla
```

### Prisma

Sempre que alterar _schema.prisma_:

```bash
npx prisma generate
```

Migração local:

```bash
npx prisma migrate dev
```

---

## ⚙️ Configuração Frontend

```bash
cd frontend
npm install
npm run dev
```

Disponível em:

```bash
http://localhost:5173
```

Proxy configurado para:

```bash
/api → http://localhost:5000
```

---

## 🔐 Variáveis de Ambiente

### Backend (.env)

```bash
# ARQUIVO: backend/.env

# ============================================
# 🔧 CONFIGURAÇÃO BASE DA API (DEVELOPMENT)
# ============================================
NODE_ENV=development
PORT=5000
API_BASE=http://localhost:5000
# API_URL=https://api.valhallasystems.site


# ============================================
# 🔧 CONFIGURAÇÃO BASE DA API (PRODUCTION)
# ============================================
# NODE_ENV=production
# PORT=5000
# API_BASE=https://valhallasystems.site

# ============================================
# 🗄️ DATABASE (Prisma / MySQL)
# ============================================
DATABASE_URL="mysql://root:<SENHA_DB>@localhost:3306/db_valhalla"

# ============================================
# 🌍 GEOLOCATION (MaxMind)
# ============================================
MAXMIND_DB_PATH=./geoip/GeoLite2-City.mmdb

# ============================================
# ⏱️ RATE LIMIT (GLOBAL)
# ============================================
# Janela em milissegundos
RATE_LIMIT_WINDOW_MS=60000

# Máx. requisições por IP (produção recomendado: 10)
# *** Ativar para Produção ***
RATE_LIMIT_MAX=10
# Apenas para modo Desenvolvimento:
# RATE_LIMIT_MAX=1000

# ============================================
# 🔐 AUTENTICAÇÃO E TOKENS
# ============================================
JWT_SECRET="<MEU_JWT_SECRET>"
JWT_EXPIRES_IN="2d"
REFRESH_TOKEN_DAYS=30
EMAIL_TOKEN_EXPIRATION_MINUTES=60

# ============================================
# 🔎 OCR (OCR.SPACE)
# ============================================
OCRSPACE_API_KEY="MINHA_OCRSPACE_API_KEY"
OCRSPACE_ENDPOINT="https://api.ocr.space/parse/image"

# ============================================
# 📸 UPLOAD LOCAL (fallback / OCR temp files)
# ============================================
UPLOAD_DIR="./uploads/verification"
OCR_RESULTS_DIR="./uploads/ocr"

# ============================================
# 📚 SISTEMA DE LEITORES / ANTI-FRAUDE
# ============================================
# Regex para validação de pedido Amazon
AMAZON_ORDER_REGEX="^[0-9]{3}-[0-9]{7}-[0-9]{7}$"

ANTI_FRAUD_MIN_INTERVAL_SECONDS=60
ANTI_FRAUD_MAX_ATTEMPTS_PER_DAY=5

# ============================================
# 🧪 FORENSE
# ============================================
FORENSIC_SALT="MEU_FORENSIC_SALT"
FORENSIC_STORAGE_PATH=./uploads/forensic
MAX_UPLOAD_SIZE=5242880
OCR_EXTRACT_EMAIL=true

# ============================================
# 🛰️ HOSTGATOR SFTP
# ============================================
HOSTGATOR_SFTP_HOST="valhallasystems.site"
HOSTGATOR_SFTP_PORT=22
HOSTGATOR_SFTP_USER="MEU_HOSTGATOR_SFTP_USER"
HOSTGATOR_SFTP_PASS="MINHA_HOSTGATOR_SFTP_PASS"
HOSTGATOR_UPLOAD_DIR="/home1/<MEU_HOSTGATOR_UPLOAD_DIR>/uploads_secure/verification/"
MAX_UPLOAD_SIZE_BYTES=2000000

# ============================================
# 👑 ADMIN (CONTA DE TESTE / SEED)
# ============================================
ADMIN_TEST_EMAIL=vagner@admin.com
ADMIN_TEST_PASSWORD=<MINHA_SENHA_DE_TESTE>

# ============================================
# 📧 SMTP EMAIL (Nodemailer)
# ============================================
# SMTP_HOST=mail.valhallasystems.site
# SMTP_PORT=465
# SMTP_PORT=587
# SMTP_SECURE=true
# SMTP_SECURE=false
# SMTP_USER=no-reply@valhallasystems.site
# SMTP_PASS=<MINHA_SMTP_PASS>
# MAIL_FROM=Valhalla Systems <no-reply@valhallasystems.site>

# ============================================
# 📧 SMTP EMAIL (Reset de senha via Resend)
# ============================================
RESEND_API_KEY=<MINHA_RESEND_API_KEY>
MAIL_FROM=Valhalla Systems <no-reply@valhallasystems.site>

# ============================================
# 🌐 FRONTEND URL
# ============================================
FRONTEND_URL=https://valhallasystems.site

# ============================================
# 🔑 TOKEN PARA TESTE DE DOWNLOAD (DEIXAR VAZIO)
# Preenchido depois de rodar test-admin-auth
# ============================================
ADMIN_JWT=
```

**_Nunca versionar .env._**

---

## 🧠 Padrões de Desenvolvimento

### TypeScript

- strict mode ativado
- noUncheckedIndexedAccess habilitado
- Sanitização obrigatória de req.params
- Tipos explícitos para middleware

### Segurança

Mesmo em desenvolvimento:

- Helmet ativo
- Rate limiting ativo
- Middleware de autenticação ativo
- Cookies com SameSite=Lax

### Logs

- requestId por requisição
- Logger estruturado
- Logs visíveis no console

---

## 🐳 Docker (Opcional)

Subir ambiente completo:

```bash
docker-compose up
```

Rebuild:

```bash
docker-compose up --build
```

Parar:

```bash
docker-compose down
```

---

## 🧪 Validação Antes de Commit

Checklist:

- [ ] _npm run build_ backend sem erros
- [ ] _npm run build_ frontend sem warnings críticos
- [ ] Prisma generate executado
- [ ] Sem variáveis sensíveis versionadas
- [ ] Sem console.log residual

---

## 🧱 Fluxo de Trabalho Git

```bash
git status
git add .
git commit -m "feat: descrição clara"
git push origin main
```

Push dispara deploy automático no Render.

---

## 📌 Boas Práticas Adotadas

- Separação clara de responsabilidades
- Middleware antes das rotas
- Rate limit antes de auth
- Sanitização de entrada
- Strict typing
- Logs rastreáveis
- Ambiente local isolado do banco de produção

---

## 🎯 Estado Atual do Ambiente

✔ Estável

✔ Compilação limpa

✔ Strict TS sem erros

✔ Docker funcional

✔ Proxy funcionando

✔ Migrações controladas

#### 👉 [Voltar ao README principal](../README.md)
