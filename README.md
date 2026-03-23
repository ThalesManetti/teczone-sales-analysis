# teczone-sales-analysis
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A0F1E,50:00E5FF,100:FF6B2B&height=180&section=header&text=Teczone%20Sales%20Analysis&fontSize=42&fontColor=ffffff&fontAlignY=38&desc=Power%20BI%20%7C%20DAX%20%7C%20Varejo%20%7C%20Case%20Study%20Completo&descAlignY=58&descSize=16&animation=fadeIn" width="100%"/>

</div>

<br/>

<div align="center">

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-FF6B2B?style=for-the-badge&logo=powerbi&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-00E5FF?style=for-the-badge&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-2EA44F?style=for-the-badge)
![Nível](https://img.shields.io/badge/N%C3%ADvel-Pleno-FF6B2B?style=for-the-badge)

</div>

<div align="center">

🔗 **[Acessar Dashboard no Power BI Service](https://app.powerbi.com/links/RJb66n1VAz?ctid=57d2ea99-01a6-4ab8-86bb-75c0642ef771&pbi_source=linkShare)**

</div>

---

## 🎯 Problema de Negócio

A **TechZone**, empresa de varejo de eletrônicos e tecnologia, enfrentava um cenário crítico em 2019: após um ano excepcional em 2018, o negócio entrou em desaceleração acentuada. Os sintomas eram claros, mas as causas e as soluções, não.

| Problema | Impacto |
|----------|---------|
| 📉 Queda de **37,8% no faturamento** vs. ano anterior | Reversão de crescimento sem causa identificada |
| 🚨 Taxa de churn **superior a 20%** | R$ 9,17M em receita perdida |
| 🌫️ Sem visibilidade sobre clientes e produtos de maior valor | Decisões de alocação de recursos baseadas em intuição |
| ❌ Sem estratégia de retenção fundamentada em dados | Ciclo vicioso de perda de base + queda de receita |

### Para quem foi desenvolvido

O dashboard foi construído para três públicos com necessidades distintas:

- **C-Level (CEO, CFO, CMO)** → decisões estratégicas sobre onde alocar recursos
- **Gerentes Comerciais e de Marketing** → ações táticas de produto e segmento
- **Equipe de CRM** → operacionalização de campanhas de retenção e ativação

> A decisão crítica que a diretoria precisava tomar: *quais segmentos priorizar, quais produtos manter ou descontinuar, e em quais mercados investir para reverter a desaceleração.*

---

## 📊 Dataset

| Dimensão | Volume |
|----------|--------|
| **Fonte** | Base transacional histórica (CSV) |
| **Período** | Junho/2017 — Agosto/2019 (27 meses) |
| **Transações** | ~204.000 registros |
| **Clientes únicos** | 18.334 |
| **Produtos ativos** | 447 SKUs |
| **Categorias** | 20 |
| **Países** | 5 (presença global) |

**Arquitetura:** Star Schema — Tabela Fato `Vendas` (19 colunas) + Dimensão `Calendário` (13 colunas + hierarquia) + Tabela `Medidas` (75 medidas DAX)

---

## ⚙️ Processo de Desenvolvimento

### ETL — Power Query
- ✅ Padronização de datas e normalização de produtos/categorias
- ✅ Criação de hierarquias geográficas (País → Continente)
- ✅ Remoção de duplicatas e tratamento de nulos
- ✅ Construção da tabela calendário completa

### Modelagem DAX — Colunas Calculadas
- ✅ **Scores RFV** — Recência, Frequência e Valor (escala 1–5 por dimensão)
- ✅ **Segmentação de Clientes** — Champions, Leais, Potenciais, Em Risco, Inativos
- ✅ **Status de Churn** — Ativo vs. Churn (corte: 6 meses sem compra)
- ✅ **Matriz BCG Adaptada** — Quadrantes Estrelas, Geradores de Caixa, Nicho Premium, Problemáticos
- ✅ **Classificação ABC** — Curva de Pareto por produto

---

## 📐 KPIs e Resultados

### 💰 Faturamento Total: R$ 64,17M
Crescimento de **97,6% em 2018** seguido de queda de **37,8% em 2019** — o ponto de inflexão que justificou toda a análise.

### 📊 Margem Bruta: 58,37%
Excelente para o setor, mas com **erosão preocupante**: 60,59% (2017) → 58,90% (2018) → 55,71% (2019). Perda de **4,88 pontos percentuais** em dois anos, indicando pressão de preços ou custos não repassados.

### 👥 Churn: 21,58% | Receita Perdida: R$ 9,18M
3.957 clientes inativos. Com CLV médio de R$ 3.500, o **valor de lifetime perdido é R$ 13,85M**. Cada ponto percentual de churn = ~R$ 640 mil em receita.

### 🏷️ Curva ABC — 106 produtos geram 80% da receita
- **Classe A:** 106 produtos (23,7%) → R$ 51,3M (80% do faturamento)
- **Classe B:** 149 produtos → 15% do faturamento
- **Classe C:** 192 produtos (43%) → apenas 5% do faturamento

### 👤 Segmentação RFV — 18.334 clientes classificados
| Segmento | Clientes | Score | Participação |
|----------|----------|-------|-------------|
| 🏆 Champions | 2.090 | 13–15 | 11,4% |
| ⭐ Leais | 7.349 | 10–12 | 40,1% |
| 👍 Potenciais | 6.280 | 7–9 | 34,3% |
| ⚠️ Em Risco | 1.874 | 5–6 | 10,2% |
| 💤 Inativos | 741 | 3–4 | 4,0% |

---

## 💡 Principais Insights

### Insight 1 — Crise de Retenção: R$ 13,8M em Valor Perdido
3.957 clientes inativos representam R$ 13,85M em CLV perdido além dos R$ 9,18M documentados em receita histórica. Com 1.874 clientes no segmento "Em Risco", a janela para intervenção é de 60–90 dias.

**Ação recomendada:** programa anti-churn em dois grupos — reativação imediata dos "Em Risco" com cupom de 20% + gatilhos automáticos aos 60/90/120 dias sem compra. Reduzir churn de 21,58% para 15% economiza ~R$ 4,2M/ano.

---

### Insight 2 — Portfólio Mal Otimizado Imobiliza R$ 2–3M em Capital
192 produtos Classe C (43% do catálogo) respondem por apenas 5% da receita, imobilizando capital com giro lento (+120 dias). Os 447 produtos no quadrante "Problemáticos" têm margem de 49,67% — abaixo da média — e destroem valor operacional.

**Ação recomendada:** auditoria "Kill or Keep" em 30 dias, liquidação via marketplace com 30–40% de desconto e realocação de R$ 2M para ampliar estoque dos Top 50 Estrelas (65,2% da receita, margem de 62%).

---

### Insight 3 — 6.280 Clientes "Potenciais" Podem Gerar +R$ 4M
34,3% da base (6.280 clientes) conhece a marca e já comprou 2–4 vezes, mas está subaproveitada. Converter 20% desse segmento para "Leais" representa aumento médio de R$ 1.500 no CLV por cliente = **+R$ 1,88M em receita incremental**.

---

## 🖥️ Screenshots do Dashboard

**Página 1 — Capa**
![Capa](assets/images/Teczone%201.png)

---

**Página 2 — Gerencial & KPIs**
![Gerencial e KPI](assets/images/Teczone%202.png)

---

**Página 3 — Lucratividade**
![Lucratividade](assets/images/Teczone%203.png)

---

**Página 4 — Análise de Pareto (Curva ABC)**
![Pareto](assets/images/Teczone%204.png)

---

**Página 5 — Segmentação RFV**
![Segmento RFV](assets/images/Teczone%205.png)

---

**Página 6 — Análise Temporal**
![Análise Temporal](assets/images/Teczone%206.png)

---

**Página 7 — Análise de Churn**
![Churn](assets/images/Teczone%207.png)

---

**Página 8 — Insights**
![Insights](assets/images/Teczone%208.png)

---

## 🛠️ Stack Técnico

```
Modelagem de Dados    →  Power BI Desktop
ETL                   →  Power Query (M)
Linguagem de Medidas  →  DAX (75 medidas | 9 colunas calculadas)
Arquitetura           →  Star Schema
Calendário            →  Tabela customizada com hierarquia Ano > Trimestre > Mês > Dia
Fonte de Dados        →  Base transacional CSV (Microsoft Sample Dataset)
```

---

## 📁 Estrutura do Repositório

```
teczone-sales-analysis/
│
├── README.md
├── Analise de Vendas.pbix     ← Arquivo Power BI completo
└── assets/
    └── images/                ← Screenshots das 8 páginas do dashboard
```

---

## 💡 Principais Aprendizados Técnicos

- **Curva ABC dinâmica em DAX** exige cuidado com contexto de filtro — a solução usou `ALLSELECTED` + `RANKX` para o ranking funcionar corretamente com filtros visuais sem quebrar o acumulado.
- **Quadrante com medianas dinâmicas** via `PERCENTILEX.INC` garante que o corte se adapte a qualquer seleção de período ou categoria — muito mais robusto que cortes fixos hardcoded.
- **Segmentação RFV via coluna calculada** (não medida) foi escolhida para permitir uso em segmentações, matrizes e cruzamentos com outras tabelas sem perda de contexto de filtro.
- **Churn como coluna calculada** com corte de 6 meses permite filtrar e cruzar o status do cliente com qualquer outra dimensão do modelo sem usar CALCULATE aninhado.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:FF6B2B,50:00E5FF,100:0A0F1E&height=100&section=footer" width="100%"/>

**Thales Manetti** · [LinkedIn](https://www.linkedin.com/in/thalesmanetti/) · [Portfólio](https://thalesmanetti.github.io)

</div>
