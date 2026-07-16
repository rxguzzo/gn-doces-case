# Case de Estudo Técnico — ERP G N Doces

Este repositório apresenta o estudo de caso técnico do **G N Doces ERP**, uma solução completa de planejamento de recursos empresariais (ERP) e relacionamento com clientes (CRM) construída sob medida para gerenciar uma doceria artesanal real.

> 🔒 **Nota de Confidencialidade e Segurança:** O código-fonte completo e o banco de dados de produção do sistema permanecem **privados** para proteger a propriedade intelectual, regras de negócio internas e a integridade de dados operacionais e financeiros reais de clientes, parceiros e fornecedores.

---

## 💡 O Problema de Negócio
Microempreendedores e produtores artesanais (como no segmento de confeitaria) lidam diariamente com desafios de:
1. **Precificação dinâmica:** A oscilação dos custos das matérias-primas no mercado dificulta o cálculo exato do custo por receita.
2. **Controle de perdas:** Rastrear o que foi comprado, consumido e o que restou de insumos/produtos acabados.
3. **Fluxo de caixa descentralizado:** Despesas operacionais de compras, receitas de vendas diretas e encomendas parciais dispersas.

---

## 🛠️ A Solução Desenvolvida
Criamos um ecossistema ERP web completo que unifica todas as pontas do negócio em tempo real:

* **🍳 Ficha Técnica e Produção Automatizada:** Mapeamento de receitas e recheios. O lançamento de lotes deduz ingredientes automaticamente e recalcula o custo médio ponderado exato de cada doce pronto.
* **🤖 Importador Inteligente por IA (Gemini OCR):** Upload de cupons fiscais via Foto ou PDF com extração estruturada de itens, quantidades e valores por processamento em nuvem.
* **🔍 Mapeador Fuzzy (Algoritmo Levenshtein):** Associação inteligente entre os itens do cupom fiscal e ingredientes cadastrados usando termos sinônimos (`aliases`) e similaridade de texto.
* **🛒 Frente de Caixa e Encomendas:** Registro rápido de vendas diretas de balcão e encomendas, integrando de forma transacional as baixas no estoque de produto acabado ao fluxo financeiro.
* **💵 Controle Financeiro:** Fluxo de caixa de receitas/despesas com alertas automáticos de insumos próximos ao limite mínimo.

---

## 🧱 Arquitetura Geral e Stack Utilizada

### Stack Tecnológica:
* **Frontend:** React 18, TypeScript, Vite, TailwindCSS, Lucide Icons, Recharts (gráficos).
* **Backend REST API:** Fastify v5 (foco em alta performance, rotas não-bloqueantes e multipart streams).
* **Banco de Dados & ORM:** PostgreSQL hospedado no Supabase + Prisma ORM (modelagem relacional rigorosa).
* **Inteligência Artificial:** SDK Oficial do Google Gemini (`@google/genai`).

### Arquitetura:
```text
docesys/
├── apps/
│   └── crm-api/        # Backend API (Fastify, Prisma, Gemini OCR)
├── src/                # Frontend SPA (React, Vite)
└── portfolio-case/     # estrtura de Estudo de Caso (este repositório)
```

---

## 🌟 Principais Destaques Técnicos

1. **Processamento em Memória (Sem Estado):** Os uploads de Foto/PDF no importador de notas são processados puramente em memória (através de streams multipart do Fastify) e despachados para o Gemini. Nenhuma imagem ou arquivo pessoal de nota é salvo permanentemente no servidor.
2. **Guard Rails Ativos de Banco:** Travas programáticas de segurança acionadas ao inicializar scripts que impedem a execução acidental de sementes (`seeds`), migrações ou testes destrutivos apontados contra a base de produção do Supabase.
3. **Consistência Relacional Pós-Incidente:** Mapeamento transactional ACID no Prisma que garante integridade absoluta das chaves estrangeiras (`FKs`) nas movimentações de estoque vinculadas a lotes.

---

## 📂 Conteúdos do Estudo de Caso
* 📐 [case-study.md](file:///portfolio-case/case-study.md) $\rightarrow$ Estudo de caso aprofundado com desafios técnicos, incidentes de banco e lições de engenharia.
* 📸 [screenshots-guide.md](file:///portfolio-case/screenshots-guide.md) $\rightarrow$ Demonstração visual segura das telas de Dashboard, Estoque, Produção, Gemini OCR e Financeiro.
* 💼 [resume-summary.md](file:///portfolio-case/resume-summary.md) $\rightarrow$ Resumo técnico estruturado para currículos, portfolios e entrevistas.
* 📢 [linkedin-post.md](file:///portfolio-case/linkedin-post.md) $\rightarrow$ Modelos prontos de divulgação profissional.
* 🛡️ [SECURITY.md](file:///portfolio-case/SECURITY.md) $\rightarrow$ Políticas adotadas para garantir segurança e privacidade neste case de estudo.
