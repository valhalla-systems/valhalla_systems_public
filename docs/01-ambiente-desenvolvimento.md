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

## 🗂️ Estrutura de Diretórios do Projeto

```bash
📂Valhalla_Systems/
│
├── 📂backend/                        # Backend da Valhalla Systems
│   ├── 📂geoip/                      # Banco de dados GeoIP
│   │   └── 📄GeoLite2-City.mmdb      # Banco de dados MaxMind GeoLite2
│   │
│   ├── 📂prisma/                     # Definições do banco de dados
│   │   ├── 📂migrations/             # Migrações do banco de dados
│   │   │   ├── 📂20251122145850_create_contact_message_table/   # Migração inicial
│   │   │   │   └── 📄migration.sql    # Script SQL da migração
│   │   │   ├── 📂20251204200554_add_log_entry/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251207150412_add_remote_path_to_verification/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251208145913_add_image_url/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251209115938_add_refresh_token/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251209123334_add_is_admin_field/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251223224853_add_reader_progress/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251224012026_add_reader_content_log/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251225140349_add_reader_phone_fields/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251225142738_add_reader_phone_fields/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251225160125_make_order_number_text/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251228124257_add_reader_password_reset_relation/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20251229121107_replace_password_reset_with_token/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260105134359_add_legal_consent_and_logs/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260106031626_refactor_reader_legal_consent/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260106124131_add_reader_legal_consent/
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260109153007_add_reader_progress_anchor_scroll
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260114102844_add_reader_theme
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260115134106_add_read_status_to_contact_message
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260119035837_add_admin_preferences
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260122121654_add_reader_profile_fields
│   │   │   │   └── 📄migration.sql
│   │   │   ├── 📂20260214202701_20260214_align_reader_relations_and_content_logs
│   │   │   │   └── 📄migration.sql
│   │   │   └── 📄migration_lock.toml  # Lockfile das migrações
│   │   │
│   │   ├── 📄schema.prisma          # Esquema do banco de dados
│   │   ├── 📄seed.contactMessages.ts
│   │   ├── 📄seed.newContact.ts
│   │   └── 📄seed.ts
│   │
│   ├── private/
│   │   └── 📂reader-assets/
│   │       └── 📄mapa_mental.webp
│   │
│   ├── 📂src/
│   │   ├── 📂config/                 # Configurações da aplicação
│   │   │   ├── 📄multer.ts           # Configuração do Multer
│   │   │   └── 📄prisma.ts           # Configuração do cliente Prisma
│   │   │
│   │   ├── 📂controllers/                          # Lógica de controle para cada rota
│   │   │   ├── 📄adminAuth.controller.ts
│   │   │   ├── 📄adminPreferences.controller.ts
│   │   │   ├── 📄adminProfile.controller.ts
│   │   │   ├── 📄adminVerification.controller.ts
│   │   │   ├── 📄contact.controller.ts
│   │   │   ├── 📄contactMessage.controller.ts
│   │   │   ├── 📄download.controller.ts
│   │   │   ├── 📄readerAuth.controller.ts
│   │   │   ├── 📄readerBook.controller.ts
│   │   │   ├── 📄readerContent.controller.ts
│   │   │   ├── 📄readerContentLog.controller.ts
│   │   │   ├── 📄readerContentLogBatch.controller.ts
│   │   │   ├── 📄readerLegalConsent.controller.ts
│   │   │   ├── 📄readerPasswordReset.controller.ts
│   │   │   ├── 📄readerPreferences.controller.ts
│   │   │   ├── 📄readerProfile.controller.ts
│   │   │   ├── 📄readerProgress.controller.ts
│   │   │   ├── 📄readerRegister.controller.ts
│   │   │   ├── 📄verification.controller.ts
│   │   │   └── 📄verificationPublic.controller.ts
│   │   │
│   │   ├── 📂jobs/
│   │   │   └── 📄readerContentLogCleanup.job.ts     # Tarefa de limpeza de logs de leitura
│   │   │
│   │   ├── 📂legal/
│   │   │   └── 📄legalVersions.ts           # Versões legais da aplicação
│   │   │
│   │   ├── 📂lib/                    # Bibliotecas e utilitários compartilhados
│   │   │   ├── 📄forensic.ts            # Módulo de forense
│   │   │   ├── 📄prisma.ts            # Cliente Prisma
│   │   │   └── 📄validators.ts         # Módulo de validadores
│   │   │
│   │   ├── 📂middlewares/               # Middlewares personalizados
│   │   │   ├── 📄auth.middleware.ts
│   │   │   ├── 📄errorHandler.ts        # Middleware de tratamento de erros
│   │   │   ├── 📄ipCapture.ts           # Middleware de captura e normalização de IPs
│   │   │   ├── 📄rateLimiters.ts        # Limitadores de requisições
│   │   │   ├── 📄rateLimitUpload.ts     # Limitador de uploads
│   │   │   ├── 📄requestId.ts           # Middleware de identificação de requisições
│   │   │   ├── 📄securityHeaders.ts     # Middleware de cabeçalhos de segurança
│   │   │   └── 📄uploadVerification.ts  # Middleware de verificação de upload
│   │   │
│   │   ├── 📂modules/                # Módulos da aplicação
│   │   │   └── 📂contact/
│   │   │       ├── 📄contact.dto.ts        # DTOs de contato
│   │   │       ├── 📄contact.schema.ts     # Schemas de validação de contato
│   │   │       └── 📄contact.validator.ts  # Validador de contato
│   │   │
│   │   ├── 📂routes/                          # Definição das rotas da API
│   │   │   ├── 📄admin.routes.ts
│   │   │   ├── 📄adminAuth.routes.ts
│   │   │   ├── 📄adminProfile.routes.ts
│   │   │   ├── 📄adminVerification.routes.ts
│   │   │   ├── 📄contact.routes.ts
│   │   │   ├── 📄contactMessage.routes.ts
│   │   │   ├── 📄readerAssets.routes.ts
│   │   │   ├── 📄readerAuth.routes.ts
│   │   │   ├── 📄readerContent.routes.ts
│   │   │   ├── 📄readerLegal.routes.ts
│   │   │   ├── 📄readerPreferences.routes.ts
│   │   │   ├── 📄readerProfile.routes.ts
│   │   │   ├── 📄readerProgress.routes.ts
│   │   │   ├── 📄readerRegister.routes.ts
│   │   │   ├── 📄testEmail.ts                 # Rota de teste de email (obs.: email não será utilizado por enquanto)
│   │   │   ├── 📄user.routes.ts               # Rota de teste
│   │   │   ├── 📄verification.routes.ts       # Rota de upload de verificação
│   │   │   └── 📄verificationPublic.routes.ts  # Rota de consulta de detalhes de verificação
│   │   │
│   │   ├── 📂scripts/                    # Scripts e ferramentas auxiliares
│   │   │   ├── 📂test-results/
│   │   │   │   └── 📄test-results-2026-02-28T13-51-53.txt
│   │   │   ├── 📂tmp/
│   │   │   │   └── 📄verification_1.jpg
│   │   │   ├── 📂uploads/
│   │   │   │   └── 📂forensic/
│   │   │   ├── 📄create-reader.ts
│   │   │   ├── 📄debug-ip.ts
│   │   │   ├── 📄generate-admin-hash.ts
│   │   │   ├── 📄migrate-imageurl-to-remotepath.ts
│   │   │   ├── 📄run-tests-v2.ts
│   │   │   ├── 📄run-tests.ts
│   │   │   ├── 📄test-admin-1.0.ts
│   │   │   ├── 📄test-admin-auth.ts
│   │   │   ├── 📄test-admin.ts
│   │   │   ├── 📄test-auth.ts
│   │   │   ├── 📄test-cleanup-reader-logs.ts
│   │   │   ├── 📄test-download-hostgator.ts
│   │   │   ├── 📄test-forensic.ts
│   │   │   ├── 📄test-orc.ts
│   │   │   ├── 📄test-resend.ts
│   │   │   ├── 📄test-smtp.ts
│   │   │   ├── 📄test-upload-hostgator.ts
│   │   │   └── 📄validate-book.ts
│   │   │
│   │   ├── 📂services/               # Definições de serviços
│   │   │   ├── 📄access.service.ts    # Serviço de acesso
│   │   │   ├── 📄auth.service.ts      # Serviço de autenticação
│   │   │   ├── 📄book.service.ts      # Serviço de livro
│   │   │   ├── 📄contact.service.ts   # Serviço de contato
│   │   │   ├── 📄fraud.service.ts     # Serviço de fraude
│   │   │   ├── 📄geoip.service.ts     # Serviço de GeoIP
│   │   │   ├── 📄jwt.service.ts       # Serviço de JWT
│   │   │   ├── 📄ocr.service.ts       # Serviço de OCR
│   │   │   ├── 📄password.service.ts  # Serviço de senha
│   │   │   ├── 📄passwordReset.service.ts    # Serviço de reset de senha
│   │   │   ├── 📄readerContentLog.service.ts    # Serviço de log de conteúdo
│   │   │   ├── 📄readerContentLogCleanup.service.ts    # Serviço de limpeza de logs de conteúdo
│   │   │   ├── 📄readerProgress.service.ts   # Serviço de progresso do leitor
│   │   │   ├── 📄sftp.service.ts              # Serviço de upload e download via SFTP
│   │   │   └── 📄upload.service.ts           # Serviço de upload
│   │   │
│   │   ├── 📂shared/                 # Definições de serviços
│   │   │   └── 📄auditLog.ts           # Serviço de log de auditoria
│   │   │
│   │   ├── 📂static/   # Conteúdo Premium
│   │   │   ├── 📂1_capa/
│   │   │   │   ├── 📄page-1.md
│   │   │   │   ├── 📄page-2.md
│   │   │   │   ├── 📄page-3.md
│   │   │   │   └── 📄page-4.md
│   │   │   ├── 📂2_bem_vindo/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂3_apendice_i/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂4_apendice_ii/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-1/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-2/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-3/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-4/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-5/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-6/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-7/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-8/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-9/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-10/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂capitulo-11/
│   │   │   │   └── 📄page-1.md
│   │   │   ├── 📂contra_capa/
│   │   │   │   └── 📄page-1.md
│   │   │   └── 📄index.ts
│   │   │
│   │   ├── 📂types/                  # Tipos personalizados
│   │   │   ├── 📄express.d.ts         # Tipos para o Express
│   │   │   ├── 📄maxmind.d.ts        # Tipos para o MaxMind
│   │   │   └── 📄mime-types.d.ts      # Tipos para o Mime-Type
│   │   │
│   │   ├── 📂utils/                  # Funções auxiliares
│   │   │   ├── 📄amazonPatters.ts    # Funções auxiliares para o Amazon S3
│   │   │   ├── 📄dateUtils.ts         # Funções auxiliares para datas e horários
│   │   │   ├── 📄email.ts            # Função de envio de email
│   │   │   ├── 📄logger.ts           # Função de logging
│   │   │   └── 📄projectRoot.ts       # Função para obter o diretório raiz do projeto
│   │   │
│   │   ├── 📄app.ts                  # Configuração da aplicação Express
│   │   ├── 📄env.ts                  # Configuração das variáveis de ambiente
│   │   └── 📄server.ts               # Ponto de entrada do servidor
│   │
│   ├── 📂tmp/                        # Arquivos temporários
│   │   ├── 📂uploads/
│   │   │   └── 📂avatars
│   │   │       └── 📂processed
│   │   └── 📄verification_1.jpg
│   │
│   ├── 📂uploads/                    # Arquivos de upload
│   │   ├── 📂forensic/               # Arquivos de forense
│   │   │   └── 📄sample-proof.jpg
│   │   │
│   │   ├── 📂ocr/                    # Arquivos de OCR
│   │   ├── 📂verification/          # Arquivos de verificação
│   │   │   └── 📄sample-proof.jpg
│   │   │
│   │   └── 📂uploads_tmp/            # Arquivos temporários de upload
│   │
│   ├── 📄.dockerignore               # Arquivos e pastas a serem ignorados pelo Docker
│   ├── 📄.env                        # Variáveis de ambiente (não versionado)
│   ├── 📄.env.example                # Exemplo de variáveis de ambiente
│   ├── 📄docker-compose.yml          # Configuração do Docker Compose
│   ├── 📄Dockerfile                  # Configuração do Dockerfile
│   ├── 📄package-lock.json           # Lockfile do npm
│   ├── 📄package.json                # Dependências do backend
│   ├── 📄tsconfig.build.json         # Configuração do TypeScript para build
│   └── 📄tsconfig.json               # Configuração do TypeScript
│
│── 📂docs/                           # Documentação do projeto
│   ├── 📄01-ambiente-desenvolvimento.md
│   ├── 📄02-frontend-detalhado.md
│   ├── 📄03-backend-detalhado.md
│   ├── 📄04-infraestrutura-deploy.md
│   └── 📄05-comandos-implantacao.md
│
│── 📂frontend/                       # Frontend da Valhalla Systems
│   ├── 📂public/                     # Arquivos públicos
│   │   ├── 📂images/                 # Imagens públicas
│   │   │   ├── 📄caderno-respostas.webp
│   │   │   ├── 📄capa-react-fullstack.webp
│   │   │   ├── 📄contra-capa.webp
│   │   │   ├── 📄direitos_autorais.webp
│   │   │   ├── 📄hand.png
│   │   │   ├── 📄logo_navbar.png
│   │   │   ├── 📄logo_reader_navbar.png
│   │   │   ├── 📄pagina_interna_one.webp
│   │   │   ├── 📄pagina_interna_two.webp
│   │   │   ├── 📄project_product_store.webp
│   │   │   ├── 📄sublinhado.svg
│   │   │   └── 📄whatsapp.png
│   │   │
│   │   ├── 📄android-chrome-192x192.png
│   │   ├── 📄android-chrome-256x256.png
│   │   ├── 📄apple-icon-57x57.png
│   │   ├── 📄apple-icon-60x60.png
│   │   ├── 📄apple-icon-72x72.png
│   │   ├── 📄apple-icon-76x76.png
│   │   ├── 📄apple-icon-114x114.png
│   │   ├── 📄apple-icon-120x120.png
│   │   ├── 📄apple-icon-144x144.png
│   │   ├── 📄apple-icon-152x152.png
│   │   ├── 📄apple-icon-180x180.png
│   │   ├── 📄favicon-16x16.png
│   │   ├── 📄favicon-32x32.png
│   │   ├── 📄favicon-48x48.png
│   │   ├── 📄favicon-64x64.png
│   │   ├── 📄favicon-128x128.png
│   │   ├── 📄favicon.ico
│   │   ├── 📄logo_50x50.png
│   │   ├── 📄logo_valhalla.png
│   │   ├── 📄manifest.json           # Manifesto do PWA
│   │   ├── 📄mstile-150x150.png
│   │   ├── 📄njord.png
│   │   ├── 📄refresh.js                # Arquivo propositalmente vazio
│   │   └── 📄safari-pinned-tab.svg
│   │
│   ├── 📂src/                        # Código-fonte
│   │   ├── 📂assets/                 # Imagens, ícones, fontes, elementos decorativos
│   │   │   ├── 📂decorations/
│   │   │   │   ├── 📄arrow-1.svg
│   │   │   │   ├── 📄arrow-2.svg
│   │   │   │   ├── 📄arrow-3.svg
│   │   │   │   ├── 📄arrow-4.svg
│   │   │   │   ├── 📄arrow-5.svg
│   │   │   │   └── 📄arrow-6.svg
│   │   │   │
│   │   │   ├── 📂fonts/
│   │   │   ├── 📂icons/
│   │   │   ├── 📂images/
│   │   │   │   ├── 📂hero/
│   │   │   │   ├── 📄hero-1.webp
│   │   │   │   ├── 📄hero-2.webp
│   │   │   │   ├── 📄hero-3.webp
│   │   │   │   ├── 📄hero-4.webp
│   │   │   │   ├── 📄hero-5.webp
│   │   │   │   └── 📄live_long_and_prosper.svg
│   │   │   │
│   │   │   └── 📂sounds/
│   │   │       └── 📄page-flip.mp3
│   │   │
│   │   ├── 📂components/             # Componentes compartilháveis
│   │   │   ├── 📂admin
│   │   │   │   ├── 📄AdminAvatarUpload.tsx
│   │   │   │   ├── 📄AdminNavbar.tsx
│   │   │   │   ├── 📄AdminPasswordForm.tsx
│   │   │   │   ├── 📄AdminProfileForm.tsx
│   │   │   │   ├── 📄AdminProtectedRoute.tsx
│   │   │   │   ├── 📄ContactMessageModal.tsx
│   │   │   │   ├── 📄ContactMessageTable.tsx
│   │   │   │   ├── 📄Pagination.tsx
│   │   │   │   ├── 📄RejectModal.tsx
│   │   │   │   ├── 📄ThemeSelect.tsx
│   │   │   │   └── 📄VerificationTable.tsx
│   │   │   │
│   │   │   ├── 📂common/             # Loader, ScrollToTop, WhatsappButton, etc.
│   │   │   │   ├── 📂Loader/
│   │   │   │   │   └── 📄TriangleLoader.tsx
│   │   │   │   │
│   │   │   │   ├── 📄FloatingButtons.tsx
│   │   │   │   ├── 📄ProtectedRoute.tsx
│   │   │   │   ├── 📄ReaderProtectedRoute.tsx
│   │   │   │   ├── 📄ScrollToTop.tsx
│   │   │   │   └── 📄WhatsappButton.tsx
│   │   │   │
│   │   │   │── 📂debug/              # Componentes para debugging
│   │   │   │   └── 📄ScreenDebug.tsx
│   │   │   │
│   │   │   ├── 📂layout/             # Navbar, Hero, SectionWrapper, etc.
│   │   │   │   ├── 📂Hero/
│   │   │   │   │   ├── 📄defaultDecorations.ts
│   │   │   │   │   ├── 📄HandDrawnDecorations.config.ts
│   │   │   │   │   ├── 📄HandDrawnDecorations.tsx
│   │   │   │   │   └── 📄useHandDrawnDecorations.ts
│   │   │   │   │
│   │   │   │   └── 📂Navbar/         # Navbar e menu animado
│   │   │   │       ├── 📄AnimatedMenuIcon.tsx
│   │   │   │       ├── 📄AuthNavbar.tsx
│   │   │   │       ├── 📄Navbar.tsx
│   │   │   │       └── 📄NavbarMenu.tsx
│   │   │   │
│   │   │   │── 📂markdown/          # Componentes de Markdown
│   │   │   │   └── 📄MarkdownRenderer.tsx
│   │   │   │
│   │   │   ├── 📂reader/
│   │   │   │   ├── 📄BlurOverlay.tsx
│   │   │   │   ├── 📄BookReader.tsx
│   │   │   │   ├── 📄ProtectedImage.tsx
│   │   │   │   ├── 📄ReaderAvatarUpload.tsx
│   │   │   │   ├── 📄ReaderDashboardNavbar.tsx
│   │   │   │   ├── 📄ReaderNavbar.tsx
│   │   │   │   ├── 📄ReaderPasswordForm.tsx
│   │   │   │   ├── 📄ReaderProfileForm.tsx
│   │   │   │   ├── 📄ReaderStatusCard.tsx
│   │   │   │   ├── 📄TableOfContents.tsx
│   │   │   │   ├── 📄UnlockedMaterialList.tsx
│   │   │   │   └── 📄WatermarkLayer.tsx
│   │   │   │
│   │   │   ├── 📂ui/                 # Botões, inputs, wrappers reutilizáveis
│   │   │   │   └── 📄SectionWrapper.tsx
│   │   │   │
│   │   │   └── 📂verification/      # Componentes de verificação
│   │   │       ├── 📄UploadBox.tsx
│   │   │       └── 📄UploadStatus.tsx
│   │   │
│   │   ├── 📂hooks/                  # Custom hooks
│   │   │   ├── 📄useContentHardening.ts
│   │   │   ├── 📄useContentProtection.ts
│   │   │   ├── 📄useIsScrolled.ts
│   │   │   └── 📄useScrollPosition.ts
│   │   │
│   │   ├── 📂layouts/               # Layouts do site
│   │   │   ├── 📄AdminLayout.tsx
│   │   │   ├── 📄LoginLayout.tsx
│   │   │   ├── 📄ReaderLayout.tsx
│   │   │   └── 📄ReaderPortalLayout.tsx
│   │   │
│   │   ├── 📂legal/                  # Páginas legais
│   │   │   ├── 📄LegalModal.tsx
│   │   │   ├── 📄privacy-policy.md
│   │   │   └── 📄terms-of-use.md
│   │   │
│   │   ├── 📂pages/                  # Páginas do site
│   │   │   ├── 📂Admin/
│   │   │   │   ├── 📄AdminDashboard.tsx
│   │   │   │   ├── 📄AdminLogin.tsx
│   │   │   │   ├── 📄AdminProfile.tsx
│   │   │   │   └── 📄AdminVerificationDetails.tsx
│   │   │   │
│   │   │   ├── 📂Home/
│   │   │   │   └── 📄Home.tsx
│   │   │   │
│   │   │   ├── 📂Legal/
│   │   │   │   ├── 📄PrivacyPolicy.tsx
│   │   │   │   └── 📄TermsOfUse.tsx
│   │   │   │
│   │   │   └── 📂Reader/
│   │   │       ├── 📄ReaderContent.tsx
│   │   │       ├── 📄ReaderDashboard.tsx
│   │   │       ├── 📄ReaderLogin.tsx
│   │   │       ├── 📄ReaderProfile.tsx
│   │   │       ├── 📄ReaderRegister.tsx
│   │   │       ├── 📄ReaderResetPassword.tsx
│   │   │       └── 📄ReaderVerificationUpload.tsx
│   │   │
│   │   ├── 📂router/                 # Configuração do React Router
│   │   │       ├── 📄adminRoutes.tsx
│   │   │       ├── 📄index.tsx
│   │   │       ├── 📄readerContentRoute.tsx
│   │   │       └── 📄readerPortalRoutes.tsx
│   │   │
│   │   ├── 📂sections/               # Cada seção do site
│   │   │   ├── 📂About/
│   │   │   │   └── 📄About.tsx
│   │   │   ├── 📂Books/
│   │   │   │   └── 📄Books.tsx
│   │   │   ├── 📂Contact/
│   │   │   │   └── 📄Contact.tsx
│   │   │   ├── 📂Footer/
│   │   │   │   ├── 📄AdminFooter.tsx
│   │   │   │   ├── 📄AuthFooter.tsx
│   │   │   │   └── 📄Footer.tsx
│   │   │   │   └── 📄ReaderDashboardFooter.tsx
│   │   │   ├── 📂Hero/
│   │   │   │   └── 📄Hero.tsx
│   │   │   ├── 📂Portfolio/
│   │   │   │   └── 📄Portfolio.tsx
│   │   │   └── 📂Skills/
│   │   │       └── 📄Skills.tsx
│   │   │
│   │   ├── 📂store/                  # Zustand states
│   │   │       ├── 📄useAdminAuth.ts
│   │   │       ├── 📄useAdminContactMessages.ts
│   │   │       ├── 📄useAdminProfile.ts
│   │   │       ├── 📄useAdminTheme.ts
│   │   │       ├── 📄useAdminVerifications.ts
│   │   │       ├── 📄useGlobalLoader.ts
│   │   │       ├── 📄useReaderAuth.ts
│   │   │       ├── 📄useReaderProfile.ts
│   │   │       └── 📄useReaderTheme.ts
│   │   │
│   │   ├── 📂theme/                  # Tema Chakra customizado
│   │   │   ├── 📂foundations/
│   │   │   │   ├── 📄colors.ts
│   │   │   │   ├── 📄fonts.ts
│   │   │   │   └── 📄styles.ts
│   │   │   ├── 📄adminTheme.ts
│   │   │   ├── 📄index.ts
│   │   │   └── 📄readerTheme.ts
│   │   │
│   │   ├── 📂types/                  # Tipos personalizados
│   │   │   ├── 📄adminProfile.ts
│   │   │   ├── 📄fontsource.d.ts
│   │   │   ├── 📄global.d.ts
│   │   │   ├── 📄images.d.ts
│   │   │   ├── 📄markdown.d.ts
│   │   │   ├── 📄reader.ts
│   │   │   └── 📄readerProfile.ts
│   │   │
│   │   ├── 📂utils/                  # Funções auxiliares
│   │   │   ├── 📄apiAxios.ts
│   │   │   ├── 📄extractToc.ts
│   │   │   ├── 📄motion.ts
│   │   │   └── 📄scrollToSection.ts
│   │   │
│   │   ├── 📄App.tsx                 # Componente raiz
│   │   └── 📄main.tsx                # Ponto de entrada da aplicação
│   │
│   ├── 📄.env                        # Variáveis de ambiente (não versionado)
│   ├── 📄.gitignore                  # Arquivos e pastas a serem ignorados pelo Git
│   ├── 📄.htaccess                   # Configuração do Apache
│   ├── 📄eslint.config.js            # Configuração do ESLint
│   ├── 📄index.html                  # HTML principal
│   ├── 📄package-lock.json           # Lockfile do npm
│   ├── 📄package.json                # Dependências do frontend
│   ├── 📄README.md                   # Documentação do frontend
│   ├── 📄tsconfig.app.json           # Configuração do TypeScript para o frontend
│   ├── 📄tsconfig.json               # Configuração base do TypeScript
│   ├── 📄tsconfig.node.json          # Configuração do TypeScript para Node.js
│   └── 📄vite.config.ts              # Configuração do Vite
│
├── 📄.gitignore                      # Arquivos e pastas a serem ignorados pelo Git
│── 📄LICENSE                         # Licença do projeto
└── 📄README.md                       # Documentação geral do projeto
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
