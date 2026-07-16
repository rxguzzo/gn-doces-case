# Política de Segurança e Privacidade do Case

Este documento detalha as políticas e práticas aplicadas no projeto **G N Doces ERP** para garantir a segurança operacional e a privacidade dos dados reais do negócio.

---

## 🔒 1. Código-Fonte Privado
O repositório de produção completo deste sistema é mantido como **privado**. Apenas o presente estudo de caso técnico e materiais de apresentação são expostos publicamente. 
### Motivos da restrição:
* **Privacidade de Custos:** Contém margens operacionais de receitas, custos de ingredientes e despesas operacionais da marca ativa G N Doces.
* **Segurança de APIs:** Endpoints e rotas de serviços integrados e tokens de ambiente do Render e Supabase.
* **Dados Sensíveis:** Dados de contato de clientes reais e histórico de faturamento financeiro.

---

## 🔑 2. Proteção de Credenciais e Chaves de API
* **Variáveis de Ambiente:** Nenhuma chave secreta (como a `GEMINI_API_KEY` do Google AI Studio ou as credenciais PostgreSQL do Supabase) é incluída no código estático ou versionada no Git.
* **Env Segregation (Frontend/Backend):** O backend consome e autentica as requisições do Gemini diretamente. O frontend nunca tem acesso e nunca armazena chaves de inteligência artificial ou chaves de banco de dados, protegendo contra vazamentos via console ou pacotes compilados JS.
* **Arquivos Locais:** Os arquivos `.env` locais estão inseridos no `.gitignore` global do workspace, garantindo que não subam acidentalmente para o controle de versão remoto.

---

## 🛡️ 3. Guard Rails Programáticos de Banco de Dados
Para eliminar o risco de perda ou corrupção de dados ativos em servidores na nuvem durante execuções locais de testes unitários ou sementes (`seed`), criamos uma camada isolada de segurança (`apps/crm-api/src/lib/safety.ts`):
* **Classificação de Conexão:** Ao iniciar comandos, a aplicação analisa a string configurada na variável `DATABASE_URL`.
* **Bloqueio de Produção:** Se a string de conexão apontar para o projeto ativo da Supabase, a execução é interrompida imediatamente disparando um erro de `SAFETY BLOCK`.
* **Banco Local Protegido:** Garante que limpezas automáticas ocorram estritamente em ambiente `localhost`.
* **Segregação de Staging:** Para bancos remotos de teste ou staging, o script exige a flag explícita `ALLOW_DESTRUCTIVE_TESTS=true` no arquivo de ambiente, atuando como confirmação manual dupla de segurança.
