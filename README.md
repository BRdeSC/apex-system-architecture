# 🎓 Apex System — SaaS Multi-Tenant de Gestão Educacional Global

> **Nota de Propriedade:** Este é um repositório de apresentação técnica (*Showcase / Architecture Portfolio*). O código-fonte principal é mantido em um repositório privado proprietário.

![Apex System Banner](https://via.placeholder.com/1200x400?text=Apex+System+SaaS+Global)

[![Next.js](https://img.shields.io/badge/Next.js-14-black?style=for-the-badge&logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20.x-green?style=for-the-badge&logo=node.js)](https://nodejs.org/)
[![Prisma](https://img.shields.io/badge/Prisma-ORM-2D3748?style=for-the-badge&logo=prisma)](https://www.prisma.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue?style=for-the-badge&logo=postgresql)](https://www.postgresql.org/)

---

## 📌 Visão Geral do Produto

O **Apex System** é uma plataforma SaaS White-Label e Multi-Tenant projetada para simplificar a gestão operacional, financeira e pedagógica de escolas de idiomas, tutores independentes, mentores e instrutores particulares no mercado global.

O sistema elimina a dependência de planilhas e softwares genéricos pesados, entregando uma solução enxuta com visões adaptativas por perfil (**Super Admin, Gestor Escolar, Professor e Aluno**).

---

## 🌟 Principais Destaques de Engenharia & Arquitetura

- **🏢 Arquitetura Multi-Tenant com Isolamento Estrito (Tenant Isolation):** Garantia de isolamento de dados por escola (`schoolId`) em nível de banco e middleware, impedindo vazamento de dados (*cross-tenant data leakage*).
- **🌍 Internacionalização Global (i18n) & DDI Dinâmico:** Suporte nativo a múltiplos idiomas (Português, Inglês, Espanhol, Francês e Alemão) com tradução dinâmica e formatação de telefonia internacional no padrão **E.164**.
- **🔒 Segurança & Conformidade (Pentest Compliant):**
  - Autenticação JWT com cookies de sessão seguros (`HttpOnly`, `SameSite`, `Secure`).
  - Controle de Acesso Baseado em Funções (**RBAC**).
  - Validação rigorosa de dados de entrada no servidor via **Zod/Joi** contra injeções XSS e SQL.
- **📈 Inteligência Financeira e Métricas SaaS:** Dashboards executivos com cálculo e projeção de faturamento recorrente (MRR), inadimplência e adoção de planos.
- **🚀 Programa de Indicação Integrado (MGM - Member Get Member):** Sistema gamificado de cupons e descontos progressivos na mensalidade do SaaS para retenção e crescimento orgânico.

---

## 🚀 Inventário Completo de Funcionalidades & Módulos

### 🛡️ 1. Painel Super Admin (Gestão SaaS Global)
**Acesso:** Usuários com a role `SUPER_ADMIN` (Isolamento global, sem vinculação a `schoolId`).

#### 📊 Visão Geral & Telemetria Global (`/superadmin`, `/superadmin/dashboard`)
- **Métricas de MRR Consolidado:** Exibição do faturamento recorrente mensal ativo com atualização em tempo real.
- **Histórico de Faturamento Recorrente:** Gráfico interativo com a evolução do faturamento dos últimos 12 meses (garantindo meses únicos e ordenados sem estouro de datas).
- **Indicadores Globais:** Contagem total de Escolas Parceiras, Alunos Ativos no SaaS e Faturamento Histórico Total acumulado.
- **Gráfico de Adoção de Planos:** Visualização comparativa do percentual de retenção nos planos `FREE`, `PRO_MENSAL`, `PRO_SEMESTRAL` e `PRO_ANUAL`.

#### 🏢 Gestão de Escolas Parceiras (`/superadmin/escolas`)
- **Tabela de Escolas:** Exibição completa com nome, e-mail do responsável, telefone com DDI internacional, plano SaaS, alunos matriculados vs. limite contratado, data de cadastro e status (`Ativa` / `Suspensa`).
- **Filtros Avançados:** Busca por nome de escola, status, plano SaaS e filtro exclusivo por **País de Origem** (padrão ISO 3166-1 alpha-2 com bandeiras nativas 🇧🇷, 🇺🇸, 🇨🇦, 🇪🇸, 🇵🇹, 🇫🇷, 🇩🇪, 🇬🇧, 🇮🇪, 🇦🇺).
- **Cadastro de Nova Escola Parceira:** Modal transacional (Escola + Usuário Administrador de Unidade) com validação de e-mail único, país de residência e telefone formatado em E.164.
- **Edição & Gestão de Status:** Atualização de dados da escola e bloqueio/liberação imediata do acesso da unidade.

#### 💳 Gestão de Planos SaaS (`/superadmin/planos`)
- **Configuração de Limites & Preços:** Definição dinâmica do nome do plano, subtítulo, valor da assinatura, limite de alunos e lista de vantagens (checkmarks).
- **Tradução Automática de Planos:** Nomes, subtítulos e vantagens traduzidos em tempo real para o idioma ativo do usuário (`pt`, `en`, `es`, `fr`, `de`).

#### 🏷️ Programa de Indicações & Cupons (`/superadmin/cupons`)
- **Gestão MGM (Member-Get-Member):** Visualização de indicações entre escolas e monitoramento de códigos promocionais ativos com desconto concedido (ex: 5%).

#### 📜 Auditoria, Logs & Configurações Globais (`/superadmin/logs`, `/superadmin/configuracoes`)
- **Logs de Eventos Globais:** Auditoria contendo data/hora, tipo de ação, IP e payload sanitizado.
- **Parametrização da Plataforma:** Alteração do Nome do Sistema, Slogan/Subtítulo Oficial na Landing Page, E-mail e Telefone de Suporte Global.

---

### 🏢 2. Painel do Gestor Escolar (Admin da Unidade)
**Acesso:** Usuários com a role `TENANT_ADMIN` (Isolamento por `schoolId`).

#### 📈 Dashboard Operacional & Telemetria (`/admin/dashboard`)
- **Projeção de Faturamento & Métricas:** Cálculo do faturamento acumulado, total de alunos ativos e taxa de frequência dos últimos 30 dias.
- **Gráficos de Desempenho:** Histórico de faturamento (com modal de zoom) e matriz de demanda por faixa de horário (16 faixas das 07h às 23h50).
- **Alertas de Retenção & Evasão:** Ranking dos alunos mais frequentes vs. alunos em risco de evasão (*churn*) para ação pedagógica preventiva.

#### 👨‍🎓 Gestão de Alunos & Equipe Docente (`/professor/alunos`, `/professor/equipe`)
- **Gestão de Alunos:** Filtro por nível (A1 ao C2), tipo de plano (`RECORRENTE` ou `AVULSO`) e histórico pedagógico individual (**Diário Pedagógico / `PedagogicalNote`**).
- **Gestão da Equipe Docente:** Registro de instrutores da escola com especificação de especialidades (ex: Business English, Conversação, IELTS).

#### 📅 Grade, Agendamentos & Faturamento (`/professor/agenda`, `/professor/faturamento`)
- **Criação de Turmas (`ClassSlot`):** Agendamento de aulas com tópico, professor, limite de alunos, cor temática e link do **Google Meet**.
- **Programa MGM da Unidade:** Código de indicação único da escola que concede **5% de desconto cumulativo** na mensalidade do SaaS a cada nova indicação convertida.

#### ⚙️ Regras, White-Label & PDFs (`/professor/configuracoes`)
- **Políticas de Agendamento (`BookingPolicy`):** Configuração de *Acesso Livre*, *Créditos* ou *Horário Fixo*, limite diário de reservas (`maxDailyBookings`) e tolerância a atrasos.
- **Customização da Marca (White-Label):** Alteração do Nome da Unidade, Logotipo e Cor Primária do Tema.
- **Biblioteca Didática:** Upload e gestão de livros pedagógicos em PDF.

---

### 👨‍🏫 3. Painel do Professor (Teacher View)
**Acesso:** Usuários com a role `TEACHER`.

- **Agenda & Chamada em Tempo Real:** Grade diária/semanal com botão de presença/falta individual e link de 1 clique para o **Google Meet**.
- **Apontamentos Pedagógicos:** Lançamento de notas de aula e feedbacks diretos no perfil do estudante.
- **Consulta a Materiais:** Leitura online da biblioteca de livros didáticos em PDF da escola.

---

### 🎓 4. Portal do Aluno (Student View)
**Acesso:** Usuários com a role `STUDENT`.

- **Dashboard do Aluno:** Nível de proficiência atual e resumo das próximas aulas.
- **Agendamento Interativo:** Calendário filtrado pelo nível do aluno, reserva com 1 clique (com validação de `maxDailyBookings`) e cancelamento dentro das regras de tolerância.
- **Acompanhamento & Desempenho:** Histórico de presenças e consulta a feedbacks deixados pelos professores.
- **Biblioteca Digital & Anotações (`MaterialAnnotation`):** Leitor de PDFs integrado com funcionalidade de salvar anotações de estudo por página do livro.

---

## 📸 Demonstração do Sistema

### 1. Landing Page Internacional & Seleção de Idioma (i18n)
*Interface pública adaptável com precificação regional por paridade de poder de compra.*
![Landing Page Showcase](https://via.placeholder.com/800x450?text=Landing+Page+Demo)

### 2. Painel do Gestor Escolar (Dashboard Operacional & Financeiro)
*Gestão centralizada de turmas, alunos, professores e visão histórica de faturamento.*
![Dashboard Manager Showcase](https://via.placeholder.com/800x450?text=Manager+Dashboard+Demo)

### 3. Painel Super Admin (Visão do Fundador do SaaS)
*Gestão global de clientes parceiros, planos de assinatura, cupons de desconto e métricas consolidadas.*
![Super Admin Showcase](https://via.placeholder.com/800x450?text=Super+Admin+Demo)

---

## 🛠️ Stack Tecnológica

### Frontend
- **Framework:** Next.js 14 (App Router)
- **Linguagem:** TypeScript
- **Estilização:** Tailwind CSS, Lucide Icons, Shadcn UI
- **Internacionalização:** Context API / i18n Engine Dinâmico
- **Visualização de Dados:** Recharts

### Backend & Banco de Dados
- **Runtime:** Node.js (Express / Fastify Architecture)
- **ORM:** Prisma ORM
- **Banco de Dados:** PostgreSQL
- **Autenticação:** JSON Web Tokens (JWT) + Bcrypt Encryption
- **Validação de Schemas:** Zod

---

## 📊 Diagrama de Entidades (ERD)

```
[ SuperAdmin ] <--- gerencia ---> [ SaasPlan ]
       |
       v
  [ School ] <--- possui ---> [ User (Manager, Teacher, Student) ]
       |                                   |
       +--- possui ---> [ ClassSchedule ] -+
       +--- possui ---> [ Material ]
       +--- possui ---> [ Invoice ]
```


---

## ✉️ Contato & Redes Profissionais

Desenvolvido por **Bruno** — *Full-Stack Developer*
- **LinkedIn:** https://www.linkedin.com/in/bruno-ti/
- **Portfólio:** System Demo (Em desenvolvimento)
- **E-mail:** brunodsc.trabalho@gmail.com
