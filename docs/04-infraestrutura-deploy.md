#### 👉 [Voltar ao README principal](../README.md)

# ⚙ Infraestrutura e Deploy

## 🏗️ Arquitetura de Produção

O sistema Valhalla Systems opera com arquitetura distribuída:

```bash
|    Camada      |          Serviço             |
|----------------|------------------------------|
| Frontend       | Hostgator (build estático)   |
| Backend        | Render (Web Service Node.js) |
| Banco de Dados | MySQL Hostgator              |
| SSL            | HTTPS obrigatório            |
| API Base       | Render                       |
```

Separação clara entre:

- Camada estática (SPA)
- Camada de API autenticada
- Banco isolado

---

## 🌐 Domínios

### Produção

Frontend:

[https://valhallasystems.site](https://valhallasystems.site)

Backend:

[https://valhalla-systems.onrender.com](https://valhalla-systems.onrender.com)

API Base:

[https://valhalla-systems.onrender.com/api](https://valhalla-systems.onrender.com/api)

---

## 🔒 HTTPS Enforcement

### Hostgator (.htaccess)

Configuração aplicada:

- Força HTTPS
- Remove www
- SPA fallback apenas para domínio correto
- Não intercepta arquivos reais
- Não intercepta /avatars/
- HSTS ativo
- CSP ativo

**Regras principais**

- Redirect HTTP → HTTPS
- _frame-ancestors 'none'_
- Strict-Transport-Security
- Content-Security-Policy
- Permissions-Policy

---

## 🛡️ Hardening de Segurança

### Backend (Helmet)

Headers aplicados:

- Content-Security-Policy
- X-Frame-Options: DENY
- X-Content-Type-Options
- Referrer-Policy
- Permissions-Policy
- HSTS

### Cookies

Produção:

- HttpOnly
- Secure
- SameSite=None
- Domínio controlado
- Somente trafegam via HTTPS.

---

## 🐳 Ambiente Docker (Desenvolvimento)

**Dockerfile**

- Multi-stage build
- Node 22-alpine
- Prisma generate no build
- Dist separado
- Runtime mínimo

### Docker Compose (Dev)

Serviços:

- mysql:8.0
- api (nodemon + tsx)

Portas:

- 3307 → MySQL
- 5000 → API

Healthcheck configurado.

---

## ☁️ Render - Backend

### Configuração

```bash
|     Campo      |                      Valor                          |
|----------------|-----------------------------------------------------|
| Root Directory | backend                                             |
| Build Command  | npm install && npx prisma generate && npm run build |
| Start Command  | node dist/server.js                                 |
| Node Version   | 22.x                                                |
```

### Variáveis de Ambiente

- DATABASE_URL
- NODE_ENV=production
- MAXMIND_DB_PATH
- RATE_LIMIT configs
- SMTP configs (opcional)

### Build Pipeline

1. npm install
2. prisma generate
3. tsc
4. node dist/server.js

Strict TS validado no build.

---

## 🗃️ Banco de Dados

### MySQL Hostgator

- Porta 3306
- Charset utf8mb4
- UTC no banco
- Conversão apenas na exibição

Migrações:

```bash
npx prisma migrate deploy
```

---

## 📦 Frontend Deploy

### Processo

1. _npm run build_
2. Upload manual de frontend/dist/
3. Validação de headers via DevTools

---

## 🔄 Fluxo Completo de Deploy

### Backend

```bash
git add .
git commit -m "deploy"
git push origin main
```

Render executa build automático.

### Frontend

```bash
npm run build
```

Upload manual para Hostgator.

---

## 📊 Monitoramento

### Render

- Logs em tempo real
- Métricas básicas
- Healthcheck

### Hostgator

- Access logs
- Error logs
- SSL ativo

---

## ⚠️ Considerações Importantes

### Render Free Tier

- Sleep após inatividade
- Cold start inicial

### Segurança Consolidada

✔ HTTPS obrigatório

✔ Cookies seguros

✔ CSP ativa

✔ HSTS ativo

✔ Rate limit segmentado

✔ Param sanitization

✔ Anti-clickjacking

---

## 🎯 Estado da Infraestrutura

✔ Estável

✔ Produção funcional

✔ Ambiente local isolado

✔ Hardening aplicado

✔ Deploy automatizado backend

#### 👉 [Voltar ao README principal](../README.md)
