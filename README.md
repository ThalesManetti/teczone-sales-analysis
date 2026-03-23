# teczone-sales-analysis
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0A0F1E,50:00E5FF,100:FF6B2B&height=180&section=header&text=Teczone%20Sales%20Analysis&fontSize=42&fontColor=ffffff&fontAlignY=38&desc=Power%20BI%20%7C%20DAX%20%7C%20SQL%20%7C%20An%C3%A1lise%20Avan%C3%A7ada%20de%20Vendas&descAlignY=58&descSize=16&animation=fadeIn" width="100%"/>

</div>

<br/>

<div align="center">

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-FF6B2B?style=for-the-badge&logo=powerbi&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-00E5FF?style=for-the-badge)

</div>

---

## 📌 Sobre o Projeto

A maioria das análises de vendas para por faturamento total e ranking de produtos. O **Teczone Sales Analysis** vai além — o objetivo foi construir um sistema de inteligência comercial completo, capaz de responder perguntas que impactam diretamente a estratégia do negócio:

> *Quais produtos concentram 80% da receita?*
> *Quais clientes estão prestes a abandonar a empresa?*
> *Quais produtos têm alta margem mas baixo volume — e como ativá-los?*

Utilizando o dataset público de vendas da **Microsoft**, foram desenvolvidos **75 medidas DAX** e **9 colunas calculadas** organizados em 5 módulos de análise.

---

## 📊 Dataset

| Campo | Descrição |
|-------|-----------|
| **Fonte** | Microsoft Sample Sales Dataset |
| **Tabela principal** | `Vendas` — 19 colunas |
| **Dimensões** | Produto, Categoria, Marca, Cliente, País, Continente |
| **Período** | Dados históricos com corte em Agosto/2019 |
| **Métricas base** | Preço Unitário, Custo Unitário, Quantidade Vendida |

---

## 🧩 Módulos de Análise

### 1. 📦 KPIs Gerais — Visão Executiva

Painel central com os indicadores de performance do negócio em tempo real.

| Medida | Descrição |
|--------|-----------|
| `Faturamento` | Receita bruta total |
| `Custo` | Custo total de produtos vendidos |
| `Lucro` | Faturamento − Custo |
| `Margem Bruta` | Lucro em valor absoluto |
| `% Margem` | Margem percentual |
| `Ticket Médio` | Valor médio por transação |
| `Total Quantidade Vendida` | Volume total comercializado |

---

### 2. 🔺 Análise de Pareto (Curva ABC)

Identificação dos produtos que realmente movem o negócio — aplicando o princípio de que ~20% dos produtos respondem por ~80% do faturamento.

```
Classificação ABC:
  ├── Classe A → produtos que acumulam até 80% do faturamento
  ├── Classe B → produtos entre 80% e 95%
  └── Classe C → cauda longa (últimos 5%)
```

**Medidas desenvolvidas:**
- `% Faturamento Acumulado` — percentual acumulado por produto (ranking dinâmico)
- `Classificação ABC` — label A/B/C calculado dinamicamente com DAX
- `Rank Faturamento Único` — ranking sem empates (desempate alfabético)
- `Meta 80%` — linha de referência visual para o corte da curva

---

### 3. 🎯 Análise de Quadrante (Margem × Faturamento)

Cada produto foi posicionado em um dos 4 quadrantes estratégicos com base na **mediana de margem** e na **mediana de faturamento** como linhas de corte dinâmicas.

| Quadrante | Lógica | Estratégia |
|-----------|--------|------------|
| ⭐ **Q1 — Estrelas** | Alta margem + Alto faturamento | Proteger e escalar |
| 💎 **Q2 — Nicho Premium** | Alta margem + Baixo faturamento | Ativar com marketing |
| 💰 **Q3 — Geradores de Caixa** | Baixa margem + Alto faturamento | Otimizar custos |
| ❌ **Q4 — Problemáticos** | Baixa margem + Baixo faturamento | Revisar ou descontinuar |

> 💡 O corte usa `PERCENTILEX.INC` para calcular medianas dinâmicas — o quadrante se atualiza conforme os filtros do relatório.

---

### 4. 👥 Segmentação RFV (Recência · Frequência · Valor)

Sistema de pontuação para classificar clientes por comportamento de compra — do mais valioso ao em risco de churn.

**Scoring (1–5 por dimensão, total 3–15):**

```
Score Recência  → baseado em dias desde última compra
  5 = comprou nos últimos 30 dias
  4 = 31–90 dias
  3 = 91–180 dias
  2 = 181–365 dias
  1 = mais de 1 ano

Score Frequência → número de transações distintas
  5 = 15+ compras   |  4 = 10–14  |  3 = 5–9  |  2 = 2–4  |  1 = 1 compra

Score Valor → faturamento total gerado pelo cliente
  5 = R$10k+  |  4 = R$5k–10k  |  3 = R$2k–5k  |  2 = R$1k–2k  |  1 = <R$1k
```

**5 Segmentos de Clientes:**

| Segmento | Score | Perfil |
|----------|-------|--------|
| 🏆 **Champions (VIP)** | 13–15 | Compram muito, com frequência e recentemente |
| ⭐ **Clientes Leais** | 10–12 | Base sólida e engajada |
| 👍 **Clientes Potenciais** | 7–9 | Bom potencial, ainda não ativado |
| ⚠️ **Em Risco** | 5–6 | Sinais de distanciamento |
| 💤 **Inativos** | 3–4 | Perdidos — ação urgente necessária |

---

### 5. 📉 Análise de Churn

Identificação proativa de clientes em risco de abandono com base em comportamento histórico.

**Definição de Churn:** cliente sem compra nos últimos **6 meses** em relação ao fim do dataset (ago/2019).

| Medida | O que responde |
|--------|---------------|
| `Taxa de Churn` | % de clientes perdidos |
| `Taxa de Retenção` | % de clientes ativos |
| `Receita Perdida Churn` | Faturamento histórico dos clientes em churn |
| `CLV Médio` | Customer Lifetime Value médio por cliente |
| `CLV Perdido Churn` | Valor total de CLV dos clientes perdidos |
| `Risco de Churn` | Classificação de risco por dias sem compra |
| `Churn por Segmento` | Taxa de churn específica por segmento RFV |
| `Evolução Taxa Retenção` | Tendência temporal da retenção |

---

### ⏱️ Time Intelligence (Bônus)

Análises temporais para acompanhamento de tendências e projeções.

- **MoM** — Variação mês a mês
- **YoY** — Comparativo ano a ano
- **YTD** — Acumulado do ano
- **Média Móvel 3 Meses** — Suavização de sazonalidade
- **Sazonalidade por Mês** — Índice de variação em relação à média
- **Tendência Linear** — Direção geral do faturamento
- **Forecast Simples** — Previsão baseada em média móvel

---

## 🛠️ Stack Técnico

```
Modelagem de Dados    →  Power BI Desktop
Linguagem de Medidas  →  DAX (75 medidas | 9 colunas calculadas)
Calendário            →  Tabela Calendário customizada com hierarquia
Relacionamentos       →  Tabela Vendas ↔ Calendário (ativo) + DateTable (local)
Fonte de Dados        →  Microsoft Sample Dataset (CSV/Excel)
```

---

## 📁 Estrutura do Repositório

```
teczone-sales-analysis/
│
├── README.md
├── /assets
│   └── /images          ← Screenshots do dashboard
└── Teczone.pbix         ← Arquivo Power BI (se disponível)
```

---

## 💡 Principais Aprendizados

- **Curva ABC dinâmica em DAX** exige cuidado com contexto de filtro — a solução usou `ALLSELECTED` combinado com `RANKX` para o ranking funcionar corretamente com filtros visuais.
- **Quadrante com medianas dinâmicas** via `PERCENTILEX.INC` garante que o corte se adapte a qualquer seleção de período ou categoria, tornando a análise muito mais robusta que cortes fixos.
- **Segmentação RFV via coluna calculada** foi escolhida sobre medida para permitir uso em segmentações e cruzamentos com outras tabelas sem perda de contexto.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:FF6B2B,50:00E5FF,100:0A0F1E&height=100&section=footer" width="100%"/>

**Thales Manetti** · [LinkedIn](https://www.linkedin.com/in/thalesmanetti/) · [Portfólio](https://thalesmanetti.github.io)

</div>
