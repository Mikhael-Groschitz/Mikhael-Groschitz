<div align="center">

# Mikhael Groschitz

### Engenheiro de Dados

**SQL Server · T-SQL · Python · Azure**

Pipelines ETL/ELT · Modelagem Dimensional · CDC · Data Warehouse · Data Quality

<br>

<a href="https://www.linkedin.com/in/mikhael-groschitz/">
  <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/>
</a>
<a href="https://mgroschitz.dev">
  <img src="https://img.shields.io/badge/Portf%C3%B3lio-111111?style=for-the-badge&logo=vercel&logoColor=white" alt="Portfólio"/>
</a>
<a href="mailto:mgroschitz@gmail.com">
  <img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/>
</a>

<br><br>

<img src="https://go-skill-icons.vercel.app/api/icons?i=python,sqlserver,azure,docker,git,postgres" />

</div>

---

## Sobre

Atuo com engenharia de dados em SQL Server e Azure: modelagem, pipelines ETL/ELT, otimização de T-SQL e automação de processos em Python.

Hoje sou responsável pela estrutura de dados de um CRM jurídico em produção — modelo de dados, views, índices e constraints, otimização das consultas críticas do sistema e robôs em Python que sustentam a rotina da operação. As implantações em ambiente são feitas em conjunto com o time de DBA.

Antes disso, trabalhei com dados financeiros e contábeis: extração e tratamento de grandes volumes com SQL e Python (Pandas, NumPy), dashboards em Power BI, detecção de anomalias e análises preditivas para fluxo de caixa e rentabilidade.

Os projetos abaixo são construídos de ponta a ponta, com foco no que uma vaga de engenharia de dados realmente cobra: ingestão incremental, modelagem dimensional, orquestração, qualidade de dados e execução em cloud.

---

## Projetos

### [Pipeline ELT de Preços de Combustíveis da ANP em Azure](https://github.com/Mikhael-Groschitz/anp-fuel-prices-elt-azure)

Série histórica pública da ANP — 20 anos de coleta semanal de preços por posto revendedor, 219 arquivos CSV/ZIP — ingerida, padronizada e modelada em um Data Warehouse dimensional na nuvem, com custo mantido perto de zero.

- **35,3M linhas de estágio → 32,2M linhas na fato**, carga histórica completa em pouco mais de 3h
- Orquestração metadata-driven no **Azure Data Factory** (4 pipelines), sem Mapping Data Flows — toda transformação em stored procedures T-SQL, dentro do compute que o banco já paga
- Modelo estrela com **SCD Tipo 2** e 8 checagens de qualidade com severidade gravadas em log
- Autenticação **100% Azure AD**: não existe login nem senha SQL em nenhum ponto do projeto
- Otimizações medidas em plano de execução: inlining de UDF escalar, índice clusterizado, conversão implícita que invalidava seek e SCD2 set-based no lugar de cursor — **projeção inicial de ~15h para 3h reais**

`Azure Data Factory` `ADLS Gen2` `Azure SQL` `T-SQL` `Bicep` `Python` `Power BI (PBIP/TMDL)`

### [CDC no SQL Server → Data Warehouse Dimensional](https://github.com/Mikhael-Groschitz/sqlserver-cdc-to-dw)

Um OLTP sintético é alterado continuamente, o **Change Data Capture nativo do SQL Server** captura as mudanças e um pipeline em Python/T-SQL as transforma incrementalmente em um Data Warehouse dimensional.

- Extração incremental por **janela de LSN**, com watermark avançado na mesma transação do insert — sem estado "capturei mas não marquei"
- **SCD Tipo 2** em dimensões com índice único filtrado garantindo uma única versão vigente por chave de negócio
- Exclusão lógica na fato em vez de `DELETE` físico, preservando auditoria de cancelamentos
- 5 checagens de qualidade, CLI de orquestração (`run` / `status` / `reset`), testes em pytest e mapeamento documentado do pipeline inteiro para Azure Data Factory

`SQL Server 2022` `T-SQL` `CDC` `Python` `Docker Compose` `pytest`

### Em construção

**Lakehouse sobre a base pública de CNPJ da Receita Federal** — Airflow e PySpark em Docker, camadas bronze/silver/gold em MinIO, Parquet particionado e checagens de qualidade. Cobre processamento distribuído e orquestração.

---

## Stack

| | |
| :--- | :--- |
| **Linguagens** | Python (Pandas, NumPy) · SQL · T-SQL · Java |
| **Bancos & Modelagem** | SQL Server · PostgreSQL · MySQL · Modelagem Dimensional · Star Schema · SCD Tipo 2 · CDC |
| **Cloud & Orquestração** | Azure (Data Factory, ADLS Gen2, Azure SQL) · Airflow · Docker · Bicep |
| **BI & Qualidade** | Power BI · Data Quality checks · pytest |
| **Engenharia** | Git · Azure DevOps · CI/CD · APIs REST · Spring Boot |

---

## Formação

- **Pós-graduação Lato Sensu** — Arquitetura de Software, Ciência de Dados e Cybersecurity · PUCPR (2025 – 2026)
- **Tecnólogo em Análise e Desenvolvimento de Sistemas** · Anhanguera (2023 – 2025)

---

<div align="center">

**Aberto a conversas sobre vagas de Engenheiro de Dados.**

[LinkedIn](https://www.linkedin.com/in/mikhael-groschitz/) · [mgroschitz.dev](https://mgroschitz.dev) · [mgroschitz@gmail.com](mailto:mgroschitz@gmail.com)

</div>
