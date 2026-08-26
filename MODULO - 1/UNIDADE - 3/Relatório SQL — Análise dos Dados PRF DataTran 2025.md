# Relatório SQL — Análise dos Dados PRF DataTran 2025

## 1. Objetivo

O SQL foi utilizado como uma das ferramentas de análise dos **Dados Abertos da Polícia Rodoviária Federal (PRF) — DataTran 2025**.

A utilização de SQL permitiu realizar consultas, filtros, agrupamentos e análises sobre os registros de acidentes, transformando os dados brutos em informações agregadas para apoiar a análise de acidentes fatais.

As consultas SQL também foram utilizadas como etapa de validação dos resultados obtidos no Python, Pandas e Excel.

---

# 2. Relação com o CRISP-DM

A utilização do SQL está relacionada principalmente às seguintes etapas:

| Etapa CRISP-DM | Utilização do SQL |
|---|---|
| Entendimento dos Dados | Exploração da estrutura e dos registros |
| Preparação dos Dados | Filtros e tratamento das informações |
| Modelagem | Agrupamentos e cruzamentos de variáveis |
| Avaliação | Geração e comparação de indicadores |
| Implantação | Criação de consultas e visões para o dashboard |

---

# 3. Estrutura do Banco de Dados

Os dados da PRF foram organizados em uma tabela para possibilitar consultas SQL.

Uma estrutura simplificada utilizada na análise contém campos como:

```text id="c8mkw5"
id
data_inversa
dia_semana
horario
uf
br
km
municipio
causa_acidente
tipo_acidente
classificacao_acidente
fase_dia
sentido_via
condicao_metereologica
tipo_pista
tracado_via
uso_solo
pessoas
mortos
feridos_leves
feridos_graves
veiculos
```

A estrutura permite realizar consultas utilizando variáveis relacionadas à localização, tempo, características da via e gravidade dos acidentes.

---

# 4. Consultas de Exploração

Inicialmente, foram realizadas consultas para conhecer a quantidade de registros disponíveis.

### Total de acidentes

```sql
SELECT COUNT(*) AS total_acidentes
FROM acidentes;
```

Essa consulta permite verificar a quantidade total de registros armazenados na tabela.

---

# 5. Acidentes por UF

Foi realizada uma consulta para identificar os estados com maior quantidade de acidentes.

```sql
SELECT
    uf,
    COUNT(*) AS total_acidentes
FROM acidentes
GROUP BY uf
ORDER BY total_acidentes DESC;
```

### Objetivo

Identificar a distribuição dos acidentes entre as Unidades Federativas.

Essa informação pode ser utilizada para criar rankings e gráficos comparativos.

---

# 6. Mortes por UF

Para analisar a distribuição das vítimas fatais:

```sql
SELECT
    uf,
    SUM(mortos) AS total_mortos
FROM acidentes
GROUP BY uf
ORDER BY total_mortos DESC;
```

### Objetivo

Identificar os estados com maior número de vítimas fatais registradas.

---

# 7. Acidentes por Município

Foi realizada uma consulta para identificar os municípios com maior número de ocorrências.

```sql
SELECT
    uf,
    municipio,
    COUNT(*) AS total_acidentes
FROM acidentes
GROUP BY uf, municipio
ORDER BY total_acidentes DESC
LIMIT 20;
```

### Objetivo

Criar um ranking dos 20 municípios com maior quantidade de acidentes registrados.

---

# 8. Acidentes Fatais

A variável `acidente_fatal` foi criada a partir da quantidade de mortos.

A regra utilizada foi:

```text id="jzvrrj"
mortos >= 1 → acidente fatal
mortos = 0  → acidente não fatal
```

Em SQL, a classificação pode ser realizada com:

```sql
SELECT
    id,
    CASE
        WHEN mortos >= 1 THEN 1
        ELSE 0
    END AS acidente_fatal
FROM acidentes;
```

Essa classificação permite separar os acidentes com vítimas fatais dos acidentes sem mortes.

---

# 9. Quantidade de Acidentes Fatais

Para contabilizar os acidentes fatais:

```sql
SELECT
    COUNT(*) AS acidentes_fatais
FROM acidentes
WHERE mortos >= 1;
```

### Objetivo

Obter a quantidade total de acidentes que resultaram em pelo menos uma vítima fatal.

---

# 10. Acidentes Fatais por UF

Uma das principais análises foi a distribuição dos acidentes fatais por estado.

```sql
SELECT
    uf,
    COUNT(*) AS acidentes_fatais
FROM acidentes
WHERE mortos >= 1
GROUP BY uf
ORDER BY acidentes_fatais DESC;
```

Essa consulta permite identificar as UFs com maior quantidade de acidentes fatais.

---

# 11. Acidentes Fatais por Tipo de Acidente

Para identificar os tipos de acidentes relacionados às mortes:

```sql
SELECT
    tipo_acidente,
    COUNT(*) AS acidentes_fatais,
    SUM(mortos) AS total_mortos
FROM acidentes
WHERE mortos >= 1
GROUP BY tipo_acidente
ORDER BY total_mortos DESC;
```

### Objetivo

Identificar quais tipos de ocorrência apresentam maior quantidade de vítimas fatais.

---

# 12. Acidentes por Dia da Semana

Foi realizada uma análise temporal utilizando o dia da semana.

```sql
SELECT
    dia_semana,
    COUNT(*) AS total_acidentes,
    SUM(mortos) AS total_mortos
FROM acidentes
GROUP BY dia_semana
ORDER BY total_acidentes DESC;
```

Essa consulta permite comparar a frequência dos acidentes e das mortes entre os diferentes dias da semana.

---

# 13. Acidentes por Fase do Dia

A variável `fase_dia` também foi utilizada para analisar a distribuição das ocorrências.

```sql
SELECT
    fase_dia,
    COUNT(*) AS total_acidentes,
    SUM(mortos) AS total_mortos
FROM acidentes
GROUP BY fase_dia
ORDER BY total_acidentes DESC;
```

### Objetivo

Verificar a distribuição dos acidentes entre diferentes períodos do dia.

---

# 14. Condição Meteorológica

Foi realizada uma consulta relacionando as condições meteorológicas com os acidentes.

```sql
SELECT
    condicao_metereologica,
    COUNT(*) AS total_acidentes,
    SUM(mortos) AS total_mortos
FROM acidentes
GROUP BY condicao_metereologica
ORDER BY total_acidentes DESC;
```

Essa análise permite observar a quantidade de acidentes e mortes registrada em cada condição meteorológica.

---

# 15. Causas dos Acidentes

As principais causas registradas foram analisadas por meio de agrupamento.

```sql
SELECT
    causa_acidente,
    COUNT(*) AS total_acidentes,
    SUM(mortos) AS total_mortos
FROM acidentes
GROUP BY causa_acidente
ORDER BY total_acidentes DESC;
```

### Objetivo

Identificar as causas com maior quantidade de ocorrências e mortes registradas.

---

# 16. Tipo de Pista

Também foi realizada uma análise considerando o tipo de pista.

```sql
SELECT
    tipo_pista,
    COUNT(*) AS total_acidentes,
    SUM(mortos) AS total_mortos
FROM acidentes
GROUP BY tipo_pista
ORDER BY total_acidentes DESC;
```

Essa consulta permite comparar a quantidade de acidentes e mortes entre os diferentes tipos de pista.

---

# 17. Consulta Bivariada

O SQL também foi utilizado para cruzar duas variáveis e analisar possíveis relações.

Exemplo:

```sql
SELECT
    fase_dia,
    CASE
        WHEN mortos >= 1 THEN 'Fatal'
        ELSE 'Não Fatal'
    END AS classificacao,
    COUNT(*) AS quantidade
FROM acidentes
GROUP BY
    fase_dia,
    classificacao
ORDER BY
    fase_dia,
    quantidade DESC;
```

### Objetivo

Comparar acidentes fatais e não fatais de acordo com a fase do dia.

Esse tipo de consulta é importante para encontrar padrões que não aparecem em uma análise de apenas uma variável.

---

# 18. Visão Consolidada

Foi criada a ideia de uma visão agregada para reunir informações importantes em uma única estrutura.

Exemplo:

```sql
CREATE VIEW visao_acidentes AS
SELECT
    uf,
    COUNT(*) AS total_acidentes,
    SUM(mortos) AS total_mortos,
    SUM(feridos_leves) AS total_feridos_leves,
    SUM(feridos_graves) AS total_feridos_graves,
    SUM(veiculos) AS total_veiculos
FROM acidentes
GROUP BY uf;
```

A `VIEW` pode ser utilizada posteriormente para alimentar relatórios, tabelas ou dashboards.

---

# 19. Validação dos Dados

As consultas SQL também foram utilizadas para validar os resultados obtidos em outras ferramentas.

O fluxo de validação foi:

```text id="qz8w1u"
Dados PRF 2025
      ↓
     SQL
      ↓
Consultas e agregações
      ↓
     Excel
      ↓
Tabelas e indicadores
      ↓
Python / Pandas
      ↓
Validação dos resultados
```

A comparação entre as ferramentas ajuda a identificar possíveis erros de contagem, filtros incorretos ou problemas de tratamento dos dados.

---

# 20. SQL e o Dashboard

Os resultados das consultas SQL podem ser utilizados como fonte para construção de dashboards.

Entre os indicadores que podem ser disponibilizados estão:

- Total de acidentes;
- Total de mortes;
- Total de feridos;
- Acidentes fatais;
- Acidentes não fatais;
- Acidentes por UF;
- Mortes por UF;
- Acidentes por município;
- Acidentes por tipo;
- Acidentes por causa;
- Acidentes por horário;
- Acidentes por fase do dia;
- Acidentes por condição meteorológica.

---

# 21. Ferramentas Utilizadas

Durante o projeto foram utilizadas diferentes ferramentas para tratamento e análise dos dados:

- **SQL** — consultas, filtros, agrupamentos e agregações;
- **SQLite** — armazenamento e consulta dos dados;
- **Python** — tratamento e análise exploratória;
- **Pandas** — manipulação dos DataFrames;
- **Google Colab** — execução dos códigos Python;
- **Excel** — tabelas, indicadores e gráficos;
- **Power BI** — visualização e dashboard;
- **GitHub** — versionamento e documentação do projeto.

---

# 22. Conclusão

A utilização de SQL nos Dados Abertos da PRF/DataTran 2025 possibilitou realizar consultas estruturadas e análises agregadas sobre os acidentes registrados nas rodovias federais.

Por meio de comandos como `SELECT`, `WHERE`, `GROUP BY`, `ORDER BY`, `COUNT()`, `SUM()`, `CASE` e `CREATE VIEW`, foi possível transformar os registros individuais em indicadores úteis para análise.

O SQL também complementou as análises realizadas no Python e Excel, permitindo validar resultados e criar bases consolidadas para utilização em dashboards.

Dessa forma, o SQL representa uma etapa importante do projeto, contribuindo para as fases de **Entendimento dos Dados, Preparação, Modelagem, Avaliação e Implantação** da metodologia CRISP-DM.

---

## Estrutura sugerida no GitHub

```text
PRF-DataTran-2025/
│
├── README.md
├── CRISP-DM.md
├── RELATORIO-EXCEL.md
├── RELATORIO-SQL.md
│
├── dados/
│   └── dados_abertos_prf-datatran2025.csv
│
├── sql/
│   ├── consultas_exploratorias.sql
│   ├── consultas_bivariadas.sql
│   └── views.sql
│
├── notebooks/
│   └── analise_prf_2025.ipynb
│
└── resultados/
    ├── tabelas_excel/
    └── resultados_sql/
```