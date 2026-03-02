#### 👉 [Voltar ao README principal](../README.md)

# 💻 Frontend - Especificações Técnicas Detalhadas

O frontend da **Valhalla Systems** é uma SPA (Single Page Application) desenvolvida com **React + Vite + TypeScript**, estruturada para:

- Site institucional
- Área do Leitor (conteúdo premium protegido)
- Painel administrativo
- Sistema de verificação de compra

---

## 🧱 Arquitetura Geral

### Stack Principal

```bash
|    Tecnologia    | Versão |
|------------------|--------|
| React            | 19.x   |
| Vite             | 7.x    |
| TypeScript       | 5.9.x  |
| Chakra UI        | 2.x    |
| Zustand          | 5.x    |
| React Router DOM | 7.x    |
| Framer Motion    | 12.x   |
```

---

## 📁 Organização por Domínio

O frontend é organizado por domínio funcional:

```bash
src/
  components/
    admin/
    reader/
  pages/
    Admin/
    Reader/
  store/
  hooks/
  utils/
```

Separação clara entre:

- Interface Admin
- Interface Reader
- Componentes institucionais
- Estado global
- Camada de API

---

## 🔐 Sistema de Autenticação

### Leitor

- Login via /api/reader/auth/login
- Refresh token via /api/reader/auth/refresh
- Cookie HTTPOnly (produção)
- Token também retornado para uso controlado

### Admin

- Token armazenado em localStorage (escopo administrativo)
- Headers Authorization: Bearer

---

## 📚 Área do Leitor (Conteúdo Premium)

### Fluxo de Acesso

1. Usuário cria conta
2. Envia comprovante
3. Admin aprova
4. Backend libera acesso
5. Frontend consulta /api/reader/content/access
6. Conteúdo desbloqueado

### Proteção de Conteúdo

#### 1️⃣ Imagens protegidas

Não são arquivos públicos.

São carregadas via:

```bash
/api/reader/assets/:assetId
```

Proteções aplicadas:

- ID opaco (anti-enumeração)
- Autenticação obrigatória
- Cache-control privado
- Nosniff
- Inline disposition

#### 2️⃣ Hardening visual

- Blur opcional
- Pointer-events controlado
- Max-height controlado
- Bloqueio de clique direito (UI-level)
- Render via blob

#### 3️⃣ Gating completo

Sem verificação aprovada:

```bash
403 Access denied
```

---

## 📖 Sistema de Leitura

### Estrutura

- Índice de capítulos
- Páginas dinâmicas
- Anchors internas
- Scroll controlado
- Continuidade de leitura

### Persistência

Backend salva:

- chapterId
- page
- anchor
- scrollY

Frontend restaura posição automaticamente.

---

## 👑 Painel Administrativo

### Funcionalidades

- Listagem de verificações
- Aprovação
- Rejeição com motivo
- Download de comprovante
- Logs agregados (OCR / Forense / Fraude / Sistema)

### Segurança Admin

- Autenticação isolada
- Rate limit dedicado
- CSP restritivo
- Anti-iframe
- HTTPS obrigatório

---

## 🎨 Design System

Baseado em Chakra UI com:

- Tokens customizados
- Tema Admin separado
- Tema Reader separado
- Responsividade completa
- Layout com overflow controlado
- Tabelas com scroll horizontal mobile

---

## 🧠 Gerenciamento de Estado

Zustand utilizado para:

- Tema Admin
- Estado de autenticação
- Verificações pendentes
- Preferências do leitor

Sem Redux. Sem Context excessivo.

---

## 🔄 Comunicação com API

### Axios customizado

Arquivo central:

```bash
utils/apiAxios.ts
```

Características:

- BaseURL dinâmica
- Interceptadores
- Tratamento de 401
- Retry controlado
- Header Authorization automático

---

## 🔐 Segurança no Frontend

- CSP compatível com Vite
- Strict HTTPS
- Sem exposição de secrets
- Validação antes de enviar para backend
- Nenhuma lógica sensível no cliente

---

## ⚡ Performance

- Build target ES2015
- Chunk size controlado
- SVG como componente
- Lazy loading onde aplicável
- Scroll restoration otimizada

---

## 🧪 Scripts

```bash
{
"dev": "vite",
"build": "tsc -b && vite build",
"preview": "vite preview",
"lint": "eslint ."
}
```

---

## 📦 Build de Produção

```bash
npm run build
```

Output:

```bash
frontend/dist/
```

Arquivos enviados manualmente para Hostgator.

---

## 📌 Estado Atual do Frontend

✔ Área institucional funcional

✔ Área do leitor protegida

✔ Painel admin completo

✔ Proteção de assets ativa

✔ Persistência de leitura

✔ HTTPS enforced

✔ CSP ativo

✔ Anti-clickjacking ativo

#### 👉 [Voltar ao README principal](../README.md)
