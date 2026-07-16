# Resumo para Currículo e Entrevistas (G N Doces ERP)

Use este material para enriquecer seu currículo, atualizar as descrições de cargo no LinkedIn ou guiar sua fala em entrevistas técnicas.

---

## 📄 1. Tópicos para Currículo (Bullet Points)

* **Desenvolvimento de ERP/CRM Completo:** Projetou e implementou um sistema integrado de controle de estoque, produção de lotes de receitas, gerenciamento de encomendas e conciliação financeira para microempresa de doces artesanais, utilizando **React**, **Fastify**, **TypeScript** e **PostgreSQL**.
* **Integração de Inteligência Artificial:** Desenvolveu um importador inteligente de cupons fiscais via **Foto/PDF** utilizando a API do **Google Gemini 2.5 Flash**, reduzindo o tempo de entrada de notas fiscais de 15 minutos para menos de 30 segundos.
* **Algoritmos de Fuzzy Matching:** Implementou algoritmo de similaridade **Levenshtein** acoplado a regras de sinônimos (`aliases`) para mapear descrições cruas de notas fiscais de fornecedores com os insumos de estoque cadastrados.
* **Segurança e DevSecOps:** Criou um script de *Guard Rails* programático ativo que bloqueia a execução acidental de seeds, migrações ou limpezas de banco de dados locais contra a base Supabase de produção.
* **Transações ACID:** Garantiu a consistência e integridade das movimentações de estoque e custo médio de insumos por meio de transações isoladas no **Prisma ORM**.

---

## 💼 2. Descrição de Projetos no LinkedIn (Projects/Experience)

**Título do Projeto:** Sistema ERP Integrado com IA & Digitalização de Compras (G N Doces)
**Tecnologias:** React, Fastify, TypeScript, Prisma ORM, PostgreSQL (Supabase), Gemini AI SDK.

**Descrição:**
Desenvolvimento de um sistema ERP completo sob medida para a gestão operacional e financeira de uma confeitaria artesanal real. O sistema integra todas as pontas da produção e vendas:
* **Módulo Financeiro:** Fluxo de caixa transacional integrado a compras de estoque e recebimentos parciais ou totais de encomendas.
* **Módulo de Lotes:** Fichas técnicas de receitas com baixa automática e proporcional de insumos do estoque e cálculo preciso do custo médio ponderado.
* **IA Multimodal (Gemini OCR):** Digitalização automática de notas fiscais por Foto/PDF com extração estruturada de dados.
* **Segurança de Dados:** Travas e políticas ativas contra deleções acidentais em ambiente de produção.

---

## 🗣️ 3. Roteiro de Entrevista Técnica (Elevator Pitch)

> *"Desenvolvi um ERP de ponta a ponta para a doceria G N Doces. O principal objetivo era substituir processos em cadernos e planilhas e dar visibilidade sobre o custo real das receitas. A stack que escolhi foi React com Vite, Fastify (pela alta performance) em TypeScript, e Prisma ORM com PostgreSQL hospedado na Supabase.*
> 
> *Os maiores destaques do projeto foram:*
> 1. *O **Cálculo de Custo Médio Unitário Ponderado**, recalculado automaticamente a cada entrada de compra e associado proporcionalmente ao consumo de ingredientes nas receitas.*
> 2. *O **Importador Inteligente com Gemini OCR**, onde o usuário faz o upload de uma Foto ou PDF da nota fiscal e a IA extrai a estrutura do cupom. Combinei isso com algoritmo de similaridade Levenshtein para sugerir o ingrediente correto correspondente no estoque.*
> 3. *Um **sistema de Guard Rails** que implementei no backend após sofrer um incidente real de deleção local. O guard rail analisa se a string de conexão ativa aponta para produção e bloqueia limpezas ou migrações indevidas.*
> 
> *O projeto gerou um impacto enorme, reduzindo o tempo de lançamento de notas de compras em $95\%$ e dando clareza exata das margens de lucro dos produtos do negócio."*
