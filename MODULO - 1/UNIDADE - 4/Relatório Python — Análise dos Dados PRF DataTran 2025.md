# Relatório Python — Análise dos Dados PRF DataTran 2025

## 1. Objetivo

O **Python** foi utilizado no projeto como uma das principais ferramentas para tratamento, preparação, exploração e análise dos **Dados Abertos da Polícia Rodoviária Federal (PRF) — DataTran 2025**.

A linguagem permitiu trabalhar com uma grande quantidade de registros, realizar procedimentos de limpeza, criar novas variáveis, calcular indicadores e preparar os dados para análises posteriores no Excel, SQL e Power BI.

O ambiente utilizado para execução dos códigos foi o **Google Colab**, utilizando principalmente as bibliotecas `Pandas`, `NumPy` e `Matplotlib`.

---

# 2. Relação com o CRISP-DM

A utilização do Python está relacionada principalmente às etapas:

| Etapa CRISP-DM | Utilização do Python |
|---|---|
| Entendimento dos Dados | Inspeção da estrutura e exploração da base |
| Preparação dos Dados | Limpeza e transformação |
| Modelagem | Criação de indicadores e variáveis |
| Avaliação | Análise dos resultados |
| Implantação | Exportação dos resultados para outras ferramentas |

---

# 3. Ambiente de Desenvolvimento

O projeto foi desenvolvido utilizando o **Google Colab**, permitindo executar os códigos Python diretamente no navegador.

### Principais bibliotecas

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

### Função das bibliotecas

**Pandas**

Utilizado para:

- carregar arquivos CSV;
- manipular DataFrames;
- filtrar registros;
- agrupar dados;
- calcular estatísticas;
- tratar valores ausentes;
- exportar resultados.

**NumPy**

Utilizado principalmente para:

- operações numéricas;
- criação de variáveis condicionais;
- tratamento de valores;
- cálculos estatísticos.

**Matplotlib**

Utilizado para:

- criação de gráficos;
- visualização dos dados;
- análise exploratória.

---

# 4. Importação dos Dados

Os dados da PRF DataTran 2025 foram carregados para um DataFrame utilizando o Pandas.

Exemplo:

```python
df = pd.read_csv(
    "dados_abertos_prf-datatran2025.csv",
    sep=";",
    encoding="latin1",
    low_memory=False
)
```

Após a importação, foram realizadas verificações para confirmar se os dados foram carregados corretamente.

---

# 5. Conhecimento da Base

Para verificar a quantidade de registros e colunas:

```python
df.shape
```

Também foram utilizadas funções para visualizar os primeiros registros:

```python
df.head()
```

E para verificar os tipos de dados:

```python
df.info()
```

Essas verificações permitiram compreender a estrutura inicial da base.

---

# 6. Análise das Colunas

As colunas disponíveis foram verificadas por meio de:

```python
df.columns
```

Essa etapa foi importante para identificar as variáveis que seriam utilizadas nas análises.

Entre as principais variáveis estão:

- `uf`;
- `municipio`;
- `data_inversa`;
- `dia_semana`;
- `horario`;
- `causa_acidente`;
- `tipo_acidente`;
- `fase_dia`;
- `condicao_metereologica`;
- `tipo_pista`;
- `pessoas`;
- `mortos`;
- `feridos_leves`;
- `feridos_graves`;
- `veiculos`.

---

# 7. Verificação de Valores Ausentes

Foi realizada uma análise dos valores ausentes utilizando:

```python
df.isnull().sum()
```

Essa etapa permitiu identificar quais colunas apresentavam informações faltantes.

Os valores ausentes foram avaliados antes da utilização das variáveis nas análises, evitando conclusões incorretas.

---

# 8. Verificação de Dados Duplicados

Também foi realizada uma verificação de registros duplicados:

```python
df.duplicated().sum()
```

Essa análise é importante porque registros duplicados podem alterar a quantidade real de acidentes e distorcer os indicadores.

---

# 9. Criação da Variável Acidente Fatal

Uma das principais transformações realizadas em Python foi a criação da variável `acidente_fatal`.

A regra utilizada foi:

```python
df["acidente_fatal"] = np.where(
    df["mortos"] >= 1,
    1,
    0
)
```

### Interpretação

```text
1 → Acidente fatal
0 → Acidente não fatal
```

A variável foi criada para facilitar a comparação entre acidentes com e sem vítimas fatais.

---

# 10. Validação da Variável-Alvo

Após a criação da variável, foi realizada uma contagem:

```python
validacao_alvo = df["acidente_fatal"].value_counts()
print(validacao_alvo)
```

Também pode ser calculado o percentual:

```python
percentual = (
    df["acidente_fatal"]
    .value_counts(normalize=True) * 100
)

print(percentual)
```

Essa etapa permite verificar a distribuição entre acidentes fatais e não fatais.

---

# 11. Análise de Acidentes por UF

O Pandas foi utilizado para agrupar os acidentes por estado:

```python
acidentes_uf = (
    df.groupby("uf")
      .size()
      .sort_values(ascending=False)
)

display(acidentes_uf)
```

Essa análise permite identificar as UFs com maior quantidade de registros.

---

# 12. Análise de Mortes por UF

Para calcular o total de vítimas fatais por estado:

```python
mortos_uf = (
    df.groupby("uf")["mortos"]
      .sum()
      .sort_values(ascending=False)
)

display(mortos_uf)
```

Esse indicador permite comparar a quantidade de mortes entre as diferentes UFs.

---

# 13. Análise por Tipo de Acidente

O Python também foi utilizado para identificar os tipos de acidentes mais frequentes.

```python
tipo_acidente = (
    df.groupby("tipo_acidente")
      .agg(
          acidentes=("id", "count"),
          mortos=("mortos", "sum")
      )
      .sort_values("mortos", ascending=False)
)

display(tipo_acidente)
```

Essa tabela permite comparar a frequência dos acidentes com a quantidade de mortes.

---

# 14. Análise por Dia da Semana

Foi realizada uma análise utilizando a variável `dia_semana`.

```python
dia_semana = (
    df.groupby("dia_semana")
      .agg(
          acidentes=("id", "count"),
          mortos=("mortos", "sum")
      )
)

display(dia_semana)
```

O objetivo é verificar como os acidentes estão distribuídos ao longo da semana.

---

# 15. Análise por Fase do Dia

A variável `fase_dia` também foi utilizada:

```python
fase_dia = (
    df.groupby("fase_dia")
      .agg(
          acidentes=("id", "count"),
          mortos=("mortos", "sum")
      )
      .sort_values("acidentes", ascending=False)
)

display(fase_dia)
```

Essa análise permite comparar períodos como dia, noite, amanhecer e anoitecer, conforme as categorias disponíveis na base.

---

# 16. Análise por Condição Meteorológica

A distribuição dos acidentes também foi analisada de acordo com a condição meteorológica:

```python
clima = (
    df.groupby("condicao_metereologica")
      .agg(
          acidentes=("id", "count"),
          mortos=("mortos", "sum")
      )
      .sort_values("acidentes", ascending=False)
)

display(clima)
```

O objetivo é identificar como os acidentes estão distribuídos entre as diferentes condições registradas.

---

# 17. Análise por Causa

As causas registradas foram agrupadas utilizando o Pandas:

```python
causas = (
    df.groupby("causa_acidente")
      .agg(
          acidentes=("id", "count"),
          mortos=("mortos", "sum")
      )
      .sort_values("mortos", ascending=False)
)

display(causas)
```

Essa análise ajuda a identificar as causas com maior quantidade de ocorrências e mortes.

---

# 18. Análise por Município

Para criar um ranking dos municípios:

```python
municipios = (
    df.groupby(["uf", "municipio"])
      .agg(
          acidentes=("id", "count"),
          mortos=("mortos", "sum")
      )
      .sort_values("acidentes", ascending=False)
)

display(municipios.head(20))
```

O resultado apresenta os municípios com maior concentração de acidentes.

---

# 19. Criação de Indicadores

O Python também foi utilizado para calcular indicadores gerais da base.

### Total de acidentes

```python
total_acidentes = len(df)
```

### Total de mortes

```python
total_mortos = df["mortos"].sum()
```

### Total de veículos

```python
total_veiculos = df["veiculos"].sum()
```

### Total de pessoas

```python
total_pessoas = df["pessoas"].sum()
```

### Total de feridos leves

```python
total_feridos_leves = df["feridos_leves"].sum()
```

### Total de feridos graves

```python
total_feridos_graves = df["feridos_graves"].sum()
```

---

# 20. Taxa de Acidentes Fatais

A taxa de acidentes fatais pode ser calculada utilizando a variável criada:

```python
taxa_fatal = df["acidente_fatal"].mean() * 100

print(f"Taxa de acidentes fatais: {taxa_fatal:.2f}%")
```

Como `acidente_fatal` possui valores 0 e 1, a média representa a proporção de acidentes fatais.

---

# 21. Visualização dos Dados

O Matplotlib foi utilizado para criar gráficos e facilitar a interpretação dos resultados.

Exemplo de gráfico de acidentes por UF:

```python
acidentes_uf.plot(
    kind="bar",
    figsize=(12, 6)
)

plt.title("Acidentes por UF — PRF DataTran 2025")
plt.xlabel("UF")
plt.ylabel("Quantidade de acidentes")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

Os gráficos permitem identificar visualmente padrões e diferenças entre categorias.

---

# 22. Tabelas de Resultado

Após o tratamento e análise, os resultados foram organizados em tabelas.

Exemplo:

```python
resumo_final = pd.DataFrame([
    {
        "item": "linhas_base_analitica",
        "valor": len(df)
    },
    {
        "item": "colunas_base_analitica",
        "valor": df.shape[1]
    },
    {
        "item": "total_acidentes",
        "valor": len(df)
    },
    {
        "item": "total_mortos",
        "valor": df["mortos"].sum()
    }
])

display(resumo_final)
```

Essas tabelas podem ser utilizadas posteriormente no Excel, Power BI ou outros sistemas de visualização.

---

# 23. Exportação dos Resultados

Os resultados gerados pelo Python podem ser exportados para CSV:

```python
resultado.to_csv(
    "resultado_prf_2025.csv",
    index=False,
    encoding="utf-8-sig"
)
```

Também é possível exportar para Excel:

```python
resultado.to_excel(
    "resultado_prf_2025.xlsx",
    index=False
)
```

Essa integração permite utilizar os resultados produzidos no Python em outras etapas do projeto.

---

# 24. Fluxo de Trabalho

O processo realizado com Python pode ser representado da seguinte maneira:

```text
Dados Abertos PRF DataTran 2025
              ↓
          Importação
              ↓
         Pandas / NumPy
              ↓
      Análise da estrutura
              ↓
       Limpeza dos dados
              ↓
      Tratamento dos dados
              ↓
    Criação de acidente_fatal
              ↓
       Análise exploratória
              ↓
      Criação de indicadores
              ↓
          Gráficos
              ↓
       Tabelas de resultados
              ↓
       Excel / Power BI / SQL
```

---

# 25. Integração com as Outras Ferramentas

O Python não foi utilizado de forma isolada.

As ferramentas foram integradas ao longo do projeto:

| Ferramenta | Função |
|---|---|
| Python | Tratamento e análise |
| Pandas | Manipulação dos dados |
| NumPy | Operações e transformações |
| Matplotlib | Visualização |
| SQL | Consultas e agregações |
| Excel | Tabelas e indicadores |
| Power BI | Dashboard |
| Google Colab | Ambiente de execução |
| GitHub | Versionamento e documentação |

---

# 26. Contribuição para o Projeto

A utilização do Python possibilitou automatizar diversas tarefas que seriam trabalhosas quando realizadas manualmente.

Entre as principais contribuições estão:

- tratamento de grandes volumes de dados;
- criação de variáveis;
- identificação de valores ausentes;
- identificação de duplicidades;
- agrupamento de informações;
- cálculo de indicadores;
- análise de acidentes fatais;
- criação de gráficos;
- geração de tabelas;
- exportação dos resultados.

---

# 27. Limitações

A análise realizada com Python está limitada às informações disponíveis nos Dados Abertos da PRF.

Algumas variáveis podem apresentar:

- valores ausentes;
- inconsistências;
- diferentes categorias;
- informações não preenchidas;
- limitações relacionadas ao registro da ocorrência.

Além disso, os dados representam acidentes registrados em **rodovias federais**, não abrangendo necessariamente todos os acidentes ocorridos em vias estaduais e municipais.

Os resultados também devem ser interpretados como associações encontradas nos dados, não necessariamente como relações de causa e efeito.

---

# 28. Conclusão

O Python foi uma ferramenta fundamental no desenvolvimento da análise dos Dados Abertos da PRF/DataTran 2025.

Por meio de bibliotecas como **Pandas, NumPy e Matplotlib**, foi possível realizar o carregamento, tratamento, transformação, exploração e análise dos dados.

A criação da variável `acidente_fatal` permitiu direcionar a análise para a identificação de características relacionadas aos acidentes com vítimas fatais.

Os resultados produzidos em Python foram utilizados como apoio às análises realizadas no **SQL e Excel**, além de servirem como base para a construção de indicadores e visualizações.

Dessa forma, o Python contribuiu diretamente para as etapas de **Entendimento dos Dados, Preparação, Modelagem, Avaliação e Implantação** da metodologia CRISP-DM.

---

## Estrutura do Projeto no GitHub

```text
PRF-DataTran-2025/
│
├── README.md
├── CRISP-DM.md
├── RELATORIO-EXCEL.md
├── RELATORIO-SQL.md
├── RELATORIO-PYTHON.md
│
├── dados/
│   └── dados_abertos_prf-datatran2025.csv
│
├── notebooks/
│   └── analise_prf_2025.ipynb
│
├── python/
│   ├── preparacao_dados.py
│   ├── analise_exploratoria.py
│   └── indicadores.py
│
├── sql/
│   ├── consultas_exploratorias.sql
│   ├── consultas_bivariadas.sql
│   └── views.sql
│
└── resultados/
    ├── tabelas_excel/
    ├── resultados_sql/
    └── resultados_python/
```