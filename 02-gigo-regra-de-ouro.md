# 🎒 Guia 02: GIGO - A Regra de Ouro da Expedição de Dados

Se você já acampou ou fez uma trilha longa, sabe que a regra número um da sobrevivência é: **o que você coloca na mochila determina o sucesso da viagem.** Se você embalar ração estragada no acampamento base, a sua equipe vai adoecer no meio da montanha. 

Na selva dos dados, chamamos isso de **GIGO: Garbage In, Garbage Out** (Lixo entra, Lixo sai).

Não importa se o seu ecossistema de dados custa milhares de dólares, se você usa as ferramentas mais modernas (*dbt, Snowflake, Tableau*) ou se aplicou um modelo de Machine Learning complexo. **Se o dado que alimenta a pipeline for um lixo, a decisão gerada no final será um lixo.** A única diferença é que, com ferramentas modernas, você processa o lixo muito mais rápido.

---

### 🗑️ A Anatomia do Lixo (Onde o GIGO acontece)

O lixo não aparece no dashboard por mágica. Ele entra sorrateiramente na mochila da expedição em três momentos principais:

1. **Na Captura (A Nascente):** O sistema não tem travas. O usuário digita "Teste123" no campo de CPF, a idade do cliente fica registrada como 150 anos, ou o fuso horário do servidor salva vendas do Brasil como se estivéssemos em Londres.
2. **Na Integração (A Trilha):** Duas bases de dados são unidas (um `JOIN` mal feito em SQL) e de repente as vendas duplicam misteriosamente.
3. **Na Definição (O Mapa Falso):** A métrica de "Usuários Ativos" significa quem fez login para o time de Produto, mas significa quem comprou para o time de Marketing. A falta de um dicionário de dados cria o "Lixo Semântico".

> "A pior coisa que pode acontecer a uma empresa não é não ter um dashboard. É ter um dashboard lindo, brilhante e rápido... que conta uma mentira com precisão matemática." 🌿

---

### 🧐 Auditoria do Guia: Como barrar o GIGO

Como Guia de Dados, meu papel é montar barreiras de proteção antes que o lixo chegue ao cume da montanha (a diretoria). É assim que eu audito e aplico o controle de qualidade:

🟢 **O que funciona (A Mentalidade):**
Descentralizar a responsabilidade. O engenheiro de software que cria o botão no aplicativo precisa saber que a falta de um ID correto naquele botão vai destruir a análise de conversão do time de Produto meses depois. Qualidade de dados é cultura, não apenas código.

🎨 **Ajustes de Design (Visualizando o Caos):**
O lixo deve ser visível para quem limpa. Todo time de dados maduro deve ter um **Painel de Data Quality (Qualidade de Dados)**. Em vez de mostrar vendas, esse painel mostra: "Percentual de cadastros com e-mail em branco", "Volume de IDs duplicados hoje" ou "Picos de faturamento acima de 3 desvios padrões".

⚠️ **Auditoria de Dados (Os 3 Testes Básicos):**
Antes de entregar uma tabela para o negócio, audite:
1. **Completude:** Existem valores `NULL` onde deveriam haver IDs obrigatórios?
2. **Unicidade:** A chave primária (ex: ID da Venda) está repetida?
3. **Validade:** Os valores fazem sentido no mundo real? (Ex: Data de nascimento no futuro ou preços negativos).

✅ **Plano de Ação para a Base:**
1. **Contratos de Dados:** Estabelecer regras claras com o time de engenharia sobre como o dado deve ser emitido.
2. **Testes Automatizados:** Implementar testes básicos nas pipelines (usando pacotes de testes do `dbt`, por exemplo) para que a execução pare se o dado estiver corrompido.
3. **Quarentena:** Se o dado falhar nos testes, ele não vai para o dashboard. Ele vai para uma tabela de "quarentena" para ser investigado.

---
*Escrito por Glaucia Portugal 🐈‍⬛🤘*
