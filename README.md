# DoaFácil — Plataforma Comunitária de Gestão de Doações

Repositório da disciplina **Prática Extensionista IV**.

**Autor:** Gabriel Zocolotto ([@zott12](https://github.com/zott12))

<p align="justify">
<strong>Introdução</strong>: Instituições comunitárias — bancos de alimentos, ONGs, associações de bairro e paróquias — dependem de doações para atender famílias em situação de vulnerabilidade, mas normalmente controlam campanhas, itens recebidos e entregas em planilhas, cadernos e grupos de mensagens. Isso dificulta saber o que está faltando, prestar contas aos doadores e evitar desperdício. <strong>Objetivo</strong>: desenvolver o <em>DoaFácil</em>, uma aplicação web que conecta doadores às instituições da comunidade, permitindo que a instituição publique campanhas com os itens necessários, que o doador registre sua doação e agende a entrega, e que ambos acompanhem o status até o recebimento, com relatórios de transparência. <strong>Metodologia</strong>: levantamento de requisitos com a instituição parceira, desenvolvimento incremental com práticas DevOps (integração e entrega contínuas com GitHub Actions) e publicação em nuvem Microsoft Azure. <strong>Resultados esperados</strong>: redução do tempo de organização das campanhas, maior engajamento de doadores e prestação de contas pública das doações recebidas.
</p>

<strong>Palavras-chave</strong>: Doações. Extensão universitária. Aplicação web. DevOps. Computação em nuvem.

---

## Funcionalidades (escopo)

- Cadastro e login de doadores e instituições (JWT, perfis `DOADOR`, `INSTITUICAO`, `ADMIN`)
- Criação e divulgação de campanhas de arrecadação com itens e metas
- Registro de doações e agendamento de entrega/coleta
- Painel da instituição com acompanhamento do status das doações
- Relatórios de transparência e notificações por e-mail

## Tecnologias

| Camada | Tecnologia |
|---|---|
| Frontend | React 18, Vite, React Router, Axios |
| Backend | Node.js 20, Express, Prisma ORM, Zod, JWT |
| Banco de dados | PostgreSQL 16 |
| DevOps | Git/GitHub, GitHub Actions, Dependabot, SonarCloud |
| Nuvem | Microsoft Azure (Static Web Apps, App Service, PostgreSQL Flexible Server, Blob Storage, Key Vault, Application Insights) |

## Documentação e diagramas

| Artefato | Arquivo |
|---|---|
| Diagrama UML de pacotes (arquitetura da aplicação) | [doc/diagramas/pacotes.png](doc/diagramas/pacotes.png) · [SVG](doc/diagramas/pacotes.svg) |
| Diagrama de implantação | [doc/diagramas/implantacao.png](doc/diagramas/implantacao.png) · [SVG](doc/diagramas/implantacao.svg) |
| Diagrama de arquitetura DevOps | [doc/diagramas/devops.png](doc/diagramas/devops.png) · [SVG](doc/diagramas/devops.svg) |
| Arquitetura (descrição) | [doc/arquitetura.md](doc/arquitetura.md) |
| Infraestrutura de deploy, justificativa e custos | [doc/infraestrutura.md](doc/infraestrutura.md) |

### Diagrama de pacotes
![Diagrama de pacotes](doc/diagramas/pacotes.png)

### Diagrama de implantação
![Diagrama de implantação](doc/diagramas/implantacao.png)

### Diagrama DevOps
![Diagrama DevOps](doc/diagramas/devops.png)

## Estrutura do repositório

```
.
├── .github/
│   ├── workflows/ci.yml        # integração contínua (lint, testes, build)
│   ├── workflows/cd.yml        # entrega contínua (staging → aprovação → produção)
│   └── dependabot.yml
├── app/
│   ├── frontend/               # SPA React + Vite
│   │   └── src/{routes,pages,components,contexts,services,utils}
│   └── backend/                # API REST Node.js + Express
│       ├── prisma/schema.prisma
│       └── src/{routes,middlewares,controllers,services,integrations,repositories,config}
└── doc/
    ├── diagramas/              # PNG + SVG dos diagramas
    ├── arquitetura.md
    └── infraestrutura.md
```

## Como executar localmente

```bash
# Backend
cd app/backend
cp .env.example .env          # ajuste DATABASE_URL e JWT_SECRET
npm install
npx prisma migrate dev
npm run dev                   # http://localhost:8080/api/health

# Frontend (outro terminal)
cd app/frontend
cp .env.example .env
npm install
npm run dev                   # http://localhost:5173
```

## Fluxo de trabalho (Git)

- `main` → produção (protegida, merge somente via Pull Request aprovado e CI verde)
- `develop` → homologação
- `feature/<nome>` → novas funcionalidades
- Commits no padrão *Conventional Commits* (`feat:`, `fix:`, `docs:` …)
