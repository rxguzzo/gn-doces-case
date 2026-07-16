# Guia de Prints e Demonstração Visual Segura

Para apresentar o projeto visualmente em seu portfólio no GitHub ou no LinkedIn sem expor informações confidenciais do negócio, siga as diretrizes deste guia.

---

## 📸 1. Telas Recomendadas para Capturar
1. **Painel de Dashboard:** Focado na exibição dos gráficos de receitas e despesas operacionais do fluxo de caixa e na caixa de alertas de ingredientes que atingiram o limite mínimo de estoque.
2. **Importador por IA (Gemini OCR):** Mostrando a área de Drag & Drop para subir Fotos/PDFs e, em seguida, a tela de cards responsivos de revisão, destacando as sugestões com nível de confiança e o card amarelo de alerta quando houve fallback.
3. **Controle de Estoque:** Listando insumos ativos (farinha, chocolate, manteiga), estoques atuais e preços médios ponderados.
4. **Ficha Técnica & Produção:** Exibindo o cadastro de uma receita (ex: Pão de Mel) com sua listagem de ingredientes, rendimento e o histórico de lotes produzidos.
5. **Encomendas:** Exibindo os pedidos futuros organizados com etiquetas coloridas de status (Planejado, Produzido, Entregue) e conciliações de pagamento.
6. **Módulo Financeiro:** Fluxo de caixa de entradas e despesas organizadas por categorias.

---

## 🛡️ 2. Como Preparar os Dados para os Prints (Sem Vazamentos)
Para evitar ter que borrar imagens depois, a melhor estratégia é **popular temporariamente um banco de dados local com dados totalmente fictícios** para fazer as capturas de tela:

* **Nomes de Insumos e Produtos:** Use ingredientes tradicionais (Farinha, Manteiga, Açúcar) e receitas fictícias (Brownie Teste, Pão de Mel Fictício).
* **Nomes de Fornecedores nas Notas:** Altere os nomes das lojas para placeholders (ex: "Mercado da Confeitaria Fictício", "Fornecedor de Alimentos Ltda").
* **Nomes de Clientes nas Encomendas:** Substitua por nomes fictícios comuns (Ana Silva, Carlos Souza, Mariana Oliveira).
* **Valores Financeiros:** Lance compras e vendas fictícias com valores genéricos (R$ 10,00, R$ 50,00, R$ 100,00) que não correspondam ao faturamento ou lucros reais da empresa G N Doces.

---

## ✏️ 3. O Que Deve Ser Mascarado/Borrados (Se usar dados reais)
Caso decida tirar prints com o sistema contendo dados de produção reais, você **deve obrigatoriamente** borrar ou cobrir os seguintes pontos:
* [ ] **Chaves de Nota Fiscal (NFe Key):** Borre completamente o número de 44 dígitos da chave de acesso e o CNPJ dos cupons expostos.
* [ ] **Nomes de Pessoas e Telefones:** Oculte o nome dos clientes reais e os números de WhatsApp cadastrados no módulo de encomendas.
* [ ] **URLs da API do Render:** Se tirar prints do console do navegador (Developer Tools) ou de rotas, oculte a URL real do servidor backend (ex: `https://gn-doces-api.onrender.com`).
* [ ] **Faturamento e Lucros Reais:** Se os gráficos do Dashboard mostrarem o faturamento total exato de vendas da empresa, utilize as ferramentas de edição de imagem para borrar os números consolidados de lucro e despesa acumulada.
