# Relatório das Tabelas Excel — PRF DataTran 2025

## 1. Objetivo

Este relatório apresenta as tabelas desenvolvidas no **Excel** a partir dos Dados Abertos da **Polícia Rodoviária Federal (PRF) — DataTran 2025**.

As tabelas foram utilizadas para organizar, resumir e analisar os registros de acidentes de trânsito, servindo como apoio às etapas do **CRISP-DM** e à construção dos indicadores utilizados no projeto.

O objetivo é transformar os dados brutos em informações estruturadas que permitam identificar padrões relacionados à quantidade de acidentes, vítimas fatais, feridos, localização, período e características das ocorrências.

---

# 2. Relação com o CRISP-DM

As tabelas Excel estão principalmente relacionadas às seguintes etapas:

| Etapa CRISP-DM | Utilização das tabelas Excel |
|---|---|
| Entendimento do Negócio | Definição dos indicadores e perguntas da análise |
| Entendimento dos Dados | Organização e exploração inicial dos registros |
| Preparação dos Dados | Tratamento, validação e criação de variáveis |
| Modelagem | Cruzamento e agregação das informações |
| Avaliação | Comparação dos resultados e identificação de padrões |
| Implantação | Apresentação dos resultados em tabelas e dashboard |

---

# 3. Tabela de Base dos Acidentes

A primeira tabela contém os registros utilizados como base para a análise.

### Principais campos

- ID do acidente;
- Data;
- Dia da semana;
- Horário;
- UF;
- Rodovia;
- KM;
- Município;
- Causa do acidente;
- Tipo de acidente;
- Classificação;
- Fase do dia;
- Condição meteorológica;
- Tipo de pista;
- Traçado da via;
- Uso do solo;
- Pessoas;
- Veículos;
- Mortos;
- Feridos leves;
- Feridos graves.

### Objetivo

Essa tabela representa a **base principal de análise** e serve como origem para as demais tabelas e indicadores.

### CRISP-DM

**Entendimento dos Dados → Preparação dos Dados**

---

# 4. Tabela de Acidentes por UF

Essa tabela apresenta a quantidade de acidentes registrados em cada Unidade Federativa.

### Indicadores

- UF;
- Quantidade de acidentes;
- Percentual sobre o total.

### Objetivo

Identificar os estados que apresentam maior concentração de acidentes.

### Exemplo de estrutura

| UF | Acidentes | % do Total |
|---|---:|---:|
| SP | — | — |
| MG | — | — |
| PR | — | — |
| BA | — | — |
| PE | — | — |

Os valores devem ser preenchidos diretamente a partir da base analisada.

### CRISP-DM

**Entendimento dos Dados → Avaliação**

---

# 5. Tabela de Mortes por UF

Essa tabela apresenta o número de vítimas fatais por estado.

### Indicadores

- UF;
- Total de mortos;
- Número de acidentes fatais;
- Taxa de acidentes fatais.

### Objetivo

Identificar quais estados apresentam maior quantidade de vítimas fatais e comparar a gravidade dos acidentes entre as UFs.

### CRISP-DM

**Modelagem → Avaliação**

---

# 6. Tabela de Acidentes Fatais e Não Fatais

Foi criada uma classificação dos acidentes utilizando a variável `acidente_fatal`.

### Regra

```text
mortos >= 1 → Acidente Fatal
mortos = 0  → Acidente Não Fatal
```

### Indicadores

- Acidentes fatais;
- Acidentes não fatais;
- Total de acidentes;
- Percentual de cada categoria.

### Objetivo

Permitir a comparação entre ocorrências com e sem vítimas fatais.

### CRISP-DM

**Preparação dos Dados → Avaliação**

---

# 7. Tabela de Mortes por Tipo de Acidente

Essa tabela cruza o tipo de acidente com a quantidade de vítimas fatais.

### Exemplos de variáveis

- Tipo de acidente;
- Quantidade de acidentes;
- Acidentes fatais;
- Total de mortos;
- Média de mortos por acidente.

### Objetivo

Identificar quais tipos de ocorrência apresentam maior gravidade.

### CRISP-DM

**Modelagem → Avaliação**

---

# 8. Tabela de Acidentes por Dia da Semana

Essa tabela apresenta a distribuição dos acidentes de acordo com o dia da semana.

### Indicadores

- Dia da semana;
- Total de acidentes;
- Acidentes fatais;
- Mortes;
- Percentual de acidentes fatais.

### Objetivo

Verificar se determinados dias apresentam maior concentração de acidentes ou de ocorrências fatais.

### CRISP-DM

**Entendimento dos Dados → Avaliação**

---

# 9. Tabela de Acidentes por Horário

Essa tabela organiza os acidentes de acordo com o horário de ocorrência.

### Indicadores

- Horário;
- Total de acidentes;
- Acidentes fatais;
- Mortes.

### Objetivo

Identificar períodos do dia com maior frequência de acidentes e mortes.

Também permite verificar se os acidentes fatais estão concentrados em determinados horários.

### CRISP-DM

**Modelagem → Avaliação**

---

# 10. Tabela por Fase do Dia

Os registros são agrupados de acordo com a fase do dia.

### Exemplos

- Pleno dia;
- Anoitecer;
- Pleno noite;
- Amanhecer.

### Indicadores

- Total de acidentes;
- Acidentes fatais;
- Mortes;
- Percentual de acidentes fatais.

### Objetivo

Avaliar possíveis diferenças entre acidentes ocorridos durante períodos claros e escuros.

### CRISP-DM

**Modelagem → Avaliação**

---

# 11. Tabela por Condição Meteorológica

Essa tabela apresenta os acidentes agrupados pelas condições meteorológicas registradas.

### Indicadores

- Condição meteorológica;
- Total de acidentes;
- Acidentes fatais;
- Mortes;
- Percentual.

### Objetivo

Verificar como os acidentes estão distribuídos entre diferentes condições climáticas.

É importante interpretar esses resultados com cautela, pois a frequência de uma condição meteorológica não significa necessariamente que ela seja a causa do acidente.

### CRISP-DM

**Entendimento dos Dados → Avaliação**

---

# 12. Tabela por Causa do Acidente

Essa tabela apresenta as principais causas registradas nos acidentes.

### Indicadores

- Causa;
- Total de acidentes;
- Acidentes fatais;
- Mortes;
- Percentual.

### Objetivo

Identificar quais causas aparecem com maior frequência e quais apresentam maior quantidade de ocorrências fatais.

### CRISP-DM

**Modelagem → Avaliação**

---

# 13. Tabela por Tipo de Pista

Os acidentes são agrupados de acordo com o tipo de pista.

### Indicadores

- Tipo de pista;
- Total de acidentes;
- Acidentes fatais;
- Mortes;
- Percentual de acidentes fatais.

### Objetivo

Avaliar a distribuição dos acidentes de acordo com as características da pista.

### CRISP-DM

**Modelagem → Avaliação**

---

# 14. Tabela por Município

Essa tabela apresenta um ranking dos municípios com maior quantidade de acidentes.

### Indicadores

- Município;
- UF;
- Total de acidentes;
- Acidentes fatais;
- Mortes.

### Objetivo

Identificar áreas com maior concentração de ocorrências e possíveis pontos de atenção.

### CRISP-DM

**Avaliação → Implantação**

---

# 15. Tabela de Indicadores Gerais

Uma tabela consolidada foi utilizada para apresentar os principais números da base.

### Indicadores

| Indicador | Resultado |
|---|---:|
| Total de acidentes | — |
| Total de acidentes fatais | — |
| Total de mortos | — |
| Total de feridos leves | — |
| Total de feridos graves | — |
| Total de pessoas envolvidas | — |
| Total de veículos | — |
| Taxa de acidentes fatais | — |

Essa tabela serve como resumo executivo da análise.

### CRISP-DM

**Avaliação → Implantação**

---

# 16. Utilização do Excel

O Excel foi utilizado como ferramenta de apoio para:

- organização dos dados;
- aplicação de filtros;
- criação de tabelas;
- cálculos estatísticos;
- criação de indicadores;
- agrupamento de informações;
- comparação entre categorias;
- construção de gráficos;
- validação dos resultados obtidos no Python/Google Colab.

As tabelas também podem ser utilizadas como fonte para construção de um dashboard.

---

# 17. Integração com Python e Google Colab

O Excel complementa a análise realizada no Python/Google Colab.

O fluxo utilizado no projeto pode ser representado da seguinte forma:

```text
Dados Abertos PRF 2025
        ↓
Importação dos dados
        ↓
Python / Pandas
        ↓
Limpeza e preparação
        ↓
Criação da variável acidente_fatal
        ↓
Análise exploratória
        ↓
Tabelas agregadas
        ↓
Excel
        ↓
Indicadores e gráficos
        ↓
Dashboard / Apresentação dos resultados
```

---

# 18. Indicadores Utilizados no Projeto

As tabelas Excel permitem gerar indicadores importantes para o projeto:

### Indicadores de ocorrência

- Total de acidentes;
- Acidentes por UF;
- Acidentes por município;
- Acidentes por rodovia;
- Acidentes por tipo.

### Indicadores de gravidade

- Total de mortos;
- Total de feridos;
- Acidentes fatais;
- Taxa de acidentes fatais;
- Mortes por tipo de acidente.

### Indicadores temporais

- Acidentes por mês;
- Acidentes por dia da semana;
- Acidentes por horário;
- Acidentes por fase do dia.

### Indicadores relacionados às condições da ocorrência

- Condição meteorológica;
- Tipo de pista;
- Traçado da via;
- Causa do acidente.

---

# 19. Conclusão

As tabelas desenvolvidas no Excel representam uma etapa importante do projeto de análise dos Dados Abertos da PRF/DataTran 2025.

Elas permitem transformar a base original em informações agregadas e mais fáceis de interpretar, facilitando a identificação de padrões relacionados à ocorrência e à gravidade dos acidentes.

A utilização das tabelas está integrada ao processo CRISP-DM, principalmente nas etapas de **Entendimento dos Dados, Preparação, Modelagem, Avaliação e Implantação**.

Dessa forma, o Excel funciona como uma ferramenta complementar ao Python/Google Colab, permitindo validar resultados, criar indicadores e preparar informações para visualização em dashboards.

O conjunto de tabelas produzido também fornece uma estrutura organizada para apoiar a análise dos acidentes fatais e contribuir para uma melhor compreensão dos fatores associados à segurança nas rodovias federais.