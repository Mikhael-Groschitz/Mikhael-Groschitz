<div align="center">

# Mikhael Groschitz

**Engenheiro de Dados**

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&color=2F81F7&center=true&vCenter=true&width=600&lines=Pipelines+ETL%2FELT+em+Azure+e+SQL+Server;Modelagem+dimensional%2C+SCD2+e+CDC;Otimiza%C3%A7%C3%A3o+de+T-SQL+em+escala)](https://git.io/typing-svg)

<a href="https://www.linkedin.com/in/mikhael-groschitz/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="https://mgroschitz.dev"><img src="https://img.shields.io/badge/Portf%C3%B3lio-111111?style=for-the-badge&logo=vercel&logoColor=white" alt="Portfólio"/></a>
<a href="mailto:mgroschitz@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/></a>

</div>

---

## Sobre

Atuo com engenharia de dados em SQL Server e Azure: modelagem, pipelines ETL/ELT, otimização de T-SQL e automação de processos em Python.

* **Atuação atual:** responsável pela estrutura de dados de um CRM jurídico em produção — modelo de dados, views, índices e constraints, otimização das consultas críticas do sistema e robôs em Python que sustentam a rotina da operação. Implantações feitas em conjunto com o time de DBA.
* **Antes disso:** dados financeiros e contábeis — extração e tratamento de grandes volumes com SQL e Python (Pandas, NumPy), dashboards em Power BI, detecção de anomalias e análises preditivas para fluxo de caixa e rentabilidade.
* **Foco técnico:** ingestão incremental, modelagem dimensional, orquestração, qualidade de dados e execução em cloud com custo controlado.

---

## Projetos

<table>
<tr><td>
<h3>Pipeline ELT de Preços de Combustíveis da ANP em Azure</h3>
<p>Série histórica pública da ANP — 20 anos de coleta semanal de preços por posto revendedor, 219 arquivos CSV/ZIP — ingerida, padronizada e modelada em um Data Warehouse dimensional na nuvem.</p>
<ul>
<li><b>Escala:</b> 35,3M linhas de estágio → <b>32,2M linhas na fato</b>, carga histórica completa em pouco mais de 3h.</li>
<li><b>Performance:</b> otimizações medidas em plano de execução — inlining de UDF escalar, índice clusterizado, conversão implícita que invalidava seek e SCD2 set-based no lugar de cursor. Projeção inicial de ~15h para <b>3h reais</b>.</li>
<li><b>Arquitetura:</b> orquestração metadata-driven no Azure Data Factory (4 pipelines, sem Mapping Data Flows), toda transformação em stored procedures T-SQL dentro do compute que o banco já paga.</li>
<li><b>Qualidade e segurança:</b> modelo estrela com SCD Tipo 2, 8 checagens de qualidade com severidade gravadas em log, autenticação 100% Azure AD — não existe login nem senha SQL em nenhum ponto do projeto.</li>
</ul>
<p><a href="https://github.com/Mikhael-Groschitz/anp-fuel-prices-elt-azure"><img src="https://img.shields.io/badge/Ver_reposit%C3%B3rio-181717?style=flat-square&logo=github&logoColor=white" /></a></p>
<p><img src="https://img.shields.io/badge/Azure_Data_Factory-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" /> <img src="https://img.shields.io/badge/ADLS_Gen2-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" /> <img src="https://img.shields.io/badge/Azure_SQL-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white" /> <img src="https://img.shields.io/badge/T--SQL-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white" /> <img src="https://img.shields.io/badge/Bicep-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" /> <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=powerbi&logoColor=black" /></p>
</td></tr>
<tr><td>
<h3>CDC no SQL Server → Data Warehouse Dimensional</h3>
<p>Um OLTP sintético é alterado continuamente, o <b>Change Data Capture nativo do SQL Server</b> captura as mudanças e um pipeline em Python/T-SQL as transforma incrementalmente em um Data Warehouse dimensional.</p>
<ul>
<li>Extração incremental por <b>janela de LSN</b>, com watermark avançado na mesma transação do insert — sem estado "capturei mas não marquei".</li>
<li><b>SCD Tipo 2</b> em dimensões com índice único filtrado garantindo uma única versão vigente por chave de negócio.</li>
<li>Exclusão lógica na fato em vez de <code>DELETE</code> físico, preservando auditoria de cancelamentos.</li>
<li>5 checagens de qualidade, CLI de orquestração (<code>run</code> / <code>status</code> / <code>reset</code>), testes em pytest e mapeamento documentado do pipeline inteiro para Azure Data Factory.</li>
</ul>
<p><a href="https://github.com/Mikhael-Groschitz/sqlserver-cdc-to-dw"><img src="https://img.shields.io/badge/Ver_reposit%C3%B3rio-181717?style=flat-square&logo=github&logoColor=white" /></a></p>
<p><img src="https://img.shields.io/badge/SQL_Server_2022-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white" /> <img src="https://img.shields.io/badge/CDC-008080?style=flat-square" /> <img src="https://img.shields.io/badge/T--SQL-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white" /> <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" /> <img src="https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white" /></p>
</td></tr>
<tr><td>
<h3>Lakehouse sobre a base pública de CNPJ da Receita Federal</h3>
<p>Processamento distribuído e orquestração sobre os dados da Receita Federal: Airflow e PySpark em Docker, camadas bronze/silver/gold em MinIO, Parquet particionado e checagens de qualidade.</p>
<p><a href="https://github.com/Mikhael-Groschitz/cnpj-lakehouse-spark-airflow"><img src="https://img.shields.io/badge/Ver_reposit%C3%B3rio-181717?style=flat-square&logo=github&logoColor=white" /></a></p>
<p><img src="https://img.shields.io/badge/Em_constru%C3%A7%C3%A3o-6E7681?style=flat-square" /> <img src="https://img.shields.io/badge/Airflow-017CEE?style=flat-square&logo=apacheairflow&logoColor=white" /> <img src="https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apachespark&logoColor=white" /> <img src="https://img.shields.io/badge/MinIO-C72E49?style=flat-square&logo=minio&logoColor=white" /></p>
</td></tr>
</table>

---

## Stack

<p><b>Linguagens</b><br>
<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/T--SQL-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white" /> <img src="https://img.shields.io/badge/SQL-4479A1?style=flat-square" /> <img src="https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white" /></p>

<p><b>Bancos e modelagem</b><br>
<img src="https://img.shields.io/badge/SQL_Server-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white" /> <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" /> <img src="https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white" /> <img src="https://img.shields.io/badge/Modelagem_Dimensional-4B0082?style=flat-square" /> <img src="https://img.shields.io/badge/SCD_Tipo_2-4B0082?style=flat-square" /> <img src="https://img.shields.io/badge/CDC-008080?style=flat-square" /></p>

<p><b>Cloud e orquestração</b><br>
<img src="https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" /> <img src="https://img.shields.io/badge/Data_Factory-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" /> <img src="https://img.shields.io/badge/Airflow-017CEE?style=flat-square&logo=apacheairflow&logoColor=white" /> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" /> <img src="https://img.shields.io/badge/Bicep-0078D4?style=flat-square&logo=microsoftazure&logoColor=white" /></p>

<p><b>BI, qualidade e engenharia</b><br>
<img src="https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=powerbi&logoColor=black" /> <img src="https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white" /> <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" /> <img src="https://img.shields.io/badge/Azure_DevOps-0080FF?style=flat-square&logo=azuredevops&logoColor=white" /></p>

---

## Formação

* **Pós-graduação Lato Sensu** — Arquitetura de Software, Ciência de Dados e Cybersecurity · PUCPR (2025 – 2026)
* **Tecnólogo em Análise e Desenvolvimento de Sistemas** · Anhanguera (2023 – 2025)

---

<div align="center">
<i>Aberto a conversas sobre vagas de Engenheiro de Dados.</i>
</div>
