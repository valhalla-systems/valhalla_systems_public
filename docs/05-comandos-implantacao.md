#### 👉 [Voltar ao README principal](../README.md)

# 🎯 Comandos de Implantação - Referência Oficial

Este documento consolida os comandos utilizados no ciclo de desenvolvimento e deploy do sistema Valhalla Systems.

## 🚀 Desenvolvimento Local

### 🔹 Backend

```bash
cd backend
npm install
npm run dev
```

Servidor:

```bash
http://localhost:5000
```

### 🔹 Frontend

```bash
cd frontend
npm install
npm run dev
```

Servidor:

```bash
http://localhost:5173
```

---

## 🗃️ Banco de Dados (Prisma)

### Gerar cliente Prisma

Sempre após alterar _schema.prisma_:

```bash
npx prisma generate
```

### Criar migração local

```bash
npx prisma migrate dev --name nome_da_migracao
```

### Executar migrações em produção

```bash
npx prisma migrate deploy
```

### Sincronizar schema sem migração (uso controlado)

```bash
npx prisma db push
```

### Abrir Prisma Studio

```bash
npx prisma studio
```

---

## 🐳 Docker (Ambiente Local Opcional)

Subir MySQL local:

```bash
docker-compose up -d mysql
```

Subir tudo:

```bash
docker-compose up
```

Parar:

```bash
docker-compose down
```

---

## 📦 Build de Produção

### Backend

```bash
cd backend
npm run build
npm start
```

Ou (modo completo):

```bash
npm run build && node dist/server.js
```

### Frontend

```bash
cd frontend
npm run build
```

Arquivos gerados em:

```bash
frontend/dist/
```

Devem ser enviados manualmente para:

```bash
public_html/
```

---

## ☁️ Deploy Backend (Render)

Fluxo real:

```bash
git add .
git commit -m "deploy: descrição objetiva"
git push origin main
```

Render executa automaticamente:

```bash
npm install
npx prisma generate
npm run build
node dist/server.js
```

---

## 🔍 Verificações Pós-Deploy

### Backend

- Testar endpoint /
- Testar /api/reader/auth/session
- Testar rota protegida
- Validar headers HTTPS

### Frontend

- Testar /reader/login
- Testar /admin
- Confirmar SPA fallback
- Confirmar ausência de mixed content

---

## 🔐 Segurança - Checklist Antes de Produção

- [ ] npm run build backend sem erros
- [ ] npm run build frontend sem erros
- [ ] Prisma generate executado
- [ ] Sem .env versionado
- [ ] HTTPS funcionando
- [ ] HSTS ativo
- [ ] CSP ativo
- [ ] Rate limit funcionando

---

## ⚡ Comandos Rápidos

### Desenvolvimento completo

```bash
docker-compose up -d mysql
cd backend && npm run dev
cd frontend && npm run dev
```

### Deploy rápido

```bash
git add .
git commit -m "deploy"
git push origin main
```

---

## 📝 Notas Importantes

1. Sempre execute npx prisma generate após alterar schema.prisma
2. Use npm ci em produção para instalação limpa
3. Build do frontend deve ser feito antes do upload para Hostgator
4. Variáveis de ambiente devem ser configuradas no Render e no .env local

---

## 📌 Estado Atual do Sistema

✔ Backend compilando sem erros

✔ Frontend build estável

✔ Prisma sincronizado

✔ HTTPS enforced

✔ HSTS ativo

✔ Proteção de conteúdo ativa

✔ Autenticação segura

✔ Logs rastreáveis

#### 👉 [Voltar ao README principal](../README.md)
