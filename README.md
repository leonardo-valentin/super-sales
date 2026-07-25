# Análise de Vendas — Superstore Sales

Projeto de análise de dados de vendas do varejo (dataset "Superstore"), utilizando **SQL** para exploração inicial e **Power BI** para construção de um dashboard executivo.

O foco do projeto foi partir de perguntas de negócio formuladas a partir da exploração dos dados brutos, e responder essas perguntas com consultas SQL e visualizações no Power BI.

---

# Objetivo

Investigar o comportamento de vendas da empresa — por categoria, região, subcategoria, modo de envio e cliente — respondendo a um conjunto de perguntas de negócio levantadas durante a exploração inicial dos dados, e comunicar os resultados através de um dashboard no Power BI.

---

# Dataset

- **Fonte:** Kaggle — [Sales Forecasting Dataset](https://www.kaggle.com/datasets/rohitsahoo/sales-forecasting)
- **Período:** 2015 a 2018 (com base em `Order Date`)
- **Registros:** 9.800 linhas de pedido
- **Campos principais:** `Order Date`, `Ship Date`, `Ship Mode`, `Customer Name`, `Segment`, `Region`, `City`/`State`, `Category`, `Sub-Category`, `Product Name`, `Sales`

---

# Processo

1. Carga dos dados brutos em um banco SQLite (`banco_dados/superstore.db`), com a tabela `train`.
2. Exploração de dados via SQL no DB Browser for SQLite (`sql/superstore.sqbpro`), incluindo: soma total de vendas, vendas por cidade, por região, por categoria+região, por categoria+cidade, por modo de envio+região, por subcategoria (soma e contagem) e por cliente+categoria.
3. Formulação de perguntas de negócio a partir das descobertas iniciais.
4. Modelagem e construção do dashboard no Power BI (`bi_dashboard/super_sales.pbix`), com uma página geral e uma página executiva de drill-down para a categoria Technology.
5. Exportação dos dashboards em imagem (`dashboard.png`, `technologydashboard.png`).

---

# Visão Geral do Dataset

O faturamento total foi de aproximadamente **2,26 milhões**, distribuído entre três categorias:

| Categoria       | Faturamento | Pedidos (linhas) |
| --------------- | ----------: | ----------------: |
| Technology      |     827.456 |             1.813 |
| Furniture       |     728.659 |             2.078 |
| Office Supplies |     705.422 |             5.909 |

### Insight

**Office Supplies** concentra o maior número de linhas de pedido, mas gera o menor faturamento das três categorias — indício de produtos de ticket unitário baixo. Já **Technology** tem o menor volume de pedidos e o maior faturamento, sugerindo produtos de maior valor agregado.

---

# Perguntas de Negócio Respondidas

## 1. Quais regiões mais compram e existe preferência por categoria?

**West** e **East** concentram o maior faturamento entre as quatro regiões (Region no dashboard geral), seguidas por Central e South.

Nas quatro regiões, as três categorias (Furniture, Office Supplies, Technology) aparecem representadas em proporções semelhantes dentro da barra — não há indício de uma região com preferência marcante por uma única categoria.

## 2. Existe tendência no modo de envio (Ship Mode)?

Sim. **Standard Class** é o modo de envio amplamente dominante em volume de vendas, muito acima de Second Class, First Class e Same Day — e essa predominância se mantém nas três categorias, já que a proporção de Furniture/Office Supplies/Technology dentro de cada barra de modo de envio é semelhante.

Uma quebra adicional por cidade e por faixa de valor do pedido não mostrou desvio desse padrão: cidades com maior volume de compras também concentram suas vendas em Standard Class, e produtos de maior valor não apresentam preferência por modos de envio mais rápidos — o comportamento se mantém consistente independentemente da cidade ou do valor do produto.

## 3. Quais subcategorias são as mais vendidas?

Em faturamento, as subcategorias que mais se destacam são, em ordem:

- Phones
- Chairs
- Storage
- Tables

## 4. Como o faturamento evoluiu por ano, por categoria?

| Ano  | Faturamento |
| ---: | ----------: |
| 2015 |     479.860 |
| 2016 |     459.440 |
| 2017 |     600.190 |
| 2018 |     722.050 |

Após uma leve queda em 2016, a empresa apresentou crescimento contínuo, encerrando 2018 com um faturamento cerca de 50% maior que o início da série histórica.

Olhando a evolução por categoria (visível no dashboard executivo de Technology), as três categorias têm trajetória parecida até 2017, mas em 2018 **Technology** se destaca e passa a crescer mais que Furniture e Office Supplies.

## 5. Existe concentração de faturamento em poucos clientes?

Não de forma expressiva. O maior comprador identificado, **Sean Miller**, soma R$ 25.043,05 — cerca de 1,1% do faturamento total. Os nove maiores compradores somados (Sean Miller, Tamara Chand, Raymond Buch, Tom Ashbrook, Adrian Barton, Ken Lonsdale, Sanjit Chand, Hunter Lopez e Sanjit Engle) representam juntos aproximadamente 6,3% do faturamento total, o que indica uma base de clientes relativamente distribuída.

---

# Dashboard Geral

![Dashboard Geral](bi_dashboard/dashboard.png)

O dashboard geral reúne o faturamento total, vendas por categoria, por região+categoria, por ano, por subcategoria, por modo de envio+categoria e o ranking dos maiores compradores.

---

# Dashboard Executivo — Technology

![Dashboard Tecnologia](bi_dashboard/technologydashboard.png)

Página de drill-down construída para comunicar rapidamente os indicadores da categoria **Technology**. Os "Key Insights" abaixo são os que já estão escritos no próprio dashboard:

- Tecnologia representa **37%** do faturamento total.
- Crescimento de **54,9%** desde 2015.
- Crescimento de **21,4%** em relação ao ano anterior.
- **Phones** é a subcategoria com maior faturamento dentro de Technology.
- **East** e **West** concentram o maior volume de vendas da categoria.

---

# Ferramentas Utilizadas

- SQL (SQLite) — `banco_dados/superstore.db`
- DB Browser for SQLite — `sql/superstore.sqbpro`
- Power BI Desktop — `bi_dashboard/super_sales.pbix`
- DAX — medidas de crescimento % ano a ano e desde 2015, usadas nos cartões do dashboard executivo

---

# Principais Aprendizados

Durante este projeto pratiquei:

- Estruturação de um banco de dados SQLite a partir de um CSV bruto.
- Exploração de dados com SQL (agregações, `GROUP BY`, ordenação, comparação entre categorias, regiões e clientes).
- Formulação de perguntas de negócio a partir de descobertas iniciais na exploração dos dados.
- Modelagem e construção de dashboard no Power BI com múltiplas visualizações.
- Criação de uma página executiva de drill-down focada em uma única categoria.
- Uso de medidas calculadas (DAX) para indicadores de crescimento percentual.
- Leitura crítica de gráficos para extrair insights sem inflar conclusões além do que os dados mostram.

---
