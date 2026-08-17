# powerbi-dashboard-logistica
Dashboard em Power BI para monitoramento de logística e transporte da LogBrasil, com modelagem Star Schema, análise de nível de serviço (OTIF, On Time, In Full) e KPIs de frete e custos.

# 🚚 LogBrasil Distribuição — Dashboard de BI em Logística

> Painel gerencial e operacional desenvolvido em Power BI para monitoramento de nível de serviço (OTIF), análise de custos de frete, performance de transportadoras e controle de ocorrências em todo o território nacional.

---

## 📌 Contexto de Negócio
A **LogBrasil Distribuição S.A.** opera com 6 centros de distribuição (CDs) próprios e atende canais de varejo, indústria e e-commerce utilizando frota própria e transportadoras terceirizadas (modais rodoviário, aéreo e fluvial). 

### Perguntas de Negócio Respondidas:
* Qual é o nível de serviço real da operação (% OTIF, On Time e In Full) frente às metas de cada CD?
* Quais transportadoras, modais e rotas apresentam maior degradação de prazo e custo elevado por km?
* Qual é o impacto financeiro das ocorrências operacionais e extravios de mercadorias?
* Como se comportam os custos por tonelada e por quilômetro rodado ao longo do tempo?

---

## 🖼️ Páginas do Dashboard

### 1. Visão Executiva
*(Substitua este texto pelo caminho da imagem: `![Visão Executiva](imagens/pagina1.png)`)*
* **Destaques:** KPIs de entregas, % OTIF, gap vs. meta, custo por km, margem de frete e distribuição geográfica por UF.

### 2. Nível de Serviço (SLA)
*(Substitua este texto pelo caminho da imagem: `![Nível de Serviço](imagens/pagina2.png)`)*
* **Destaques:** Matriz de desempenho por transportadora, dispersão de lead time x distância e análise de atraso médio.

### 3. Custos e Rentabilidade
*(Substitua este texto pelo caminho da imagem: `![Custos e Rentabilidade](imagens/pagina3.png)`)*
* **Destaques:** Custo por km por modal/veículo, gráfico de Pareto por cliente e custo por tonelada por CD.

### 4. Ocorrências e Detalhamento (Drill-Through)
*(Substitua este texto pelo caminho da imagem: `![Ocorrências](imagens/pagina4.png)`)*
* **Destaques:** Valor de mercadoria em risco, causas-raiz de ocorrências por responsável e detalhamento em nível de CT-e.

---

## 🛠️ Arquitetura e Modelagem

* **Modelo Dimensional (Star Schema):** 1 tabela fato central (`fEntregas` com 15 mil registros), 1 fato de metas mensais (`fMetas`) e 8 dimensões (`dCalendario`, `dCliente`, `dTransportadora`, `dVeiculo`, `dMotorista`, `dCentroDistribuicao`, `dDestino`, `dStatus`, `dOcorrencia`).
* **Tratamento de Dados (Power Query):** Criação de parâmetros para caminho dinâmico (`pCaminho`), tipagem estrita de dados e flags calculadas na carga para otimização de performance.
* **DAX Avançado:** 
  * Relacionamentos inativos acionados via `USERELATIONSHIP`.
  * Inteligência de tempo com `DATESINPERIOD` (OTIF Móvel 3M) e `SAMEPERIODLASTYEAR`.
  * Análise de Pareto e rankings dinâmicos com `RANKX` e `ALLSELECTED`.

---

## 💡 Principais Insights e Conclusões

1. **Gargalo nas rotas Norte/Nordeste:** As transportadoras que atendem as rotas fluviais e regionais puxam a média do OTIF para baixo, exigindo renegociação de SLA ou revisão da matriz modal.
2. **Sazonalidade de Final de Ano:** Identificado aumento acentuado no volume entre novembro e dezembro acompanhado de queda no nível de serviço (trade-off de capacidade).
3. **Causa-Raiz das Ocorrências:** Parcela relevante das devoluções decorre de problemas internos na separação e documentação fiscal no CD, antes do embarque na transportadora.

---

## 📂 Como Reproduzir este Projeto

1. Clone o repositório ou baixe os arquivos.
2. Abra o arquivo `.pbix` no Power BI Desktop.
3. No Power Query, altere o parâmetro `pCaminho` para a pasta local onde estão salvos os arquivos `Fato_Entregas.csv` e `Dimensoes_Logistica.xlsx`.
4. Clique em **Fechar e Aplicar**.
