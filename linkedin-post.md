# Modelos de Postagem para o LinkedIn

Use estes modelos de posts para compartilhar o desenvolvimento e a finalização deste projeto com sua rede profissional.

---

## 📄 Versão 1: Média (Foco em Solução de Negócio e Impacto Real)

```text
🚀 Do caderno ao ERP com IA: Como otimizei a operação da doceria G N Doces!

Desenvolvi um sistema web completo de ERP/CRM para a gestão da G N Doces, um negócio real de doces artesanais. O projeto unifica o controle de estoque, produção de receitas, vendas, agendamento de encomendas e fluxo de caixa financeiro.

Principais Destaques do Projeto:
1. 🍳 Produção Relacional e Custo Médio: O sistema consome insumos do estoque proporcionalmente ao multiplicador da receita e calcula o custo médio unitário dinâmico do produto acabado baseado no histórico de compras.
2. 🤖 Importador de Notas por Foto/PDF com Gemini OCR: Integrando o modelo Gemini 2.5 Flash, o sistema extrai dados estruturados de cupons fiscais e usa algoritmos Levenshtein para associar itens da nota aos ingredientes cadastrados.
3. 🛡️ Guard Rails de Banco: Implementei travas de segurança ativas no backend que detectam strings de conexão de produção locais e evitam qualquer execução acidental de scripts destrutivos.

🛠️ Stack Utilizada:
- Frontend: React 18, Vite, TailwindCSS, Lucide Icons, Recharts (gráficos).
- Backend: REST API em Node.js com Fastify v5 (alta performance e streams de memória) em TypeScript.
- Banco de Dados: PostgreSQL (Supabase) + Prisma ORM.
- IA: Google Gemini Multimodal SDK (@google/genai).

O código-fonte e o banco de dados permanecem privados por se tratar de um negócio real e ativo. Confira o estudo de caso técnico detalhado e os prints das telas no repositório de apresentação: [Link do Repositório do Case]
```

---

## ⚡ Versão 2: Curta (Foco em Agilidade e Resultados)

```text
💡 Como IA e engenharia de software transformaram a gestão da microempresa familiar G N Doces!

Desenvolvi um ERP sob medida que automatiza o controle de estoque, produção, faturamento e encomendas da marca. 

Destaque principal:
- Um importador inteligente de cupons fiscais por Foto/PDF que extrai os dados via Google Gemini 2.5 Flash OCR, combinando com algoritmos Fuzzy Match (Levenshtein) para mapear ingredientes comprados de forma automatizada. 

Tecnologias: React, TypeScript, Fastify, Prisma, PostgreSQL (Supabase).

O case de estudo completo, com os aprendizados sobre segurança de banco e decisões de arquitetura, está documentado publicamente no GitHub: [Link do Repositório do Case]
```

---

## 🛠️ Versão 3: Técnica (Foco em Arquitetura e Engenharia)

```text
💻 Desafio de Engenharia: Construção de um ERP Relacional Integrado com IA (Gemini OCR)

Compartilho o estudo de caso do G N Doces ERP, um software que desenvolvi para gerir a produção de uma doceria artesanal ativa.

Aprendizados e Desafios Superados:
* ⚖️ Consistência Transacional: Lotes de fabricação e cancelamentos usam transações ACID robustas no Prisma ORM para garantir que ingredientes e produtos acabados permaneçam sincronizados sob qualquer falha operacional.
* 📦 Uploads Eficientes em Memória: O backend lê uploads de Foto/PDF por meio de streams do Fastify Multipart, convertendo os buffers direto para despacho ao Gemini API sem tocar no disco rígido.
* 🛡️ DevSecOps & Guard Rails: Após um incidente local que limpou tabelas de teste (rapidamente recuperadas), implementei um script ativo de segurança de banco que bloqueia comandos destrutivos (seeds/limpezas) contra a URL do Supabase de produção.
* 🧠 Fuzzy Match com Confiança: O matcher do importador de notas associa aliases de mercado e faz busca Levenshtein, rebaixando a confiança do item a no máximo 0.50 caso a IA tenha precisado usar fallbacks numéricos.

Stack: React, Vite, Fastify, Prisma, PostgreSQL, SDK Gemini.

O repositório do case público detalha as decisões arquiteturais e guias de segurança do projeto: [Link do Repositório do Case]
```
