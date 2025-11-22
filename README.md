# Sistema de Rastreamento GTX

Aplicação Next.js focada apenas em **tela de login** e **área logada** conforme o roadmap técnico atualizado (itens 11 a 20). O projeto reutiliza a mesma paleta e logo da Agência GTX, integra-se ao Supabase já utilizado no `gtx-landing` e define todo o modelo de dados no Prisma.

## Stack

- Next.js 14 (App Router) + TypeScript
- Tailwind CSS com a paleta verde padrão da agência
- Supabase Auth para login (mesmas variáveis `NEXT_PUBLIC_SUPABASE_URL/NEXT_PUBLIC_SUPABASE_ANON_KEY`)
- Prisma + PostgreSQL (use o banco do Supabase ou outro Postgres compatível)

## Estrutura rápida

```
app/
  login/         → Tela de login com formulário conectado ao Supabase
  dashboard/     → Área logada com todos os módulos do roadmap (relatórios, alertas etc.)
components/      → Logo, cards e formulários reutilizáveis
lib/             → Clientes do Supabase (browser/server) e Prisma
prisma/schema    → Modelo completo das tabelas novas
```

## Variáveis de ambiente

Copie `.env.example` para `.env.local` e reutilize as mesmas credenciais do Supabase já usadas em `gtx-landing`:

```bash
NEXT_PUBLIC_SUPABASE_URL=...
NEXT_PUBLIC_SUPABASE_ANON_KEY=...
SUPABASE_SERVICE_ROLE_KEY=...
DATABASE_URL=postgresql://.../postgres?schema=public
DIRECT_URL=postgresql://.../postgres?schema=public
```

## Scripts úteis

| Script | Descrição |
| --- | --- |
| `npm run dev` | Ambiente de desenvolvimento |
| `npm run build` | Build de produção |
| `npm run lint` | ESLint |
| `npm run prisma:generate` | Gera o client do Prisma |
| `npm run db:reset` | **Derruba todas as tabelas e recria com base no schema atual** |

> Use `npm run db:reset` (que roda `prisma migrate reset --force`) para atender ao pedido de “deletar todas as tabelas existentes e recriar tudo baseado nesse projeto”. Isso derruba o schema público e o reconstrói usando os modelos definidos em `prisma/schema.prisma`.

## Login e área logada

- `/login`: segue a identidade visual da landing oficial, com cartão translúcido e suporte ao Supabase Auth. Também oferece link direto para `https://app.agenciagtx.com.br` caso o usuário já esteja autenticado.
- `/dashboard`: consolida todos os módulos extras do roadmap (relatórios customizados, notificações proativas, Academy, permissões, auditoria, testes A/B, preditivo, webhooks e inbox unificado). Os dados exibidos são mocks definidos em `data/dashboard.ts` para demonstrar o layout.

## Próximos passos sugeridos

1. Instalar dependências (`npm install`).
2. Importar as credenciais do Supabase iguais às do `gtx-landing`.
3. Rodar `npm run db:reset` para limpar o schema antigo e subir todas as tabelas novas.
4. Ajustar os componentes para consumir dados reais do Prisma/Supabase conforme as integrações forem liberadas.

Tudo foi construído com foco em clareza (fundo branco) e evitando o visual futurista, mantendo uma experiência consistente com a marca GTX.
