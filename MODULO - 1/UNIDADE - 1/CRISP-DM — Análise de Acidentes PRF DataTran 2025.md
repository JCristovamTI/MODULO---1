# CRISP-DM — Análise de Acidentes de Trânsito PRF DataTran 2025

## 1. Entendimento do Negócio

### Contexto

Os acidentes de trânsito nas rodovias federais representam um importante problema de segurança viária. Este projeto utiliza os **Dados Abertos da Polícia Rodoviária Federal (PRF) — DataTran 2025** para identificar padrões relacionados à ocorrência e à gravidade dos acidentes.

### Problema

Identificar quais características dos acidentes estão mais associadas à ocorrência de vítimas fatais.

### Objetivo

Analisar os acidentes registrados pela PRF em 2025 e identificar padrões relacionados aos acidentes fatais, considerando fatores como:

- tipo de acidente;
- causa do acidente;
- horário;
- dia da semana;
- fase do dia;
- condição meteorológica;
- tipo e condição da pista;
- UF;
- município;
- quantidade de pessoas envolvidas;
- quantidade de veículos;
- número de mortos e feridos.

### Público-alvo

- Polícia Rodoviária Federal;
- gestores de segurança viária;
- analistas de dados;
- gestores públicos;
- profissionais envolvidos em prevenção de acidentes.

---

## 2. Entendimento dos Dados

### Fonte

**Dados Abertos da Polícia Rodoviária Federal — DataTran 2025.**

A base contém registros de acidentes ocorridos em rodovias federais durante o ano de 2025.

### Principais variáveis

| Variável | Descrição |
|---|---|
| `id` | Identificação do acidente |
| `data_inversa` | Data da ocorrência |
| `dia_semana` | Dia da semana |
| `horario` | Horário do acidente |
| `uf` | Unidade Federativa |
| `br` | Rodovia federal |
| `km` | Quilômetro da ocorrência |
| `municipio` | Município |
| `causa_acidente` | Causa do acidente |
| `tipo_acidente` | Tipo de acidente |
| `classificacao_acidente` | Classificação do acidente |
| `fase_dia` | Fase do dia |
| `condicao_metereologica` | Condição meteorológica |
| `tipo_pista` | Tipo de pista |
| `tracado_via` | Traçado da via |
| `uso_solo` | Uso do solo |
| `pessoas` | Pessoas envolvidas |
| `mortos` | Vítimas fatais |
| `feridos_leves` | Feridos leves |
| `feridos_graves` | Feridos graves |
| `veiculos` | Veículos envolvidos |

### Variável-alvo

Foi criada a variável `acidente_fatal` para identificar a ocorrência de vítimas fatais.

```python
df["acidente_fatal"] = np.where(df["mortos"] >= 1, 1, 0)
```

Interpretação:

- `1` → acidente fatal;
- `0` → acidente não fatal.

---

## 3. Preparação dos Dados

As seguintes etapas foram consideradas no tratamento da base:

### Limpeza

- Verificação de valores ausentes;
- Identificação de registros duplicados;
- Verificação de inconsistências;
- Padronização de variáveis categóricas;
- Tratamento de caracteres especiais;
- Verificação dos tipos de dados.

### Validação

Foram realizadas verificações para garantir que:

- a quantidade de registros fosse preservada após o tratamento;
- a variável `mortos` apresentasse valores coerentes;
- a variável `acidente_fatal` fosse criada corretamente;
- as categorias das variáveis fossem consistentes.

### Base Analítica

Após a preparação, os dados são organizados em uma base adequada para análises exploratórias, estatísticas e posteriormente para construção de indicadores e modelos.

---

## 4. Modelagem

A etapa de modelagem busca identificar relações entre as características dos acidentes e a ocorrência de mortes.

### Análises realizadas/propostas

#### Análise por UF

Identificar os estados com maior quantidade de acidentes e vítimas fatais.

#### Análise por tipo de acidente

Verificar quais tipos de acidentes apresentam maior frequência de mortes.

#### Análise temporal

Avaliar a distribuição dos acidentes fatais por:

- horário;
- dia da semana;
- fase do dia;
- período do ano.

#### Análise meteorológica

Verificar a distribuição dos acidentes fatais de acordo com as condições meteorológicas.

#### Análise das causas

Identificar as causas de acidentes mais frequentes entre os registros fatais.

#### Análise das características da via

Avaliar possíveis relações entre acidentes fatais e:

- tipo de pista;
- traçado da via;
- sentido da via;
- uso do solo.

---

## 5. Avaliação

A avaliação busca verificar se os resultados encontrados respondem ao problema definido inicialmente.

### Principais perguntas

1. Qual tipo de acidente está associado ao maior número de mortes?
2. Quais UFs apresentam maior quantidade de acidentes fatais?
3. Quais horários apresentam maior concentração de acidentes fatais?
4. Existe diferença entre acidentes ocorridos durante o dia e à noite?
5. Finais de semana apresentam maior concentração de acidentes fatais?
6. Quais condições meteorológicas aparecem com maior frequência nos acidentes fatais?
7. Quais são as principais causas associadas aos acidentes fatais?
8. Existe relação entre características da pista e ocorrência de mortes?
9. Quais municípios apresentam maior quantidade de acidentes fatais?

### Indicadores

Os principais indicadores utilizados na análise são:

- Total de acidentes;
- Total de acidentes fatais;
- Total de mortes;
- Total de feridos;
- Taxa de acidentes fatais;
- Média de mortos por acidente;
- Acidentes fatais por UF;
- Acidentes fatais por município;
- Acidentes fatais por horário;
- Acidentes fatais por dia da semana;
- Acidentes fatais por tipo de acidente;
- Acidentes fatais por causa.

---

## 6. Implantação

Os resultados da análise podem ser disponibilizados por meio de um **dashboard interativo**, permitindo a exploração dos dados por diferentes dimensões.

### Dashboard

O dashboard poderá apresentar:

- indicadores gerais;
- ranking de UFs;
- ranking de municípios;
- distribuição temporal;
- distribuição por tipo de acidente;
- distribuição por causa;
- distribuição por condição meteorológica;
- análise de acidentes fatais e não fatais;
- mapas e gráficos interativos.

### Ferramentas

O projeto pode utilizar:

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Google Colab**
- **Power BI**
- **GitHub**

---

## 7. Limitações

A análise possui algumas limitações importantes:

- Os dados representam acidentes registrados em **rodovias federais**;
- Não abrangem acidentes ocorridos exclusivamente em rodovias estaduais ou vias municipais;
- Algumas variáveis podem apresentar valores ausentes;
- Informações sobre causas podem depender do registro realizado no momento da ocorrência;
- Nem todos os fatores relacionados ao acidente são necessariamente identificados ou registrados;
- Os resultados representam os registros disponíveis na base da PRF e não todos os acidentes ocorridos no Brasil.

---

## 8. Resultado Esperado

Espera-se identificar padrões que permitam compreender melhor as características associadas aos acidentes fatais nas rodovias federais brasileiras em 2025.

A análise poderá auxiliar na identificação de:

- locais de maior ocorrência;
- períodos de maior risco;
- tipos de acidentes mais graves;
- principais causas registradas;
- condições associadas aos acidentes fatais.

Essas informações podem contribuir para análises de segurança viária e apoiar ações de prevenção, fiscalização e planejamento.

---

## Estrutura do Projeto

```text
PRF-DataTran-2025/
│
├── README.md
├── CRISP-DM.md
│
├── dados/
│   └── dados_abertos_prf-datatran2025.csv
│
├── notebooks/
│   └── analise_prf_2025.ipynb
│
├── scripts/
│   └── preparacao_dados.py
│
└── resultados/
    └── resultados_analise.csv
```

## Conclusão

A aplicação da metodologia **CRISP-DM** organiza o projeto desde a compreensão do problema até a disponibilização dos resultados.

A análise dos Dados Abertos da PRF/DataTran 2025 tem como foco principal compreender os fatores associados à ocorrência de acidentes fatais e transformar os registros de acidentes em informações úteis para análise de segurança viária.