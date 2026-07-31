# apex-system-architecture
Showcase e arquitetura técnica do SaaS Apex System — Plataforma Multi-Tenant de Gestão Educacional Global.

# 🎓 Apex System — SaaS Multi-Tenant de Gestão Educacional Global

> **Nota de Propriedade:** Este é um repositório de apresentação técnica (*Showcase/Portfolio*). O código-fonte principal é mantido em um repositório privado proprietário.

![Apex System Banner](https://via.placeholder.com/1200x400?text=Apex+System+SaaS+Global)

[![Next.js](https://img.shields.io/badge/Next.js-14-black?style=for-the-badge&logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20.x-green?style=for-the-badge&logo=node.js)](https://nodejs.org/)
[![Prisma](https://img.shields.io/badge/Prisma-ORM-2D3748?style=for-the-badge&logo=prisma)](https://www.prisma.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue?style=for-the-badge&logo=postgresql)](https://www.postgresql.org/)

---

## 📌 Visão Geral do Produto

O **Apex System** é uma plataforma SaaS White-Label e Multi-Tenant projetada para simplificar a gestão operacional, financeira e pedagógica de escolas de idiomas, tutores independentes, mentores e instrutores particulares no mercado global.

O sistema elimina a dependência de planilhas e softwares genéricos pesados, entregando uma solução enxuta com visões adaptativas por perfil (Super Admin, Gestor Escolar, Professor e Aluno).

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
- **Portfólio:** [Link para do sistema/demo] em desenvolvimento.
- **E-mail:** brunodsc.trabalho@gmail.com
