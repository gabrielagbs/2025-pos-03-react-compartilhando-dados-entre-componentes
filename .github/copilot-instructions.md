# Instruções para agentes de codificação

Objetivo curto: tornar um agente imediatamente produtivo neste repositório Next.js + TypeScript + Tailwind.

- Projeto: app Next.js (App Router) com `src/app` como entrada. Versão `next@15.x` (ver `package.json`).
- Linguagem: TypeScript. Alias de import: `@/*` mapeia para `./src/*` (veja `tsconfig.json`).

Visão geral (big picture)
- Estrutura principal: `src/app` contém o layout global (`layout.tsx`) e a página principal (`page.tsx`).
- Componentes reutilizáveis ficam em `src/componentes` (ex.: `Cabecalho.tsx`).
- Dados estáticos/fixtures ficam em `src/data/index.ts` (exporta `TarefaInterface` e a lista de tarefas usada pela UI).
- Estilos globais: `src/app/globals.css` + Tailwind (configuração já presente). Fonts via `next/font` no `layout.tsx`.

Padrões e convenções específicas do projeto
- Arquivos e símbolos em Português (ex.: `Cabecalho`, `Tarefa`) — siga os nomes existentes quando possível.
- Uso de Tailwind utilities diretamente em JSX (ex.: `className="p-3 mb-3 rounded-lg shadow-md"`).
- Componentes de UI pequenos e compostos — exemplo: `Cabecalho` reúne `Titulo` e `SubTitulo` em `src/componentes/Cabecalho.tsx`.
- Data flow: páginas importam os dados diretamente de `@/data` e passam como props para componentes (padrão de fixtures estáticos, não API).
- Client components: quando há estado local use a diretiva `"use client"` no topo de arquivos (ex.: `src/app/page.tsx`).

Fluxo de desenvolvimento e comandos úteis
- Instalação (escolha de gerenciador de pacotes): `npm install` (project contém `pnpm` config, `pnpm install` também funciona se desejar). 
- Desenvolvimento: `npm run dev` (executa `next dev --turbopack`).
- Build/Start: `npm run build` e `npm run start`.
- Lint: `npm run lint` (usa `eslint-config-next`).

Pontos importantes e armadilhas observadas
- Verifique import paths com alias `@/` — `tsconfig.json` define `@/* -> ./src/*`.
- Há um possível typo no import em `src/app/page.tsx`: `import Cabecalho from "@/componentes/Cabecalhot"` (o arquivo real é `Cabecalho.tsx`). Busque por imports incorretos antes de rodar a build.
- `src/data/index.ts` é a fonte de verdade para o exemplo de tarefas; alterações aqui mudam todo o comportamento visual das listas.

Exemplos rápidos (what to change / where)
- Para adicionar uma nova UI: criar componente em `src/componentes/` e exportar default.
- Para alterar dados de exemplo: editar `src/data/index.ts` ou substituir por fetch/endpoint se for transformar em app dinâmico.
- Para estilos globais: editar `src/app/globals.css` ou adicionar classes Tailwind diretamente nos componentes.

Como um agente deve operar aqui (prática)
1. Sempre rodar `npm install` e `npm run dev` localmente para validar mudanças.
2. Antes de renomear ou mover arquivos, procurar por imports com `@/` (grep por `@/componentes` etc.).
3. Mantener componente pequeno e sem lógica de roteamento — `src/app` controla layout/rotas.
4. Ao alterar tipagens, atualizar `TarefaInterface` em `src/data/index.ts` para manter consistência.

Quando pedir verificação ao usuário
- Mudanças que renomeiam arquivos (p.ex. corrigir o `Cabecalhot` -> `Cabecalho`) devem ser aprovadas.
- Substituir dados estáticos por chamadas reais a APIs precisa de confirmação (escopo de aula).

Links rápidos para referência no repositório
- `src/app/layout.tsx` (fonts + globals)
- `src/app/page.tsx` (página principal, `use client`, exemplos de `Tarefa`/`Tarefas`)
- `src/componentes/Cabecalho.tsx` (composição de header)
- `src/data/index.ts` (tipo `TarefaInterface` e fixtures)
- `package.json` (scripts e dependências)

Se algo estiver ambíguo: pergunte ao autor/professor antes de mudanças de ampla superfície (renomear arquivos, alterar estrutura de imports, trocar a estratégia de dados).

Fim.
