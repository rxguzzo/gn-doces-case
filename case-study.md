# Estudo de Caso — ERP G N Doces

Este documento detalha o desenvolvimento do G N Doces ERP, abordando as decisões técnicas, desafios enfrentados, gerenciamento de incidentes reais de banco de dados e a arquitetura geral do sistema.

---

## 1. Contexto do Negócio
A G N Doces é uma microempresa familiar que produz doces e confeitos artesanais (brownies, pães de mel, etc.). A operação contava com fluxos manuais em planilhas para gerenciar compras de insumos, acompanhar encomendas e calcular o custo de produção de cada lote.

---

## 2. O Problema Inicial
Com a expansão das vendas e a alta volatilidade dos preços de ingredientes nos mercados locais, surgiram três problemas graves:
* **Falta de visibilidade de margem:** O preço de custo real do doce flutuava semanalmente devido à variação do preço da manteiga, chocolate e leite condensado.
* **Processo ineficiente de compras:** Cadastrar manualmente cupons de compras com 40 ou 50 itens tomava muito tempo da equipe.
* **Falta de integração operacional-financeira:** As compras eram anotadas num caderno, a produção de receitas noutro, e as entradas de encomendas numa planilha separada, dificultando calcular o fluxo de caixa consolidado.

---

## 3. A Solução Desenvolvida
Implementamos uma Single Page Application responsiva conectada a uma API REST robusta, integrando compras, estoque de insumos, produção de receitas, produto pronto, faturamento e fluxo de caixa financeiro sob transações relacionais rígidas.

---

## 4. Módulos Implementados
O sistema foi dividido nos seguintes módulos:
1. **Dashboard:** Visão consolidada de lucros, faturamento, despesas operacionais, alertas visuais de ingredientes abaixo do estoque mínimo.
2. **Estoque de Insumos:** Controle de matérias-primas e embalagens, exibindo o custo médio ponderado atualizado a cada nova compra.
3. **Produção (Lotes e Receitas):** Gerenciamento de fichas técnicas de receitas e recheios, cálculo de custo dinâmico e registro de lote.
4. **Vendas & Encomendas:** Vendas diretas de balcão e encomendas agendadas integradas ao estoque de produtos acabados e ao fluxo de recebíveis financeiros.
5. **Importador por IA (Gemini OCR):** Digitalização automática de cupons e notas fiscais por Foto/PDF com associação inteligente de termos.

---

## 5. Decisões Técnicas de Engenharia
* **TypeScript de ponta a ponta:** Monorepo com backend Fastify e frontend React para compartilhamento simplificado de definições de interfaces de dados.
* **ORM e Transações Rígidas (Prisma + PostgreSQL):** Garantia de transações ACID na produção e cancelamento de lotes. Se um lote falha, todos os estornos são revertidos.
* **Fastify Multipart Streams:** O recebimento de Foto/PDF é transmitido direto em buffers de memória, reduzindo processamento e eliminando persistência física temporária no disco do servidor.
* **Zod Schemas no Transporte:** Validação e sanitização estrita de payloads JSON que entram nos endpoints e das variáveis de ambiente na inicialização da aplicação.

---

## 6. Desafios Encontrados
* **Cálculo Dinâmico de Custo Médio:** A cada compra de ingrediente confirmada, recalculamos a média ponderada com a fórmula:
  \[C_{novo} = \frac{(E_{atual} \times C_{atual}) + (Q_{comprada} \times P_{compra})}{E_{atual} + Q_{comprada}}\]
* **Controle de Unidades de Medida:** A disparidade de unidades nas compras (ex: compra em saco de $1\text{ kg}$ ou caixa de $5\text{ kg}$) vs. consumo da receita (ex: $150\text{ g}$) exigiu conversores matemáticos de unidade e tabelas de equivalência no backend.

---

## 7. Incidente Real e Aprendizado de Segurança (Guard Rails)
Durante a fase de testes local no monorepo, um script de teste de produção executou comandos destrutivos (`deleteMany`) no banco de dados ativo. Como a variável `DATABASE_URL` local estava configurada temporariamente com as credenciais de produção da Supabase (pelo banco local não estar instanciado), a base de produção teve dados de receitas, produtos prontos e lotes apagados.

### Ação Corretiva Imediata:
1. Os dados de ingredientes e recheios foram preservados. As receitas e o estoque de produtos prontos foram reconstruídos manualmente através da UI de produção de lotes de forma segura.
2. **Criação de Guard Rails:** Implementamos uma validação profunda de conexão em `lib/safety.ts`. Qualquer script local de teste, migração ou semente (`seed`) invoca este guard rail, que analisa a URL de destino:
   * Se contiver referências de produção (`supabase.com` ou o hash do projeto de produção), aborta o processo imediatamente.
   * Se for banco remoto não-local, exige confirmação explícita (`ALLOW_DESTRUCTIVE_TESTS=true`).
   * Banco local (`localhost`) é liberado automaticamente.

---

## 8. Uso de IA com Gemini OCR
O processo de importação inteligente de notas foi um dos grandes destaques do projeto:
1. **IA Multimodal (Gemini 2.5 Flash):** Utilizado para ler o arquivo binário (Foto/PDF) e extrair os itens no formato estruturado via JSON Schema.
2. **Tratamento de Incerteza (Fallbacks):** Se a nota estiver rasgada ou embaçada e a IA precisar usar valores padrão (fallbacks) para quantidade ou preços, o sistema detecta e força `needsReview = true` e limita a confiança para no máximo `0.50` (capping), bloqueando associações automáticas.
3. **Matcher Levenshtein:** Compara a string extraída pela IA com a base de ingredientes salvando aliases de termos (ex: `L COND MOCOCA 395G` mapeia permanentemente para o ingrediente `Leite condensado`).

---

## 9. Resultados Práticos do ERP
* **Margens reais:** A G N Doces passou a ter o custo centavo por centavo de cada brownie produzido.
* **Automação de Entrada:** Redução do tempo de lançamento de notas de compras de 15 minutos manuais para menos de 30 segundos (via Foto/PDF + revisão assistida).
* **Previsibilidade Financeira:** O fluxo de caixa real passou a considerar as encomendas pendentes de faturamento futuro, melhorando o planejamento financeiro.
