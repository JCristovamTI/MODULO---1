```python
#importar comandos

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from pathlib import Path
from datetime import datetime
import unicodedata
pd.set_option("display.max_columns", 120)
pd.set_option("display.width", 160)
```


```python
#Criar estrutura de pastas
RAIZ = Path(".")
PASTAS = [
"dados_brutos", "dados_tratados", "notebooks", "sql",
"dashboards", "relatorios", "apresentacao", "logs"
]
for pasta in PASTAS:
    (RAIZ / pasta).mkdir(parents=True, exist_ok=True)
print("Pastas verificadas/criadas:")
for pasta in PASTAS:
    print("-", RAIZ / pasta)
```

    Pastas verificadas/criadas:
    - dados_brutos
    - dados_tratados
    - notebooks
    - sql
    - dashboards
    - relatorios
    - apresentacao
    - logs



```python
#Definir parâmetros do projeto
ARQUIVO_BRUTO = Path("/content/dados_abertos_prf-datatran2025.csv")
ARQUIVO_BASE_ANALITICA = Path("dados_tratados/base_analitica_prf_2025.csv")
ARQUIVO_BASE_MODELAVEL = Path("dados_tratados/base_modelavel_prf_2025.csv")
ARQUIVO_DICIONARIO = Path("dados_tratados/dicionario_variaveis_modulo4.csv")
ARQUIVO_DECISOES = Path("logs/decisoes_tratamento_modulo4.md")
ARQUIVO_README = Path("README.md")
SEPARADOR = ";"
ENCODING_ENTRADA = "latin1"
ENCODING_SAIDA = "utf-8-sig"
```


```python
#Ler o CSV da PRF com fallback de encoding
def ler_csv_prf(caminho, sep=";", encodings=("latin1", "utf-8", "utf-8-sig")):
    ultimo_erro = None
    for enc in encodings:
        try:
            print(f"Tentando leitura com encoding={enc}...")
            return pd.read_csv(caminho, sep=sep, encoding=enc, low_memory=False)
        except Exception as erro:
            ultimo_erro = erro
            print(f"Falhou com {enc}: {erro}")
    raise ultimo_erro
df = ler_csv_prf(ARQUIVO_BRUTO, sep=SEPARADOR)
df.head()
```

    Tentando leitura com encoding=latin1...






  <div id="df-d9e4e286-b29c-4cde-a423-7044baab3157" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>data_inversa</th>
      <th>dia_semana</th>
      <th>horario</th>
      <th>uf</th>
      <th>br</th>
      <th>km</th>
      <th>municipio</th>
      <th>causa_acidente</th>
      <th>tipo_acidente</th>
      <th>classificacao_acidente</th>
      <th>fase_dia</th>
      <th>sentido_via</th>
      <th>condicao_metereologica</th>
      <th>tipo_pista</th>
      <th>tracado_via</th>
      <th>uso_solo</th>
      <th>pessoas</th>
      <th>mortos</th>
      <th>feridos_leves</th>
      <th>feridos_graves</th>
      <th>ilesos</th>
      <th>ignorados</th>
      <th>feridos</th>
      <th>veiculos</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>regional</th>
      <th>delegacia</th>
      <th>uop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>652493</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>06:20:00</td>
      <td>SP</td>
      <td>116</td>
      <td>225</td>
      <td>GUARULHOS</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Tombamento</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Decrescente</td>
      <td>Céu Claro</td>
      <td>Múltipla</td>
      <td>Reta;Declive</td>
      <td>Sim</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>-23,48586772</td>
      <td>-46,54075317</td>
      <td>SPRF-SP</td>
      <td>DEL01-SP</td>
      <td>UOP01-DEL01-SP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>652519</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>07:50:00</td>
      <td>CE</td>
      <td>116</td>
      <td>546,2</td>
      <td>PENAFORTE</td>
      <td>Pista esburacada</td>
      <td>Colisão frontal</td>
      <td>NaN</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Simples</td>
      <td>Reta</td>
      <td>Não</td>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>6</td>
      <td>-7,812288</td>
      <td>-39,08333306</td>
      <td>SPRF-CE</td>
      <td>DEL05-CE</td>
      <td>UOP03-DEL05-CE</td>
    </tr>
    <tr>
      <th>2</th>
      <td>652522</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>08:45:00</td>
      <td>PR</td>
      <td>369</td>
      <td>88,2</td>
      <td>CORNELIO PROCOPIO</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Colisão traseira</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Sol</td>
      <td>Dupla</td>
      <td>Reta;Aclive</td>
      <td>Sim</td>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
      <td>-23,182565</td>
      <td>-50,637228</td>
      <td>SPRF-PR</td>
      <td>DEL07-PR</td>
      <td>UOP05-DEL07-PR</td>
    </tr>
    <tr>
      <th>3</th>
      <td>652544</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>11:00:00</td>
      <td>PR</td>
      <td>116</td>
      <td>74</td>
      <td>CAMPINA GRANDE DO SUL</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Saída de leito carroçável</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Dupla</td>
      <td>Reta</td>
      <td>Não</td>
      <td>5</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>-25,36517687</td>
      <td>-49,04223028</td>
      <td>SPRF-PR</td>
      <td>DEL01-PR</td>
      <td>UOP02-DEL01-PR</td>
    </tr>
    <tr>
      <th>4</th>
      <td>652549</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>09:30:00</td>
      <td>MG</td>
      <td>251</td>
      <td>471</td>
      <td>FRANCISCO SA</td>
      <td>Velocidade Incompatível</td>
      <td>Colisão frontal</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Decrescente</td>
      <td>Chuva</td>
      <td>Simples</td>
      <td>Curva;Declive</td>
      <td>Não</td>
      <td>5</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>4</td>
      <td>-16,46801304</td>
      <td>-43,43121303</td>
      <td>SPRF-MG</td>
      <td>DEL12-MG</td>
      <td>UOP01-DEL12-MG</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-d9e4e286-b29c-4cde-a423-7044baab3157')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  

    <script>
      const buttonEl =
        document.querySelector('#df-d9e4e286-b29c-4cde-a423-7044baab3157 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-d9e4e286-b29c-4cde-a423-7044baab3157');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




### Acidentes por Estado (UF)
Vamos visualizar a distribuição dos acidentes por Unidade da Federação (UF) para entender onde a maioria dos acidentes ocorre.


```python
uf_accident_counts = df['uf'].value_counts().reset_index()
uf_accident_counts.columns = ['UF', 'Numero de Acidentes']

plt.figure(figsize=(12, 6))
sns.barplot(x='UF', y='Numero de Acidentes', data=uf_accident_counts, palette='viridis')
plt.title('Número de Acidentes por UF')
plt.xlabel('Unidade da Federação')
plt.ylabel('Número de Acidentes')
plt.xticks(rotation=45)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()
```

    /tmp/ipykernel_3993/1744622856.py:5: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.barplot(x='UF', y='Numero de Acidentes', data=uf_accident_counts, palette='viridis')



    
![png](Unidade%204%20python%20aponti%20%281%29_files/Unidade%204%20python%20aponti%20%281%29_5_1.png)
    



```python
#Padronizar nomes das colunas
def normalizar_nome_coluna(nome):
    nome = str(nome).strip().lower()
    nome = unicodedata.normalize("NFKD", nome).encode("ascii", "ignore").decode("utf-8")
    nome = nome.replace(" ", "_").replace("-", "_").replace("/", "_")
    while "__" in nome:
        nome = nome.replace("__", "_")
    return nome.strip("_")
df.columns = [normalizar_nome_coluna(c) for c in df.columns]
# Compatibilização de grafias possíveis
renomear = {"condicao_meteorologica": "condicao_metereologica"}
df = df.rename(columns={k: v for k, v in renomear.items() if k in df.columns})
print(df.columns.tolist())
```

    ['id', 'data_inversa', 'dia_semana', 'horario', 'uf', 'br', 'km', 'municipio', 'causa_acidente', 'tipo_acidente', 'classificacao_acidente', 'fase_dia', 'sentido_via', 'condicao_metereologica', 'tipo_pista', 'tracado_via', 'uso_solo', 'pessoas', 'mortos', 'feridos_leves', 'feridos_graves', 'ilesos', 'ignorados', 'feridos', 'veiculos', 'latitude', 'longitude', 'regional', 'delegacia', 'uop']



```python
#Conferir colunas esperadas
colunas_esperadas = [
"data_inversa", "dia_semana", "horario", "uf", "br", "municipio",
"causa_acidente", "tipo_acidente", "classificacao_acidente",
"fase_dia", "condicao_metereologica", "tipo_pista", "tracado_via",
"uso_solo", "pessoas", "mortos", "feridos_leves",
"feridos_graves", "feridos", "veiculos"
]
faltantes = [c for c in colunas_esperadas if c not in df.columns]
print("Colunas faltantes:", faltantes)
if faltantes:
    print("Atenção: ajuste nomes ou confirme o dicionário oficial da PRF usado no arquivo.")
```

    Colunas faltantes: []



```python
#Retrato inicial da base
print("Dimensões:", df.shape)
print("Linhas:", df.shape[0])
print("Colunas:", df.shape[1])
display(df.head())
display(df.sample(5, random_state=42))
```

    Dimensões: (72529, 30)
    Linhas: 72529
    Colunas: 30




  <div id="df-5d29f0f8-9c9d-47b2-b05f-5bf42e34ccfc" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>data_inversa</th>
      <th>dia_semana</th>
      <th>horario</th>
      <th>uf</th>
      <th>br</th>
      <th>km</th>
      <th>municipio</th>
      <th>causa_acidente</th>
      <th>tipo_acidente</th>
      <th>classificacao_acidente</th>
      <th>fase_dia</th>
      <th>sentido_via</th>
      <th>condicao_metereologica</th>
      <th>tipo_pista</th>
      <th>tracado_via</th>
      <th>uso_solo</th>
      <th>pessoas</th>
      <th>mortos</th>
      <th>feridos_leves</th>
      <th>feridos_graves</th>
      <th>ilesos</th>
      <th>ignorados</th>
      <th>feridos</th>
      <th>veiculos</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>regional</th>
      <th>delegacia</th>
      <th>uop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>652493</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>06:20:00</td>
      <td>SP</td>
      <td>116</td>
      <td>225</td>
      <td>GUARULHOS</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Tombamento</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Decrescente</td>
      <td>Céu Claro</td>
      <td>Múltipla</td>
      <td>Reta;Declive</td>
      <td>Sim</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>-23,48586772</td>
      <td>-46,54075317</td>
      <td>SPRF-SP</td>
      <td>DEL01-SP</td>
      <td>UOP01-DEL01-SP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>652519</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>07:50:00</td>
      <td>CE</td>
      <td>116</td>
      <td>546,2</td>
      <td>PENAFORTE</td>
      <td>Pista esburacada</td>
      <td>Colisão frontal</td>
      <td>NaN</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Simples</td>
      <td>Reta</td>
      <td>Não</td>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>6</td>
      <td>-7,812288</td>
      <td>-39,08333306</td>
      <td>SPRF-CE</td>
      <td>DEL05-CE</td>
      <td>UOP03-DEL05-CE</td>
    </tr>
    <tr>
      <th>2</th>
      <td>652522</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>08:45:00</td>
      <td>PR</td>
      <td>369</td>
      <td>88,2</td>
      <td>CORNELIO PROCOPIO</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Colisão traseira</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Sol</td>
      <td>Dupla</td>
      <td>Reta;Aclive</td>
      <td>Sim</td>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
      <td>-23,182565</td>
      <td>-50,637228</td>
      <td>SPRF-PR</td>
      <td>DEL07-PR</td>
      <td>UOP05-DEL07-PR</td>
    </tr>
    <tr>
      <th>3</th>
      <td>652544</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>11:00:00</td>
      <td>PR</td>
      <td>116</td>
      <td>74</td>
      <td>CAMPINA GRANDE DO SUL</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Saída de leito carroçável</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Dupla</td>
      <td>Reta</td>
      <td>Não</td>
      <td>5</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>-25,36517687</td>
      <td>-49,04223028</td>
      <td>SPRF-PR</td>
      <td>DEL01-PR</td>
      <td>UOP02-DEL01-PR</td>
    </tr>
    <tr>
      <th>4</th>
      <td>652549</td>
      <td>2025-01-01</td>
      <td>quarta-feira</td>
      <td>09:30:00</td>
      <td>MG</td>
      <td>251</td>
      <td>471</td>
      <td>FRANCISCO SA</td>
      <td>Velocidade Incompatível</td>
      <td>Colisão frontal</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Decrescente</td>
      <td>Chuva</td>
      <td>Simples</td>
      <td>Curva;Declive</td>
      <td>Não</td>
      <td>5</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>4</td>
      <td>-16,46801304</td>
      <td>-43,43121303</td>
      <td>SPRF-MG</td>
      <td>DEL12-MG</td>
      <td>UOP01-DEL12-MG</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-5d29f0f8-9c9d-47b2-b05f-5bf42e34ccfc')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-5d29f0f8-9c9d-47b2-b05f-5bf42e34ccfc button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-5d29f0f8-9c9d-47b2-b05f-5bf42e34ccfc');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>





  <div id="df-a63ff0c0-7d16-4297-a1d7-f4f4471726e6" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>data_inversa</th>
      <th>dia_semana</th>
      <th>horario</th>
      <th>uf</th>
      <th>br</th>
      <th>km</th>
      <th>municipio</th>
      <th>causa_acidente</th>
      <th>tipo_acidente</th>
      <th>classificacao_acidente</th>
      <th>fase_dia</th>
      <th>sentido_via</th>
      <th>condicao_metereologica</th>
      <th>tipo_pista</th>
      <th>tracado_via</th>
      <th>uso_solo</th>
      <th>pessoas</th>
      <th>mortos</th>
      <th>feridos_leves</th>
      <th>feridos_graves</th>
      <th>ilesos</th>
      <th>ignorados</th>
      <th>feridos</th>
      <th>veiculos</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>regional</th>
      <th>delegacia</th>
      <th>uop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6366</th>
      <td>691804</td>
      <td>2025-03-15</td>
      <td>sábado</td>
      <td>12:30:00</td>
      <td>ES</td>
      <td>101</td>
      <td>67</td>
      <td>SAO MATEUS</td>
      <td>Condutor desrespeitou a iluminação vermelha do...</td>
      <td>Colisão transversal</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Sol</td>
      <td>Simples</td>
      <td>Rotatória</td>
      <td>Sim</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>4</td>
      <td>-18,72802869</td>
      <td>-39,85997558</td>
      <td>SPRF-ES</td>
      <td>DEL04-ES</td>
      <td>UOP02-DEL04-ES</td>
    </tr>
    <tr>
      <th>9405</th>
      <td>704622</td>
      <td>2025-07-13</td>
      <td>domingo</td>
      <td>22:30:00</td>
      <td>PE</td>
      <td>423</td>
      <td>74,1</td>
      <td>JUPI</td>
      <td>Condutor deixou de manter distância do veículo...</td>
      <td>Colisão traseira</td>
      <td>Sem Vítimas</td>
      <td>Plena Noite</td>
      <td>Decrescente</td>
      <td>Céu Claro</td>
      <td>Simples</td>
      <td>Aclive;Reta</td>
      <td>Sim</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>-8,7160879</td>
      <td>-36,4219923</td>
      <td>SPRF-PE</td>
      <td>DEL03-PE</td>
      <td>UOP01-DEL03-PE</td>
    </tr>
    <tr>
      <th>26102</th>
      <td>663260</td>
      <td>2025-02-23</td>
      <td>domingo</td>
      <td>18:10:00</td>
      <td>BA</td>
      <td>242</td>
      <td>231</td>
      <td>ITABERABA</td>
      <td>Animais na Pista</td>
      <td>Atropelamento de Animal</td>
      <td>Com Vítimas Feridas</td>
      <td>Plena Noite</td>
      <td>Decrescente</td>
      <td>Céu Claro</td>
      <td>Simples</td>
      <td>Reta</td>
      <td>Sim</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>-12,511706</td>
      <td>-40,324247</td>
      <td>SPRF-BA</td>
      <td>DEL06-BA</td>
      <td>UOP02-DEL06-BA</td>
    </tr>
    <tr>
      <th>28616</th>
      <td>667036</td>
      <td>2025-03-13</td>
      <td>quinta-feira</td>
      <td>19:55:00</td>
      <td>DF</td>
      <td>20</td>
      <td>9,9</td>
      <td>BRASILIA</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Engavetamento</td>
      <td>Com Vítimas Feridas</td>
      <td>Plena Noite</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Dupla</td>
      <td>Reta</td>
      <td>Não</td>
      <td>6</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>4</td>
      <td>3</td>
      <td>-15,6502715</td>
      <td>-47,7763723</td>
      <td>SPRF-DF</td>
      <td>DEL02-DF</td>
      <td>UOP01-DEL02-DF</td>
    </tr>
    <tr>
      <th>1696</th>
      <td>660353</td>
      <td>2025-02-09</td>
      <td>domingo</td>
      <td>19:05:00</td>
      <td>MA</td>
      <td>222</td>
      <td>665</td>
      <td>ACAILANDIA</td>
      <td>Pedestre andava na pista</td>
      <td>Atropelamento de Pedestre</td>
      <td>Com Vítimas Feridas</td>
      <td>Plena Noite</td>
      <td>Decrescente</td>
      <td>Céu Claro</td>
      <td>Simples</td>
      <td>Declive</td>
      <td>Não</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>-4,89367779</td>
      <td>-47,38426513</td>
      <td>SPRF-MA</td>
      <td>DEL04-MA</td>
      <td>UOP03-DEL04-MA</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-a63ff0c0-7d16-4297-a1d7-f4f4471726e6')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-a63ff0c0-7d16-4297-a1d7-f4f4471726e6 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-a63ff0c0-7d16-4297-a1d7-f4f4471726e6');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




```python
#Tipos de dados e memória
df.info(memory_usage="deep")
resumo_tipos = (
df.dtypes.astype(str)
.value_counts()
.rename_axis("tipo")
.reset_index(name="qtd_colunas")
)
display(resumo_tipos)
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 72529 entries, 0 to 72528
    Data columns (total 30 columns):
     #   Column                  Non-Null Count  Dtype 
    ---  ------                  --------------  ----- 
     0   id                      72529 non-null  int64 
     1   data_inversa            72529 non-null  object
     2   dia_semana              72529 non-null  object
     3   horario                 72529 non-null  object
     4   uf                      72529 non-null  object
     5   br                      72529 non-null  int64 
     6   km                      72529 non-null  object
     7   municipio               72529 non-null  object
     8   causa_acidente          72529 non-null  object
     9   tipo_acidente           72529 non-null  object
     10  classificacao_acidente  72528 non-null  object
     11  fase_dia                72529 non-null  object
     12  sentido_via             72529 non-null  object
     13  condicao_metereologica  72529 non-null  object
     14  tipo_pista              72529 non-null  object
     15  tracado_via             72529 non-null  object
     16  uso_solo                72529 non-null  object
     17  pessoas                 72529 non-null  int64 
     18  mortos                  72529 non-null  int64 
     19  feridos_leves           72529 non-null  int64 
     20  feridos_graves          72529 non-null  int64 
     21  ilesos                  72529 non-null  int64 
     22  ignorados               72529 non-null  int64 
     23  feridos                 72529 non-null  int64 
     24  veiculos                72529 non-null  int64 
     25  latitude                72529 non-null  object
     26  longitude               72529 non-null  object
     27  regional                72527 non-null  object
     28  delegacia               72507 non-null  object
     29  uop                     72491 non-null  object
    dtypes: int64(10), object(20)
    memory usage: 92.7 MB




  <div id="df-d5cdc124-b6ef-48d3-b7ac-d9b1705a731f" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tipo</th>
      <th>qtd_colunas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>object</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>int64</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-d5cdc124-b6ef-48d3-b7ac-d9b1705a731f')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-d5cdc124-b6ef-48d3-b7ac-d9b1705a731f button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-d5cdc124-b6ef-48d3-b7ac-d9b1705a731f');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


  <div id="id_1c0ff12f-2467-449a-9186-fe26e09614ca">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('resumo_tipos')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_1c0ff12f-2467-449a-9186-fe26e09614ca button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('resumo_tipos');
      }
      })();
    </script>
  </div>

    </div>
  </div>



### Estatísticas Descritivas para Mortos e Feridos

Vamos analisar as estatísticas descritivas para as colunas `mortos` e `feridos` para entender a distribuição desses eventos nos acidentes.


```python
print('Estatísticas Descritivas para a coluna mortos:')
display(df['mortos'].describe())

print('\nEstatísticas Descritivas para a coluna feridos:')
display(df['feridos'].describe())
```


```python
#Diagnóstico de valores ausentes
nulos = pd.DataFrame({
"qtd_nulos": df.isna().sum(),
"perc_nulos": df.isna().mean() * 100
}).sort_values("perc_nulos", ascending=False)
display(nulos[nulos["qtd_nulos"] > 0])
```



  <div id="df-fb356f8e-ef6b-48f3-a098-27ad77c6d088" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>qtd_nulos</th>
      <th>perc_nulos</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>uop</th>
      <td>38</td>
      <td>0.052393</td>
    </tr>
    <tr>
      <th>delegacia</th>
      <td>22</td>
      <td>0.030333</td>
    </tr>
    <tr>
      <th>regional</th>
      <td>2</td>
      <td>0.002758</td>
    </tr>
    <tr>
      <th>classificacao_acidente</th>
      <td>1</td>
      <td>0.001379</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-fb356f8e-ef6b-48f3-a098-27ad77c6d088')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-fb356f8e-ef6b-48f3-a098-27ad77c6d088 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-fb356f8e-ef6b-48f3-a098-27ad77c6d088');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




```python
#Diagnóstico e remoção de duplicidades
qtd_duplicadas = df.duplicated().sum()
print("Duplicidades exatas:", qtd_duplicadas)
if qtd_duplicadas > 0:
    df = df.drop_duplicates().copy()
    print("Duplicidades removidas. Nova dimensão:", df.shape)
```

    Duplicidades exatas: 0



```python
#Cardinalidade das categorias
categoricas = df.select_dtypes(include="object").columns
cardinalidade = (
df[categoricas]
.nunique(dropna=True)
.sort_values(ascending=False)
.reset_index()
)
cardinalidade.columns = ["variavel", "qtd_categorias"]
display(cardinalidade.head(30))

```



  <div id="df-1667da52-4564-4e46-8b98-cfa8f9df5037" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>variavel</th>
      <th>qtd_categorias</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>latitude</td>
      <td>69294</td>
    </tr>
    <tr>
      <th>1</th>
      <td>longitude</td>
      <td>69237</td>
    </tr>
    <tr>
      <th>2</th>
      <td>km</td>
      <td>7655</td>
    </tr>
    <tr>
      <th>3</th>
      <td>municipio</td>
      <td>1844</td>
    </tr>
    <tr>
      <th>4</th>
      <td>horario</td>
      <td>1412</td>
    </tr>
    <tr>
      <th>5</th>
      <td>tracado_via</td>
      <td>605</td>
    </tr>
    <tr>
      <th>6</th>
      <td>uop</td>
      <td>395</td>
    </tr>
    <tr>
      <th>7</th>
      <td>data_inversa</td>
      <td>365</td>
    </tr>
    <tr>
      <th>8</th>
      <td>delegacia</td>
      <td>153</td>
    </tr>
    <tr>
      <th>9</th>
      <td>causa_acidente</td>
      <td>69</td>
    </tr>
    <tr>
      <th>10</th>
      <td>regional</td>
      <td>28</td>
    </tr>
    <tr>
      <th>11</th>
      <td>uf</td>
      <td>27</td>
    </tr>
    <tr>
      <th>12</th>
      <td>tipo_acidente</td>
      <td>17</td>
    </tr>
    <tr>
      <th>13</th>
      <td>condicao_metereologica</td>
      <td>9</td>
    </tr>
    <tr>
      <th>14</th>
      <td>dia_semana</td>
      <td>7</td>
    </tr>
    <tr>
      <th>15</th>
      <td>fase_dia</td>
      <td>4</td>
    </tr>
    <tr>
      <th>16</th>
      <td>sentido_via</td>
      <td>3</td>
    </tr>
    <tr>
      <th>17</th>
      <td>classificacao_acidente</td>
      <td>3</td>
    </tr>
    <tr>
      <th>18</th>
      <td>tipo_pista</td>
      <td>3</td>
    </tr>
    <tr>
      <th>19</th>
      <td>uso_solo</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-1667da52-4564-4e46-8b98-cfa8f9df5037')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-1667da52-4564-4e46-8b98-cfa8f9df5037 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-1667da52-4564-4e46-8b98-cfa8f9df5037');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




```python
#Transformações e variáveis derivadas
#Converter colunas numéricas
colunas_numericas = [
    "br", "km", "pessoas", "mortos", "feridos", "feridos_leves",
    "feridos_graves", "ilesos", "ignorados", "veiculos"
]
for coluna in colunas_numericas:
    if coluna in df.columns:
        df[coluna] = pd.to_numeric(df[coluna], errors="coerce")
print(df[[c for c in colunas_numericas if c in df.columns]].dtypes)
```

    br                  int64
    km                float64
    pessoas             int64
    mortos              int64
    feridos             int64
    feridos_leves       int64
    feridos_graves      int64
    ilesos              int64
    ignorados           int64
    veiculos            int64
    dtype: object



```python
#Tratar datas e criar variáveis temporais
df["data_inversa"] = pd.to_datetime(df["data_inversa"], errors="coerce")

df["ano"] = df["data_inversa"].dt.year
df["mes"] = df["data_inversa"].dt.month
df["trimestre"] = df["data_inversa"].dt.quarter
df["dia_semana_num"] = df["data_inversa"].dt.dayofweek
df["fim_de_semana"] = df["dia_semana_num"].isin([5, 6]).astype(int)
display(df[["data_inversa", "ano", "mes", "trimestre", "dia_semana_num",
"fim_de_semana"]].head())
```



  <div id="df-deb6b8fc-9040-4968-bcd5-7e69cc43ca3d" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>data_inversa</th>
      <th>ano</th>
      <th>mes</th>
      <th>trimestre</th>
      <th>dia_semana_num</th>
      <th>fim_de_semana</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2025-01-01</td>
      <td>2025</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2025-01-01</td>
      <td>2025</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2025-01-01</td>
      <td>2025</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2025-01-01</td>
      <td>2025</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2025-01-01</td>
      <td>2025</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-deb6b8fc-9040-4968-bcd5-7e69cc43ca3d')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-deb6b8fc-9040-4968-bcd5-7e69cc43ca3d button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-deb6b8fc-9040-4968-bcd5-7e69cc43ca3d');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




```python
#Tratar horário e criar turno
horario_limpo = df["horario"].astype(str).str.strip()
df["hora"] = pd.to_datetime(horario_limpo, format="%H:%M:%S", errors="coerce").dt.hour
# Tentativa alternativa para arquivos com HH:MM
faltou_hora = df["hora"].isna()
if faltou_hora.any():
    df.loc[faltou_hora, "hora"] = pd.to_datetime(
        horario_limpo[faltou_hora], format="%H:%M", errors="coerce"
    ).dt.hour
def classificar_turno(hora):
    if pd.isna(hora):
        return "IGNORADO"
    if 0 <= hora <= 5:
        return "MADRUGADA"
    if 6 <= hora <= 11:
        return "MANHA"
    if 12 <= hora <= 17:
        return "TARDE"
    return "NOITE"
df["turno"] = df["hora"].apply(classificar_turno)
display(df[["horario", "hora", "turno"]].head())
```



  <div id="df-7d831173-cc0c-48d5-a48e-04e68b7c81c6" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>horario</th>
      <th>hora</th>
      <th>turno</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>06:20:00</td>
      <td>6</td>
      <td>MANHA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>07:50:00</td>
      <td>7</td>
      <td>MANHA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>08:45:00</td>
      <td>8</td>
      <td>MANHA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11:00:00</td>
      <td>11</td>
      <td>MANHA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>09:30:00</td>
      <td>9</td>
      <td>MANHA</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-7d831173-cc0c-48d5-a48e-04e68b7c81c6')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-7d831173-cc0c-48d5-a48e-04e68b7c81c6 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-7d831173-cc0c-48d5-a48e-04e68b7c81c6');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>



### Número de Mortos por Turno

Vamos analisar a distribuição de fatalidades ('mortos') de acordo com o turno do dia para identificar padrões.


```python
mortos_por_turno = df.groupby('turno')['mortos'].sum().reset_index()

plt.figure(figsize=(10, 6))
sns.barplot(x='turno', y='mortos', data=mortos_por_turno, palette='viridis')
plt.title('Número de Mortos por Turno')
plt.xlabel('Turno')
plt.ylabel('Número Total de Mortos')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()
```

    /tmp/ipykernel_3993/1055991364.py:4: FutureWarning: 
    
    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.
    
      sns.barplot(x='turno', y='mortos', data=mortos_por_turno, palette='viridis')



    
![png](Unidade%204%20python%20aponti%20%281%29_files/Unidade%204%20python%20aponti%20%281%29_19_1.png)
    



```python
#Criar faixa horária
def criar_faixa_horaria(hora):
  if pd.isna(hora):
    return "IGNORADO"
  inicio = int(hora // 3) * 3
  fim = inicio + 2
  return f"{inicio:02d}h-{fim:02d}h"
df["faixa_horaria"] = df["hora"].apply(criar_faixa_horaria)
display(df["faixa_horaria"].value_counts(dropna=False).sort_index())
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>faixa_horaria</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>00h-02h</th>
      <td>3959</td>
    </tr>
    <tr>
      <th>03h-05h</th>
      <td>4948</td>
    </tr>
    <tr>
      <th>06h-08h</th>
      <td>11517</td>
    </tr>
    <tr>
      <th>09h-11h</th>
      <td>9342</td>
    </tr>
    <tr>
      <th>12h-14h</th>
      <td>9678</td>
    </tr>
    <tr>
      <th>15h-17h</th>
      <td>12624</td>
    </tr>
    <tr>
      <th>18h-20h</th>
      <td>13473</td>
    </tr>
    <tr>
      <th>21h-23h</th>
      <td>6988</td>
    </tr>
  </tbody>
</table>
</div><br><label><b>dtype:</b> int64</label>



```python
colunas_texto = df.select_dtypes(include="object").columns
for coluna in colunas_texto:
 df[coluna] = (
  df[coluna]
   .astype("string")
.str.strip()
.str.upper()
)
df[coluna] = df[coluna].replace({"": pd.NA, "NAN": pd.NA, "NONE": pd.NA, "NULL": pd.NA})
print("Colunas textuais padronizadas:", len(colunas_texto))
```

    Colunas textuais padronizadas: 0



```python
#Tratar nulos categóricos
categoricas_importantes = [
"uf", "municipio", "causa_acidente", "tipo_acidente", "fase_dia",
"condicao_metereologica", "tipo_pista", "tracado_via", "uso_solo",
"classificacao_acidente", "dia_semana"
]
for coluna in categoricas_importantes:
 if coluna in df.columns:
  df[coluna] = df[coluna].fillna("IGNORADO")
print(df[categoricas_importantes].isna().sum().sort_values(ascending=False))
```

    uf                        0
    municipio                 0
    causa_acidente            0
    tipo_acidente             0
    fase_dia                  0
    condicao_metereologica    0
    tipo_pista                0
    tracado_via               0
    uso_solo                  0
    classificacao_acidente    0
    dia_semana                0
    dtype: int64



```python
#Tratar nulos numéricos de contagem
contagens_vitimas = ["mortos", "feridos", "feridos_leves", "feridos_graves", "pessoas",
"veiculos"]
for coluna in contagens_vitimas:
  if coluna in df.columns:
    df[coluna] = df[coluna].fillna(0)
print(df[[c for c in contagens_vitimas if c in df.columns]].isna().sum())
```

    mortos            0
    feridos           0
    feridos_leves     0
    feridos_graves    0
    pessoas           0
    veiculos          0
    dtype: int64



```python
#Variável-alvo e indicadores de gravidade
#Criar variável-alvo acidente_fatal
df["acidente_fatal"] = np.where(df["mortos"] >= 1, 1, 0)
validacao_alvo =df["acidente_fatal"].value_counts(dropna=False).rename_axis("acidente_fatal").reset_index(name="qtd")
validacao_alvo["perc"] = validacao_alvo["qtd"] / validacao_alvo["qtd"].sum() * 100
display(validacao_alvo)
display(validacao_alvo)
```



  <div id="df-f4aad397-3f08-4747-a139-1025d58f9b91" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>acidente_fatal</th>
      <th>qtd</th>
      <th>perc</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>67319</td>
      <td>92.816666</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>5210</td>
      <td>7.183334</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-f4aad397-3f08-4747-a139-1025d58f9b91')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-f4aad397-3f08-4747-a139-1025d58f9b91 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-f4aad397-3f08-4747-a139-1025d58f9b91');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


  <div id="id_6c56228f-40e9-4adb-be47-8792cfe63e06">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('validacao_alvo')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_6c56228f-40e9-4adb-be47-8792cfe63e06 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('validacao_alvo');
      }
      })();
    </script>
  </div>

    </div>
  </div>




```python
#Validar logicamente o alvo
violacoes = df.loc[
((df["mortos"] >= 1) & (df["acidente_fatal"] != 1)) |
((df["mortos"] == 0) & (df["acidente_fatal"] != 0))
]
print("Violações da regra do alvo:", len(violacoes))
assert len(violacoes) == 0, "Há erro na criação de acidente_fatal."
```

    Violações da regra do alvo: 0



```python
#Criar indicadores de gravidade
df["total_vitimas"] = df["mortos"] + df["feridos_leves"] + df["feridos_graves"]
df["acidente_grave"] = np.where(
(df["mortos"] >= 1) | (df["feridos_graves"] >= 1),
1,
0
)
df["indice_gravidade"] = (
df["mortos"] * 3
+ df["feridos_graves"] * 2
+ df["feridos_leves"]
)
display(df[["mortos", "feridos_leves", "feridos_graves", "total_vitimas",
"indice_gravidade"]].head())
```



  <div id="df-af2840ed-6e2b-41dc-943b-b3665f90dbaa" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mortos</th>
      <th>feridos_leves</th>
      <th>feridos_graves</th>
      <th>total_vitimas</th>
      <th>indice_gravidade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-af2840ed-6e2b-41dc-943b-b3665f90dbaa')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-af2840ed-6e2b-41dc-943b-b3665f90dbaa button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-af2840ed-6e2b-41dc-943b-b3665f90dbaa');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




```python
#Criar BR formatada e chave de localidade
def formatar_br(valor):
 if pd.isna(valor) or valor == 0:
  return "BR-IGNORADA"
  return f"BR-{int(valor):03d}"
df["br_formatada"] = df["br"].apply(formatar_br)
df["chave_localidade"] = (
df["uf"].astype(str) + "_" +
df["municipio"].astype(str) + "_" +
df["br_formatada"].astype(str)
)
display(df[["uf", "municipio", "br", "br_formatada", "chave_localidade"]].head())
```



  <div id="df-6d4a9682-9623-4827-98ef-aa8d09e41f6d" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>uf</th>
      <th>municipio</th>
      <th>br</th>
      <th>br_formatada</th>
      <th>chave_localidade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SP</td>
      <td>GUARULHOS</td>
      <td>116</td>
      <td>None</td>
      <td>SP_GUARULHOS_None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CE</td>
      <td>PENAFORTE</td>
      <td>116</td>
      <td>None</td>
      <td>CE_PENAFORTE_None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PR</td>
      <td>CORNELIO PROCOPIO</td>
      <td>369</td>
      <td>None</td>
      <td>PR_CORNELIO PROCOPIO_None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PR</td>
      <td>CAMPINA GRANDE DO SUL</td>
      <td>116</td>
      <td>None</td>
      <td>PR_CAMPINA GRANDE DO SUL_None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MG</td>
      <td>FRANCISCO SA</td>
      <td>251</td>
      <td>None</td>
      <td>MG_FRANCISCO SA_None</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-6d4a9682-9623-4827-98ef-aa8d09e41f6d')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-6d4a9682-9623-4827-98ef-aa8d09e41f6d button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-6d4a9682-9623-4827-98ef-aa8d09e41f6d');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




```python
#Checagens rápidas após transformação
checagens = {
"linhas": len(df),
"colunas": df.shape[1],
"acidentes_fatais": int(df["acidente_fatal"].sum()),
"taxa_fatalidade": float(df["acidente_fatal"].mean()),
"total_mortos": int(df["mortos"].sum()),
 "total_feridos": int(df["feridos"].sum()) if "feridos" in df.columns else None,
}
checagens
```




    {'linhas': 72529,
     'colunas': 44,
     'acidentes_fatais': 5210,
     'taxa_fatalidade': 0.07183333563126473,
     'total_mortos': 6043,
     'total_feridos': 83550}




```python
#Ranking rápido de categorias
def ranking_categoria(base, coluna, n=10):
 return (
 base[coluna]
.value_counts(dropna=False)
.head(n)
.rename_axis(coluna)
.reset_index(name="qtd")
)
display(ranking_categoria(df, "causa_acidente", 10))
display(ranking_categoria(df, "tipo_acidente", 10))
```



  <div id="df-e7a255d8-b74e-44d1-ba41-6ee6f70acc83" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>causa_acidente</th>
      <th>qtd</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AUSÊNCIA DE REAÇÃO DO CONDUTOR</td>
      <td>11469</td>
    </tr>
    <tr>
      <th>1</th>
      <td>REAÇÃO TARDIA OU INEFICIENTE DO CONDUTOR</td>
      <td>10799</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ACESSAR A VIA SEM OBSERVAR A PRESENÇA DOS OUTR...</td>
      <td>7097</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CONDUTOR DEIXOU DE MANTER DISTÂNCIA DO VEÍCULO...</td>
      <td>4413</td>
    </tr>
    <tr>
      <th>4</th>
      <td>VELOCIDADE INCOMPATÍVEL</td>
      <td>4088</td>
    </tr>
    <tr>
      <th>5</th>
      <td>MANOBRA DE MUDANÇA DE FAIXA</td>
      <td>4016</td>
    </tr>
    <tr>
      <th>6</th>
      <td>INGESTÃO DE ÁLCOOL PELO CONDUTOR</td>
      <td>3685</td>
    </tr>
    <tr>
      <th>7</th>
      <td>DEMAIS FALHAS MECÂNICAS OU ELÉTRICAS</td>
      <td>3385</td>
    </tr>
    <tr>
      <th>8</th>
      <td>TRANSITAR NA CONTRAMÃO</td>
      <td>2475</td>
    </tr>
    <tr>
      <th>9</th>
      <td>CONDUTOR DORMINDO</td>
      <td>2116</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-e7a255d8-b74e-44d1-ba41-6ee6f70acc83')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-e7a255d8-b74e-44d1-ba41-6ee6f70acc83 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-e7a255d8-b74e-44d1-ba41-6ee6f70acc83');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>





  <div id="df-c0c52cc9-ebd1-4392-bfc4-04b38e495e32" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tipo_acidente</th>
      <th>qtd</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>COLISÃO TRASEIRA</td>
      <td>14360</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SAÍDA DE LEITO CARROÇÁVEL</td>
      <td>10209</td>
    </tr>
    <tr>
      <th>2</th>
      <td>COLISÃO TRANSVERSAL</td>
      <td>9306</td>
    </tr>
    <tr>
      <th>3</th>
      <td>COLISÃO LATERAL MESMO SENTIDO</td>
      <td>7885</td>
    </tr>
    <tr>
      <th>4</th>
      <td>TOMBAMENTO</td>
      <td>6351</td>
    </tr>
    <tr>
      <th>5</th>
      <td>COLISÃO COM OBJETO</td>
      <td>5109</td>
    </tr>
    <tr>
      <th>6</th>
      <td>COLISÃO FRONTAL</td>
      <td>4739</td>
    </tr>
    <tr>
      <th>7</th>
      <td>QUEDA DE OCUPANTE DE VEÍCULO</td>
      <td>3450</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ATROPELAMENTO DE PEDESTRE</td>
      <td>3057</td>
    </tr>
    <tr>
      <th>9</th>
      <td>COLISÃO LATERAL SENTIDO OPOSTO</td>
      <td>2152</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-c0c52cc9-ebd1-4392-bfc4-04b38e495e32')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-c0c52cc9-ebd1-4392-bfc4-04b38e495e32 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-c0c52cc9-ebd1-4392-bfc4-04b38e495e32');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




```python
#Taxa fatal por categoria
def taxa_fatal_por_categoria(base, coluna, min_registros=30):
 tab = base.groupby(coluna).agg(
qtd_acidentes=("acidente_fatal", "size"),
qtd_fatais=("acidente_fatal", "sum"),
taxa_fatal=("acidente_fatal", "mean")
).reset_index()
 tab = tab[tab["qtd_acidentes"] >= min_registros]
 return tab.sort_values("taxa_fatal", ascending=False)
display(taxa_fatal_por_categoria(df, "tipo_acidente", min_registros=30).head(10))
```



  <div id="df-f32d609b-cbd2-4c77-93ff-760eba6e7280" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tipo_acidente</th>
      <th>qtd_acidentes</th>
      <th>qtd_fatais</th>
      <th>taxa_fatal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>ATROPELAMENTO DE PEDESTRE</td>
      <td>3057</td>
      <td>902</td>
      <td>0.295061</td>
    </tr>
    <tr>
      <th>4</th>
      <td>COLISÃO FRONTAL</td>
      <td>4739</td>
      <td>1396</td>
      <td>0.294577</td>
    </tr>
    <tr>
      <th>6</th>
      <td>COLISÃO LATERAL SENTIDO OPOSTO</td>
      <td>2152</td>
      <td>212</td>
      <td>0.098513</td>
    </tr>
    <tr>
      <th>11</th>
      <td>EVENTOS ATÍPICOS</td>
      <td>287</td>
      <td>23</td>
      <td>0.080139</td>
    </tr>
    <tr>
      <th>0</th>
      <td>ATROPELAMENTO DE ANIMAL</td>
      <td>1133</td>
      <td>68</td>
      <td>0.060018</td>
    </tr>
    <tr>
      <th>14</th>
      <td>SAÍDA DE LEITO CARROÇÁVEL</td>
      <td>10209</td>
      <td>605</td>
      <td>0.059261</td>
    </tr>
    <tr>
      <th>3</th>
      <td>COLISÃO COM OBJETO</td>
      <td>5109</td>
      <td>297</td>
      <td>0.058133</td>
    </tr>
    <tr>
      <th>2</th>
      <td>CAPOTAMENTO</td>
      <td>1373</td>
      <td>63</td>
      <td>0.045885</td>
    </tr>
    <tr>
      <th>7</th>
      <td>COLISÃO TRANSVERSAL</td>
      <td>9306</td>
      <td>427</td>
      <td>0.045884</td>
    </tr>
    <tr>
      <th>8</th>
      <td>COLISÃO TRASEIRA</td>
      <td>14360</td>
      <td>619</td>
      <td>0.043106</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-f32d609b-cbd2-4c77-93ff-760eba6e7280')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-f32d609b-cbd2-4c77-93ff-760eba6e7280 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-f32d609b-cbd2-4c77-93ff-760eba6e7280');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>




```python
#Gráfico simples de conferência
ax = df["acidente_fatal"].value_counts().sort_index().plot(kind="bar")
ax.set_title("Distribuição da variável-alvo acidente_fatal")
ax.set_xlabel("acidente_fatal")
ax.set_ylabel("Quantidade de acidentes")
plt.show()
```


    
![png](Unidade%204%20python%20aponti%20%281%29_files/Unidade%204%20python%20aponti%20%281%29_31_0.png)
    



```python
#Construção das bases finais e documentação
#Construção das duas bases (analítica e modelável)
#Conceito de base analítica completa
#Gerar base analítica completa
base_analitica = df.copy()
print("Base analítica:", base_analitica.shape)
print("Colunas:", base_analitica.columns.tolist())
```

    Base analítica: (72529, 44)
    Colunas: ['id', 'data_inversa', 'dia_semana', 'horario', 'uf', 'br', 'km', 'municipio', 'causa_acidente', 'tipo_acidente', 'classificacao_acidente', 'fase_dia', 'sentido_via', 'condicao_metereologica', 'tipo_pista', 'tracado_via', 'uso_solo', 'pessoas', 'mortos', 'feridos_leves', 'feridos_graves', 'ilesos', 'ignorados', 'feridos', 'veiculos', 'latitude', 'longitude', 'regional', 'delegacia', 'uop', 'ano', 'mes', 'trimestre', 'dia_semana_num', 'fim_de_semana', 'hora', 'turno', 'faixa_horaria', 'acidente_fatal', 'total_vitimas', 'acidente_grave', 'indice_gravidade', 'br_formatada', 'chave_localidade']



```python
from google.colab import files

#Conceito de base modelável
uploaded = files.upload()

arquivo = list(uploaded.keys())[0]

# Tenta abrir com diferentes configurações de codificação
try:
    df = pd.read_csv(arquivo, sep=';', encoding='utf-8')
except:
    try:
        df = pd.read_csv(arquivo, sep=';', encoding='latin1')
    except:
        df = pd.read_csv(arquivo, encoding='latin1')

print("\nArquivo carregado:", arquivo)
print("Quantidade de linhas:", len(df))
print("Quantidade de colunas:", len(df))
df.columns = (
    df.columns
    .str.strip()
    .str.lower()
    .str.replace(" ", "_")
)

print("\n=== COLUNAS ENCONTRADAS ===")
for coluna in df.columns:
    print("-", coluna)

# Refactoring the 'mortos' and 'acidente_fatal' creation outside the loop
if "mortos" in df.columns:
    df["mortos"] = pd.to_numeric(
        df["mortos"],
        errors="coerce"
    ).fillna(0)

    df["acidente_fatal"] = np.where(
        df["mortos"] > 0,
        1,
        0
    )
    print("\nVariável alvo criada: acidente_fatal")
else:
    print("\nATENÇÃO: a coluna 'mortos' não foi encontrada.")
    print("Verifique o nome da coluna no arquivo.")

ALVO = "acidente_fatal"
proibidas = [
"mortos",
ALVO,
"feridos_graves",
"feridos_leves",
"ilesos",
"ignorados"
]

duvidosas = [
"pessoas",
"veiculos"
]
permitidas = [
"uf",
"br",
"km",
"municipio",
"causa_acidente",
"tipo_acidente",
"classificacao_acidente",
"fase_dia",
"sentido_via",
"condicao_metereologica",
"condicao_meteorologica",
"tipo_pista",
"tracado_via",
"uso_solo",
"dia_semana",
"horario"
]

permitidas_existentes = [
coluna for coluna in permitidas
if coluna in df.columns
]

proibidas_existentes = [
coluna for coluna in proibidas
if coluna in df.columns
]

duvidosas_existentes = [
coluna for coluna in duvidosas
if coluna in df.columns
]

print("\n")
print("=" * 70)
print("CLASSIFICAÇÃO DAS VARIÁVEIS")
print("=" * 70)

print("\n🟢 VARIÁVEIS PERMITIDAS")
print("-" * 40)

if permitidas_existentes:
    for coluna in permitidas_existentes:
        print("✔", coluna)
else:
    print("Nenhuma variável permitida encontrada.")


print("\n🔴 VARIÁVEIS PROIBIDAS")
print("-" * 40)

if proibidas_existentes:
    for coluna in proibidas_existentes:
        print("✘", coluna)
else:
    print("Nenhuma variável proibida encontrada.")


print("\n🟡 VARIÁVEIS DUVIDOSAS")
print("-" * 40)

if duvidosas_existentes:
    for coluna in duvidosas_existentes:
        print("?", coluna)
else:
    print("Nenhuma variável duvidosa encontrada.")

# Ensure colunas_modelo is always defined
colunas_modelo = permitidas_existentes + [ALVO]

base_modelavel = df[colunas_modelo].copy()
print("\n")
print("=" * 70)
print("BASE MODELÁVEL")
print("=" * 70)

print("\nDimensões:")
print("Linhas:", base_modelavel.shape[0])
print("Colunas:", base_modelavel.shape[1])

print("\nPrimeiras 10 linhas:")
display(base_modelavel.head(10))

print("\n")
print("=" * 70)
print("DISTRIBUIÇÃO DO ALVO — acidente_fatal")
print("=" * 70)

print(
    base_modelavel["acidente_fatal"]
    .value_counts()
    .sort_index()
)


# Percentual
percentuais = (
    base_modelavel["acidente_fatal"]
    .value_counts(normalize=True)
    .sort_index() * 100
)

print("\nPercentual:")
print(percentuais)

classificacao = []

for coluna in df.columns:

    if coluna == ALVO:
        categoria = "ALVO"
        motivo = "Variável que a árvore de decisão deve prever."

    elif coluna in proibidas_existentes:
        categoria = "PROIBIDA"
        motivo = "Relacionada diretamente ao desfecho ou pode causar vazamento."

    elif coluna in duvidosas_existentes:
        categoria = "DUVIDOSA"
        motivo = "Pode representar informação relacionada ao desfecho."

    elif coluna in permitidas_existentes:
        categoria = "PERMITIDA"
        motivo = "Variável explicativa disponível antes ou durante o acidente."

    else:
        categoria = "ANALISAR"
        motivo = "Necessita avaliação antes de entrar no modelo."

    classificacao.append({
        "variavel": coluna,
        "classificacao": categoria,
        "motivo": motivo
    })
    # tabela_classificacao should be created outside the loop after all appends
tabela_classificacao = pd.DataFrame(classificacao)

print("\n")
print("=" * 70)
print("TABELA DE CLASSIFICAÇÃO")
print("=" * 70)

display(tabela_classificacao)

print("\n")
print("=" * 70)
print("RESUMO — CONCEITO DE BASE MODELÁVEL")
print("=" * 70)

print(f"""




Total de registros: {len(base_modelavel)}
Total de variáveis explicativas: {len(colunas_modelo)-1}
Total de variáveis proibidas encontradas: {len(proibidas_existentes)}
Total de variáveis duvidosas encontradas: {len(duvidosas_existentes)}
""")
```



     <input type="file" id="files-d6cd6b47-b432-4a3b-8986-327b34b5618a" name="files[]" multiple disabled
        style="border:none" />
     <output id="result-d6cd6b47-b432-4a3b-8986-327b34b5618a">
      Upload widget is only available when the cell has been executed in the
      current browser session. Please rerun this cell to enable.
      </output>
      <script>// Copyright 2017 Google LLC
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//      http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * @fileoverview Helpers for google.colab Python module.
 */
(function(scope) {
function span(text, styleAttributes = {}) {
  const element = document.createElement('span');
  element.textContent = text;
  for (const key of Object.keys(styleAttributes)) {
    element.style[key] = styleAttributes[key];
  }
  return element;
}

// Max number of bytes which will be uploaded at a time.
const MAX_PAYLOAD_SIZE = 100 * 1024;

function _uploadFiles(inputId, outputId) {
  const steps = uploadFilesStep(inputId, outputId);
  const outputElement = document.getElementById(outputId);
  // Cache steps on the outputElement to make it available for the next call
  // to uploadFilesContinue from Python.
  outputElement.steps = steps;

  return _uploadFilesContinue(outputId);
}

// This is roughly an async generator (not supported in the browser yet),
// where there are multiple asynchronous steps and the Python side is going
// to poll for completion of each step.
// This uses a Promise to block the python side on completion of each step,
// then passes the result of the previous step as the input to the next step.
function _uploadFilesContinue(outputId) {
  const outputElement = document.getElementById(outputId);
  const steps = outputElement.steps;

  const next = steps.next(outputElement.lastPromiseValue);
  return Promise.resolve(next.value.promise).then((value) => {
    // Cache the last promise value to make it available to the next
    // step of the generator.
    outputElement.lastPromiseValue = value;
    return next.value.response;
  });
}

/**
 * Generator function which is called between each async step of the upload
 * process.
 * @param {string} inputId Element ID of the input file picker element.
 * @param {string} outputId Element ID of the output display.
 * @return {!Iterable<!Object>} Iterable of next steps.
 */
function* uploadFilesStep(inputId, outputId) {
  const inputElement = document.getElementById(inputId);
  inputElement.disabled = false;

  const outputElement = document.getElementById(outputId);
  outputElement.innerHTML = '';

  const pickedPromise = new Promise((resolve) => {
    inputElement.addEventListener('change', (e) => {
      resolve(e.target.files);
    });
  });

  const cancel = document.createElement('button');
  inputElement.parentElement.appendChild(cancel);
  cancel.textContent = 'Cancel upload';
  const cancelPromise = new Promise((resolve) => {
    cancel.onclick = () => {
      resolve(null);
    };
  });

  // Wait for the user to pick the files.
  const files = yield {
    promise: Promise.race([pickedPromise, cancelPromise]),
    response: {
      action: 'starting',
    }
  };

  cancel.remove();

  // Disable the input element since further picks are not allowed.
  inputElement.disabled = true;

  if (!files) {
    return {
      response: {
        action: 'complete',
      }
    };
  }

  for (const file of files) {
    const li = document.createElement('li');
    li.append(span(file.name, {fontWeight: 'bold'}));
    li.append(span(
        `(${file.type || 'n/a'}) - ${file.size} bytes, ` +
        `last modified: ${
            file.lastModifiedDate ? file.lastModifiedDate.toLocaleDateString() :
                                    'n/a'} - `));
    const percent = span('0% done');
    li.appendChild(percent);

    outputElement.appendChild(li);

    const fileDataPromise = new Promise((resolve) => {
      const reader = new FileReader();
      reader.onload = (e) => {
        resolve(e.target.result);
      };
      reader.readAsArrayBuffer(file);
    });
    // Wait for the data to be ready.
    let fileData = yield {
      promise: fileDataPromise,
      response: {
        action: 'continue',
      }
    };

    // Use a chunked sending to avoid message size limits. See b/62115660.
    let position = 0;
    do {
      const length = Math.min(fileData.byteLength - position, MAX_PAYLOAD_SIZE);
      const chunk = new Uint8Array(fileData, position, length);
      position += length;

      const base64 = btoa(String.fromCharCode.apply(null, chunk));
      yield {
        response: {
          action: 'append',
          file: file.name,
          data: base64,
        },
      };

      let percentDone = fileData.byteLength === 0 ?
          100 :
          Math.round((position / fileData.byteLength) * 100);
      percent.textContent = `${percentDone}% done`;

    } while (position < fileData.byteLength);
  }

  // All done.
  yield {
    response: {
      action: 'complete',
    }
  };
}

scope.google = scope.google || {};
scope.google.colab = scope.google.colab || {};
scope.google.colab._files = {
  _uploadFiles,
  _uploadFilesContinue,
};
})(self);
</script> 


    Saving dados_abertos_prf-datatran2025.csv to dados_abertos_prf-datatran2025 (2).csv
    
    Arquivo carregado: dados_abertos_prf-datatran2025 (2).csv
    Quantidade de linhas: 72529
    Quantidade de colunas: 72529
    
    === COLUNAS ENCONTRADAS ===
    - id
    - data_inversa
    - dia_semana
    - horario
    - uf
    - br
    - km
    - municipio
    - causa_acidente
    - tipo_acidente
    - classificacao_acidente
    - fase_dia
    - sentido_via
    - condicao_metereologica
    - tipo_pista
    - tracado_via
    - uso_solo
    - pessoas
    - mortos
    - feridos_leves
    - feridos_graves
    - ilesos
    - ignorados
    - feridos
    - veiculos
    - latitude
    - longitude
    - regional
    - delegacia
    - uop
    
    Variável alvo criada: acidente_fatal
    
    
    ======================================================================
    CLASSIFICAÇÃO DAS VARIÁVEIS
    ======================================================================
    
    🟢 VARIÁVEIS PERMITIDAS
    ----------------------------------------
    ✔ uf
    ✔ br
    ✔ km
    ✔ municipio
    ✔ causa_acidente
    ✔ tipo_acidente
    ✔ classificacao_acidente
    ✔ fase_dia
    ✔ sentido_via
    ✔ condicao_metereologica
    ✔ tipo_pista
    ✔ tracado_via
    ✔ uso_solo
    ✔ dia_semana
    ✔ horario
    
    🔴 VARIÁVEIS PROIBIDAS
    ----------------------------------------
    ✘ mortos
    ✘ acidente_fatal
    ✘ feridos_graves
    ✘ feridos_leves
    ✘ ilesos
    ✘ ignorados
    
    🟡 VARIÁVEIS DUVIDOSAS
    ----------------------------------------
    ? pessoas
    ? veiculos
    
    
    ======================================================================
    BASE MODELÁVEL
    ======================================================================
    
    Dimensões:
    Linhas: 72529
    Colunas: 16
    
    Primeiras 10 linhas:




  <div id="df-c35cf791-dbb9-4ff1-b21b-97a837fb74a9" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>uf</th>
      <th>br</th>
      <th>km</th>
      <th>municipio</th>
      <th>causa_acidente</th>
      <th>tipo_acidente</th>
      <th>classificacao_acidente</th>
      <th>fase_dia</th>
      <th>sentido_via</th>
      <th>condicao_metereologica</th>
      <th>tipo_pista</th>
      <th>tracado_via</th>
      <th>uso_solo</th>
      <th>dia_semana</th>
      <th>horario</th>
      <th>acidente_fatal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SP</td>
      <td>116</td>
      <td>225</td>
      <td>GUARULHOS</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Tombamento</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Decrescente</td>
      <td>Céu Claro</td>
      <td>Múltipla</td>
      <td>Reta;Declive</td>
      <td>Sim</td>
      <td>quarta-feira</td>
      <td>06:20:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>CE</td>
      <td>116</td>
      <td>546,2</td>
      <td>PENAFORTE</td>
      <td>Pista esburacada</td>
      <td>Colisão frontal</td>
      <td>NaN</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Simples</td>
      <td>Reta</td>
      <td>Não</td>
      <td>quarta-feira</td>
      <td>07:50:00</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PR</td>
      <td>369</td>
      <td>88,2</td>
      <td>CORNELIO PROCOPIO</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Colisão traseira</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Sol</td>
      <td>Dupla</td>
      <td>Reta;Aclive</td>
      <td>Sim</td>
      <td>quarta-feira</td>
      <td>08:45:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PR</td>
      <td>116</td>
      <td>74</td>
      <td>CAMPINA GRANDE DO SUL</td>
      <td>Reação tardia ou ineficiente do condutor</td>
      <td>Saída de leito carroçável</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Dupla</td>
      <td>Reta</td>
      <td>Não</td>
      <td>quarta-feira</td>
      <td>11:00:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MG</td>
      <td>251</td>
      <td>471</td>
      <td>FRANCISCO SA</td>
      <td>Velocidade Incompatível</td>
      <td>Colisão frontal</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Decrescente</td>
      <td>Chuva</td>
      <td>Simples</td>
      <td>Curva;Declive</td>
      <td>Não</td>
      <td>quarta-feira</td>
      <td>09:30:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>MT</td>
      <td>70</td>
      <td>669</td>
      <td>CACERES</td>
      <td>Transitar na contramão</td>
      <td>Colisão frontal</td>
      <td>Com Vítimas Fatais</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Simples</td>
      <td>Reta</td>
      <td>Não</td>
      <td>quarta-feira</td>
      <td>10:40:00</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>RS</td>
      <td>116</td>
      <td>376</td>
      <td>TAPES</td>
      <td>Ausência de reação do condutor</td>
      <td>Saída de leito carroçável</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Decrescente</td>
      <td>Céu Claro</td>
      <td>Dupla</td>
      <td>Reta</td>
      <td>Não</td>
      <td>quarta-feira</td>
      <td>12:23:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SC</td>
      <td>101</td>
      <td>207,4</td>
      <td>SAO JOSE</td>
      <td>Ausência de reação do condutor</td>
      <td>Colisão traseira</td>
      <td>Com Vítimas Feridas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Nublado</td>
      <td>Dupla</td>
      <td>Reta</td>
      <td>Sim</td>
      <td>quarta-feira</td>
      <td>17:45:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>MG</td>
      <td>116</td>
      <td>708,5</td>
      <td>MURIAE</td>
      <td>Velocidade Incompatível</td>
      <td>Tombamento</td>
      <td>Com Vítimas Fatais</td>
      <td>Anoitecer</td>
      <td>Crescente</td>
      <td>Nublado</td>
      <td>Simples</td>
      <td>Curva</td>
      <td>Não</td>
      <td>quarta-feira</td>
      <td>18:40:00</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>PE</td>
      <td>407</td>
      <td>7,4</td>
      <td>AFRANIO</td>
      <td>Demais falhas mecânicas ou elétricas</td>
      <td>Incêndio</td>
      <td>Sem Vítimas</td>
      <td>Pleno dia</td>
      <td>Crescente</td>
      <td>Céu Claro</td>
      <td>Simples</td>
      <td>Aclive;Curva</td>
      <td>Não</td>
      <td>quarta-feira</td>
      <td>17:00:00</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-c35cf791-dbb9-4ff1-b21b-97a837fb74a9')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-c35cf791-dbb9-4ff1-b21b-97a837fb74a9 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-c35cf791-dbb9-4ff1-b21b-97a837fb74a9');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


    </div>
  </div>



    
    
    ======================================================================
    DISTRIBUIÇÃO DO ALVO — acidente_fatal
    ======================================================================
    acidente_fatal
    0    67319
    1     5210
    Name: count, dtype: int64
    
    Percentual:
    acidente_fatal
    0    92.816666
    1     7.183334
    Name: proportion, dtype: float64
    
    
    ======================================================================
    TABELA DE CLASSIFICAÇÃO
    ======================================================================




  <div id="df-462b1e81-4d86-462e-bd23-24eb1c95845b" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>variavel</th>
      <th>classificacao</th>
      <th>motivo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id</td>
      <td>ANALISAR</td>
      <td>Necessita avaliação antes de entrar no modelo.</td>
    </tr>
    <tr>
      <th>1</th>
      <td>data_inversa</td>
      <td>ANALISAR</td>
      <td>Necessita avaliação antes de entrar no modelo.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>dia_semana</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>horario</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>uf</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>br</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>km</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>municipio</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>causa_acidente</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>tipo_acidente</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>classificacao_acidente</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>fase_dia</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>sentido_via</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>13</th>
      <td>condicao_metereologica</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>14</th>
      <td>tipo_pista</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>tracado_via</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>uso_solo</td>
      <td>PERMITIDA</td>
      <td>Variável explicativa disponível antes ou duran...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>pessoas</td>
      <td>DUVIDOSA</td>
      <td>Pode representar informação relacionada ao des...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>mortos</td>
      <td>PROIBIDA</td>
      <td>Relacionada diretamente ao desfecho ou pode ca...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>feridos_leves</td>
      <td>PROIBIDA</td>
      <td>Relacionada diretamente ao desfecho ou pode ca...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>feridos_graves</td>
      <td>PROIBIDA</td>
      <td>Relacionada diretamente ao desfecho ou pode ca...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>ilesos</td>
      <td>PROIBIDA</td>
      <td>Relacionada diretamente ao desfecho ou pode ca...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>ignorados</td>
      <td>PROIBIDA</td>
      <td>Relacionada diretamente ao desfecho ou pode ca...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>feridos</td>
      <td>ANALISAR</td>
      <td>Necessita avaliação antes de entrar no modelo.</td>
    </tr>
    <tr>
      <th>24</th>
      <td>veiculos</td>
      <td>DUVIDOSA</td>
      <td>Pode representar informação relacionada ao des...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>latitude</td>
      <td>ANALISAR</td>
      <td>Necessita avaliação antes de entrar no modelo.</td>
    </tr>
    <tr>
      <th>26</th>
      <td>longitude</td>
      <td>ANALISAR</td>
      <td>Necessita avaliação antes de entrar no modelo.</td>
    </tr>
    <tr>
      <th>27</th>
      <td>regional</td>
      <td>ANALISAR</td>
      <td>Necessita avaliação antes de entrar no modelo.</td>
    </tr>
    <tr>
      <th>28</th>
      <td>delegacia</td>
      <td>ANALISAR</td>
      <td>Necessita avaliação antes de entrar no modelo.</td>
    </tr>
    <tr>
      <th>29</th>
      <td>uop</td>
      <td>ANALISAR</td>
      <td>Necessita avaliação antes de entrar no modelo.</td>
    </tr>
    <tr>
      <th>30</th>
      <td>acidente_fatal</td>
      <td>ALVO</td>
      <td>Variável que a árvore de decisão deve prever.</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-462b1e81-4d86-462e-bd23-24eb1c95845b')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-462b1e81-4d86-462e-bd23-24eb1c95845b button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-462b1e81-4d86-462e-bd23-24eb1c95845b');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


  <div id="id_199b5b96-af32-4a0e-a852-d2988020279c">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('tabela_classificacao')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_199b5b96-af32-4a0e-a852-d2988020279c button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('tabela_classificacao');
      }
      })();
    </script>
  </div>

    </div>
  </div>



    
    
    ======================================================================
    RESUMO — CONCEITO DE BASE MODELÁVEL
    ======================================================================
    
    
    
    
    
    Total de registros: 72529
    Total de variáveis explicativas: 15
    Total de variáveis proibidas encontradas: 6
    Total de variáveis duvidosas encontradas: 2
    



```python
#Selecionar variáveis modeláveis
variaveis_modelaveis = [
"uf", "br_formatada", "municipio", "mes", "trimestre",
"dia_semana", "dia_semana_num", "fim_de_semana",
"hora", "faixa_horaria", "turno", "fase_dia",
"causa_acidente", "tipo_acidente", "condicao_metereologica",
"tipo_pista", "tracado_via", "uso_solo",
"acidente_fatal"
]
variaveis_modelaveis = [c for c in variaveis_modelaveis if c in df.columns]
base_modelavel = df[variaveis_modelaveis].copy()
print("Base modelável:", base_modelavel.shape)
```

    Base modelável: (72529, 11)



```python
#Verificar data leakage
variaveis_proibidas = [
"mortos", "feridos", "feridos_leves", "feridos_graves",
"total_vitimas", "indice_gravidade", "acidente_grave",
"classificacao_acidente"
]
def verificar_data_leakage(base, proibidas):
 presentes = [c for c in proibidas if c in base.columns]
 if presentes:
  raise ValueError(f"Data leakage detectado: {presentes}")
 return "OK — nenhuma variável proibida encontrada."
verificar_data_leakage(base_modelavel, variaveis_proibidas)
```




    'OK — nenhuma variável proibida encontrada.'




```python
#Tratamento final de nulos na base modelável
for coluna in base_modelavel.columns:
 if coluna == "acidente_fatal":
  continue
if base_modelavel[coluna].dtype == "object" or str(base_modelavel[coluna].dtype) == "string":
   base_modelavel[coluna] = base_modelavel[coluna].fillna("IGNORADO")
else:
 base_modelavel[coluna] = base_modelavel[coluna].fillna(-1)
print(base_modelavel.isna().sum().sort_values(ascending=False).head())
```

    uf                0
    municipio         0
    dia_semana        0
    fase_dia          0
    causa_acidente    0
    dtype: int64



```python
#Exportar bases tratadas
base_analitica.to_csv(ARQUIVO_BASE_ANALITICA, index=False, sep=SEPARADOR,
encoding=ENCODING_SAIDA)
base_modelavel.to_csv(ARQUIVO_BASE_MODELAVEL, index=False, sep=SEPARADOR,
encoding=ENCODING_SAIDA)
print("Arquivos exportados:")
print("-", ARQUIVO_BASE_ANALITICA)
print("-", ARQUIVO_BASE_MODELAVEL)
```

    Arquivos exportados:
    - dados_tratados/base_analitica_prf_2025.csv
    - dados_tratados/base_modelavel_prf_2025.csv



```python
#Reabrir arquivos exportados
valid_analitica = pd.read_csv(ARQUIVO_BASE_ANALITICA, sep=SEPARADOR, encoding=ENCODING_SAIDA)
valid_modelavel = pd.read_csv(ARQUIVO_BASE_MODELAVEL, sep=SEPARADOR, encoding=ENCODING_SAIDA)
print("Analítica reaberta:", valid_analitica.shape)
print("Modelável reaberta:", valid_modelavel.shape)
assert len(valid_analitica) == len(base_analitica)
assert len(valid_modelavel) == len(base_modelavel)
```

    Analítica reaberta: (72529, 44)
    Modelável reaberta: (72529, 11)



```python
#Gerar dicionário das variáveis criadas
linhas_dic = [
{"variavel": "acidente_fatal", "descricao": "1 se mortos >= 1; 0 se mortos = 0", "uso":
"alvo"},
{"variavel": "total_vitimas", "descricao": "mortos + feridos leves + feridos graves", "uso":
"analise/dashboard"},
{"variavel": "indice_gravidade", "descricao": "mortos*3 + feridos_graves*2 + feridos_leves",
"uso": "analise/dashboard"},
{"variavel": "br_formatada", "descricao": "BR padronizada no formato BR-000", "uso":
"analise/modelagem"},
{"variavel": "chave_localidade", "descricao": "UF + município + BR formatada", "uso":
"analise/dashboard"},
]
dicionario = pd.DataFrame(linhas_dic)
dicionario.to_csv(ARQUIVO_DICIONARIO, index=False, sep=SEPARADOR, encoding=ENCODING_SAIDA)
display(dicionario)

```



  <div id="df-15635bb2-e6c3-40cc-8d15-c5284814ca51" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>variavel</th>
      <th>descricao</th>
      <th>uso</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>acidente_fatal</td>
      <td>1 se mortos &gt;= 1; 0 se mortos = 0</td>
      <td>alvo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>total_vitimas</td>
      <td>mortos + feridos leves + feridos graves</td>
      <td>analise/dashboard</td>
    </tr>
    <tr>
      <th>2</th>
      <td>indice_gravidade</td>
      <td>mortos*3 + feridos_graves*2 + feridos_leves</td>
      <td>analise/dashboard</td>
    </tr>
    <tr>
      <th>3</th>
      <td>br_formatada</td>
      <td>BR padronizada no formato BR-000</td>
      <td>analise/modelagem</td>
    </tr>
    <tr>
      <th>4</th>
      <td>chave_localidade</td>
      <td>UF + município + BR formatada</td>
      <td>analise/dashboard</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-15635bb2-e6c3-40cc-8d15-c5284814ca51')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-15635bb2-e6c3-40cc-8d15-c5284814ca51 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-15635bb2-e6c3-40cc-8d15-c5284814ca51');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


  <div id="id_9644cf41-bd4e-4de5-8927-74ebe53e2966">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('dicionario')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_9644cf41-bd4e-4de5-8927-74ebe53e2966 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('dicionario');
      }
      })();
    </script>
  </div>

    </div>
  </div>




```python
#Registrar decisões de tratamento
texto_decisoes = f"""
# Decisões de tratamento — Módulo 4
Data de geração: {datetime.now().strftime('%Y-%m-%d %H:%M')}
## Principais decisões
- Nomes de colunas padronizados para minúsculas, sem acentos e com underline.
- Colunas numéricas convertidas com `pd.to_numeric(errors='coerce')`.
- Datas convertidas com `pd.to_datetime(errors='coerce')`.
- Categorias ausentes relevantes preenchidas como IGNORADO.
- Variável-alvo: acidente_fatal = 1 quando mortos >= 1.
- Base modelável exclui variáveis derivadas do desfecho.
## Arquivos gerados
- {ARQUIVO_BASE_ANALITICA}
- {ARQUIVO_BASE_MODELAVEL}
- {ARQUIVO_DICIONARIO}
"""
ARQUIVO_DECISOES.write_text(texto_decisoes, encoding="utf-8")
print(ARQUIVO_DECISOES)
```

    logs/decisoes_tratamento_modulo4.md



```python
#Criar README do projeto
readme = f"""
# Projeto PRF 2025 — Preparação dos Dados
## Objetivo
Preparar os dados de acidentes da PRF 2025 para análise exploratória, Power BI e árvore de
decisão explicável.
## Variável-alvo
`acidente_fatal = 1` quando `mortos >= 1`; caso contrário, `acidente_fatal = 0`.
## Bases geradas
- `{ARQUIVO_BASE_ANALITICA}`: base completa para EDA e Power BI.
- `{ARQUIVO_BASE_MODELAVEL}`: base para modelagem, sem data leakage.
## Observação metodológica
A base modelável exclui mortos, feridos, total_vitimas, indice_gravidade e variáveis diretamente
derivadas do desfecho.
"""
ARQUIVO_README.write_text(readme, encoding="utf-8")
print("README criado:", ARQUIVO_README)
```

    README criado: README.md



```python
#Resumo final da preparação
resumo_final = pd.DataFrame([
{"item": "linhas_base_analitica", "valor": len(base_analitica)},
{"item": "colunas_base_analitica", "valor": base_analitica.shape[1]},
{"item": "linhas_base_modelavel", "valor": len(base_modelavel)},
{"item": "colunas_base_modelavel", "valor": base_modelavel.shape[1]},
{"item": "taxa_global_acidente_fatal", "valor": base_modelavel["acidente_fatal"].mean()},
])
display(resumo_final)
```



  <div id="df-7ce67c46-d25c-42c2-988f-dbd466719f61" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>item</th>
      <th>valor</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>linhas_base_analitica</td>
      <td>72529.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>colunas_base_analitica</td>
      <td>44.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>linhas_base_modelavel</td>
      <td>72529.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>colunas_base_modelavel</td>
      <td>11.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>taxa_global_acidente_fatal</td>
      <td>0.071833</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-7ce67c46-d25c-42c2-988f-dbd466719f61')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-7ce67c46-d25c-42c2-988f-dbd466719f61 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-7ce67c46-d25c-42c2-988f-dbd466719f61');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


  <div id="id_6f72d91e-8fe0-4fe1-a555-0a8519a14d5a">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('resumo_final')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_6f72d91e-8fe0-4fe1-a555-0a8519a14d5a button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('resumo_final');
      }
      })();
    </script>
  </div>

    </div>
  </div>


