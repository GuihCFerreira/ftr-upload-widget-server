# Upload Widget Server

Backend do projeto Upload Widget da pós-graduação Fullstack da Rocketseat. API para upload de imagens com armazenamento no Cloudflare R2.

## Tecnologias

- **Runtime:** Node.js 22
- **Framework:** Fastify
- **Linguagem:** TypeScript
- **Banco de dados:** PostgreSQL + Drizzle ORM
- **Armazenamento:** Cloudflare R2 (compatível com S3)
- **Validação:** Zod
- **Build:** tsup
- **Testes:** Vitest
- **Linter:** Biome
- **Gerenciador de pacotes:** pnpm

## Endpoints da API

| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/uploads` | Fazer upload de uma imagem |
| GET | `/uploads` | Listar uploads |
| GET | `/uploads/export` | Exportar uploads como CSV |

Documentação da API disponível em `/docs` (Swagger UI).

## Pré-requisitos

- Node.js 22+
- pnpm 10.30+
- PostgreSQL 13+
- Bucket no Cloudflare R2

## Configuração

1. Instale as dependências:

```bash
pnpm install
```

2. Crie um arquivo `.env` com as seguintes variáveis:

```env
PORT=3333
NODE_ENV=development
DATABASE_URL=postgresql://user:password@localhost:5432/upload

CLOUDFLARE_ACCOUNT_ID=
CLOUDFLARE_ACCESS_KEY_ID=
CLOUDFLARE_SECRET_ACCESS_KEY=
CLOUDFLARE_BUCKET=
CLOUDFLARE_PUBLIC_URL=
```

3. Execute as migrations do banco de dados:

```bash
pnpm run db:migrate
```

4. Inicie o servidor de desenvolvimento:

```bash
pnpm run dev
```

O servidor estará rodando em `http://localhost:3333`.

## Scripts

| Script | Descrição |
|--------|-----------|
| `pnpm run dev` | Iniciar servidor de desenvolvimento com hot reload |
| `pnpm run build` | Build para produção |
| `pnpm run test` | Executar testes |
| `pnpm run test:watch` | Executar testes em modo watch |
| `pnpm run db:generate` | Gerar migrations do Drizzle |
| `pnpm run db:migrate` | Executar migrations do banco de dados |
| `pnpm run db:studio` | Abrir Drizzle Studio |

## Estrutura do Projeto

```
src/
├── app/functions/       # Lógica de negócio (casos de uso)
├── infra/
│   ├── db/              # Configuração do banco, schemas e migrations
│   ├── http/            # Servidor Fastify, rotas e plugins
│   └── storage/         # Cliente de armazenamento Cloudflare R2
├── shared/              # Utilitários compartilhados (padrão Either)
├── test/                # Factories de teste
└── env.ts               # Validação de variáveis de ambiente
```
