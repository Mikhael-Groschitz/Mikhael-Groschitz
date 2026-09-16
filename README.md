# `mikhael@groschitz:~$ whoami`

```text
Mikhael Groschitz
Engenheiro de Dados
SQL Server · Azure · Python · Spark
```
<p align="left">
  <a href="https://www.linkedin.com/in/mikhael-groschitz/"><img src="https://img.shields.io/badge/LinkedIn-111820?style=for-the-badge&logo=linkedin&logoColor=39D353" alt="LinkedIn" /></a>
  <a href="https://mgroschitz.dev"><img src="https://img.shields.io/badge/Portf%C3%B3lio-111820?style=for-the-badge&logo=vercel&logoColor=39D353" alt="Portfólio" /></a>
  <a href="mailto:mgroschitz@gmail.com"><img src="https://img.shields.io/badge/Email-111820?style=for-the-badge&logo=gmail&logoColor=39D353" alt="Email" /></a>
</p>


<p align="left">
  <a href="https://readme-typing-svg.demolab.com">
    <img
      src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=17&pause=1200&color=39D353&vCenter=true&width=700&lines=%24+construindo+pipelines+de+dados+confi%C3%A1veis;%24+otimizando+T-SQL+em+escala;%24+modelando+dados+para+decis%C3%B5es+reais"
      alt="Áreas de atuação: pipelines de dados, otimização de T-SQL e modelagem"
    />
  </a>
</p>

---
## `cat sobre.md`

Construo e mantenho estruturas de dados que precisam funcionar em produção — de modelos e pipelines até a consulta crítica que não pode atrasar a operação.

Hoje sou responsável pela estrutura de dados de um **CRM jurídico em produção**: modelo relacional, views, índices, constraints, otimização de consultas e automações em Python. As implantações são feitas em conjunto com o time de DBA.

Antes disso, trabalhei com dados financeiros e contábeis, processando grandes volumes com SQL e Python, construindo dashboards no Power BI e desenvolvendo análises de anomalias, fluxo de caixa e rentabilidade.

```console
mikhael@data-engineering:~$ ./focus --list

[01] ingestão incremental
[02] modelagem dimensional
[03] orquestração e observabilidade
[04] qualidade de dados
[05] performance e custo em cloud

status: 5 áreas carregadas com sucesso
```

---

## `ls -la ./projetos`

<table>
  <tr>
    <td width="50%" valign="top">
      <h3><code>01</code> · Pipeline ELT de preços da ANP</h3>
      <p>
        <img alt="Azure Data Factory" src="https://img.shields.io/badge/Azure_Data_Factory-111820?style=flat-square&logo=microsoftazure&logoColor=39D353">
        <img alt="SQL Server" src="https://img.shields.io/badge/SQL_Server-111820?style=flat-square&logo=microsoftsqlserver&logoColor=39D353">
        <img alt="T-SQL" src="https://img.shields.io/badge/T--SQL-111820?style=flat-square&logo=microsoftsqlserver&logoColor=39D353">
        <img alt="Data Warehouse" src="https://img.shields.io/badge/Data_Warehouse-111820?style=flat-square&logoColor=39D353">
      </p>
      <p>Pipeline metadata-driven para ingerir e modelar <strong>20 anos de preços semanais</strong> da ANP: 219 arquivos CSV/ZIP processados em um Data Warehouse dimensional na Azure.</p>
      <p><strong>35,3 mi</strong> de linhas em estágio<br><strong>32,2 mi</strong> de linhas na fato<br><strong>~3 horas</strong> de carga histórica<br><strong>8 checks</strong> com severidade e log</p>
      <p><strong>O problema interessante:</strong> a carga tinha projeção de 15 horas. Inlining de UDF escalar, índice clusterizado, correção de conversão implícita que invalidava <code>seek</code> e SCD2 set-based reduziram a execução para 3 horas reais.</p>
      <p><strong>Arquitetura:</strong> quatro pipelines no ADF, sem Mapping Data Flows; transformações em stored procedures T-SQL e autenticação 100% Azure AD.</p>
    </td>
    <td width="50%" valign="top">
      <h3><code>02</code> · CDC para Data Warehouse</h3>
      <p>
        <img alt="SQL Server CDC" src="https://img.shields.io/badge/SQL_Server_CDC-111820?style=flat-square&logo=microsoftsqlserver&logoColor=39D353">
        <img alt="Python" src="https://img.shields.io/badge/Python-111820?style=flat-square&logo=python&logoColor=39D353">
        <img alt="T-SQL" src="https://img.shields.io/badge/T--SQL-111820?style=flat-square&logo=microsoftsqlserver&logoColor=39D353">
        <img alt="pytest" src="https://img.shields.io/badge/pytest-111820?style=flat-square&logo=pytest&logoColor=39D353">
      </p>
      <p>Um OLTP sintético recebe alterações contínuas. O CDC nativo captura as mudanças e um pipeline Python/T-SQL as transforma incrementalmente em um Data Warehouse dimensional.</p>
      <p><code>OLTP → CDC → LSN → transformação → SCD2 → fato → checks</code></p>
      <ul>
        <li>Watermark avança na mesma transação do <code>INSERT</code>.</li>
        <li>SCD2 com índice único filtrado.</li>
        <li>Exclusão lógica preserva a auditoria.</li>
        <li>Cinco checks, CLI e testes em pytest.</li>
        <li>Mapeamento para Azure Data Factory.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3><code>03</code> · Lakehouse de dados públicos</h3>
      <p>
        <img alt="Airflow" src="https://img.shields.io/badge/Airflow-111820?style=flat-square&logo=apacheairflow&logoColor=39D353">
        <img alt="PySpark" src="https://img.shields.io/badge/PySpark-111820?style=flat-square&logo=apachespark&logoColor=39D353">
        <img alt="Delta Lake" src="https://img.shields.io/badge/Delta_Lake-111820?style=flat-square&logo=databricks&logoColor=39D353">
        <img alt="MinIO" src="https://img.shields.io/badge/MinIO-111820?style=flat-square&logo=minio&logoColor=39D353">
        <img alt="DuckDB" src="https://img.shields.io/badge/DuckDB-111820?style=flat-square&logo=duckdb&logoColor=39D353">
        <img alt="Docker" src="https://img.shields.io/badge/Docker-111820?style=flat-square&logo=docker&logoColor=39D353">
      </p>
      <p>Lakehouse local sobre dados públicos de CNPJ da Receita Federal, organizado em bronze, silver e gold — sem depender de serviços pagos de nuvem.</p>
      <p><strong>~30 mi</strong> de estabelecimentos<br><strong>2h40</strong> de bronze a gold<br><strong>5.631 → 103</strong> arquivos<br><strong>99,99999%</strong> dos CNPJs validados<br><strong>30</strong> cenários em pytest</p>
      <p><strong>Otimização:</strong> reparticionamento por UF, validação com expressões de coluna em vez de UDF e broadcast join para domínios.</p>
      <p><strong>Confiabilidade:</strong> ingestão idempotente, manifesto, hash e quality gate antes da camada gold.</p>
    </td>
    <td width="50%" valign="top">
      <h3><code>04</code> · Streaming de propostas</h3>
      <p>
        <img alt="MongoDB" src="https://img.shields.io/badge/MongoDB-111820?style=flat-square&logo=mongodb&logoColor=39D353">
        <img alt="Kafka" src="https://img.shields.io/badge/Kafka-111820?style=flat-square&logo=apachekafka&logoColor=39D353">
        <img alt="Spark Structured Streaming" src="https://img.shields.io/badge/Spark_Streaming-111820?style=flat-square&logo=apachespark&logoColor=39D353">
        <img alt="Delta Lake" src="https://img.shields.io/badge/Delta_Lake-111820?style=flat-square&logo=databricks&logoColor=39D353">
        <img alt="Docker" src="https://img.shields.io/badge/Docker-111820?style=flat-square&logo=docker&logoColor=39D353">
      </p>
      <p>Change streams do MongoDB propagam propostas de crédito ao Kafka, materializadas em bronze, silver e gold por quatro jobs concorrentes.</p>
      <p><strong>Bug detectado pelos checks:</strong> 508 transições impossíveis expuseram a semântica do <code>updateLookup</code>. A sobreposição de <code>updatedFields</code> ao <code>fullDocument</code> reduziu o resultado a dois casos residuais conhecidos.</p>
      <p><strong>Gargalo removido:</strong> a troca de um <code>.isin()</code> com plano de 2,2 MiB por broadcast join tornou a execução independente do histórico.</p>
      <p><code>at-least-once · resume token · watermark · MERGE · reconciliação</code></p>
    </td>
  </tr>
</table>

---

## `./stack --list`

**LINGUAGENS**

![SQL](https://img.shields.io/badge/SQL-111820?style=for-the-badge&logo=databricks&logoColor=39D353)
![Python](https://img.shields.io/badge/Python-111820?style=for-the-badge&logo=python&logoColor=39D353)
![T-SQL](https://img.shields.io/badge/T--SQL-111820?style=for-the-badge&logo=microsoftsqlserver&logoColor=39D353)

**DADOS**

![SQL Server](https://img.shields.io/badge/SQL_Server-111820?style=for-the-badge&logo=microsoftsqlserver&logoColor=39D353)
![MongoDB](https://img.shields.io/badge/MongoDB-111820?style=for-the-badge&logo=mongodb&logoColor=39D353)
![Delta Lake](https://img.shields.io/badge/Delta_Lake-111820?style=for-the-badge&logo=databricks&logoColor=39D353)
![DuckDB](https://img.shields.io/badge/DuckDB-111820?style=for-the-badge&logo=duckdb&logoColor=39D353)
![MinIO](https://img.shields.io/badge/MinIO-111820?style=for-the-badge&logo=minio&logoColor=39D353)

**PROCESSAMENTO**

![Pandas](https://img.shields.io/badge/Pandas-111820?style=for-the-badge&logo=pandas&logoColor=39D353)
![NumPy](https://img.shields.io/badge/NumPy-111820?style=for-the-badge&logo=numpy&logoColor=39D353)
![PySpark](https://img.shields.io/badge/PySpark-111820?style=for-the-badge&logo=apachespark&logoColor=39D353)
![Spark Structured Streaming](https://img.shields.io/badge/Spark_Streaming-111820?style=for-the-badge&logo=apachespark&logoColor=39D353)

**ORQUESTRAÇÃO**

![Azure Data Factory](https://img.shields.io/badge/Azure_Data_Factory-111820?style=for-the-badge&logo=microsoftazure&logoColor=39D353)
![Airflow](https://img.shields.io/badge/Airflow-111820?style=for-the-badge&logo=apacheairflow&logoColor=39D353)
![Kafka](https://img.shields.io/badge/Kafka-111820?style=for-the-badge&logo=apachekafka&logoColor=39D353)

**CLOUD & PLATAFORMA**

![Azure](https://img.shields.io/badge/Azure-111820?style=for-the-badge&logo=microsoftazure&logoColor=39D353)
![Docker](https://img.shields.io/badge/Docker-111820?style=for-the-badge&logo=docker&logoColor=39D353)

**BI & QUALIDADE**

![Power BI](https://img.shields.io/badge/Power_BI-111820?style=for-the-badge&logo=powerbi&logoColor=39D353)
![pytest](https://img.shields.io/badge/pytest-111820?style=for-the-badge&logo=pytest&logoColor=39D353)
![Data Quality Gates](https://img.shields.io/badge/Data_Quality_Gates-111820?style=for-the-badge&logoColor=39D353)

**MODELAGEM**

![Dimensional](https://img.shields.io/badge/Dimensional-111820?style=for-the-badge&logoColor=39D353)
![SCD Tipo 2](https://img.shields.io/badge/SCD_Tipo_2-111820?style=for-the-badge&logoColor=39D353)
![CDC](https://img.shields.io/badge/CDC-111820?style=for-the-badge&logoColor=39D353)
![OLTP](https://img.shields.io/badge/OLTP-111820?style=for-the-badge&logoColor=39D353)
![Lakehouse](https://img.shields.io/badge/Lakehouse-111820?style=for-the-badge&logoColor=39D353)

---

## `cat formacao.txt`

```text
2025—2026  Pós-graduação em Arquitetura de Software,
           Ciência de Dados e Cybersecurity · PUCPR

2023—2025  Tecnólogo em Análise e Desenvolvimento de Sistemas
           Anhanguera
```

---

## `echo $STATUS`

```diff
+ aberto a conversas sobre oportunidades em Engenharia de Dados
```

<sub>Se algum dos problemas acima também aparece no seu ambiente, vamos conversar.</sub>
