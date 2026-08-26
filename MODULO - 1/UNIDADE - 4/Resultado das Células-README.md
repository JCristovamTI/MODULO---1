# Análise de Dados — PRF DataTran 2025

Este README apresenta os resultados obtidos nas células executadas no Google Colab durante a análise dos dados abertos da PRF DataTran 2025.

> Este documento contém apenas os resultados das células, não os códigos utilizados.

---

### Resultado

```text
Pastas verificadas/criadas:
- dados_brutos
- dados_tratados
- notebooks
- sql
- dashboards
- relatorios
- apresentacao
- logs
```

---

### Resultado

```text
Tentando leitura com encoding=latin1...
```

```text
id data_inversa    dia_semana   horario  uf   br     km              municipio                            causa_acidente              tipo_acidente  \
0  652493   2025-01-01  quarta-feira  06:20:00  SP  116    225              GUARULHOS  Reação tardia ou ineficiente do condutor                 Tombamento   
1  652519   2025-01-01  quarta-feira  07:50:00  CE  116  546,2              PENAFORTE                          Pista esburacada            Colisão frontal   
2  652522   2025-01-01  quarta-feira  08:45:00  PR  369   88,2      CORNELIO PROCOPIO  Reação tardia ou ineficiente do condutor           Colisão traseira   
3  652544   2025-01-01  quarta-feira  11:00:00  PR  116     74  CAMPINA GRANDE DO SUL  Reação tardia ou ineficiente do condutor  Saída de leito carroçável   
4  652549   2025-01-01  quarta-feira  09:30:00  MG  251    471           FRANCISCO SA                   Velocidade Incompatível            Colisão frontal   

  classificacao_acidente   fase_dia  sentido_via condicao_metereologica tipo_pista    tracado_via uso_solo  pessoas  mortos  feridos_leves  feridos_graves  \
0    Com Vítimas Feridas  Pleno dia  Decrescente              Céu Claro   Múltipla   Reta;Declive      Sim        2       0              1               0   
1                    NaN  Pleno dia    Crescente              Céu Claro    Simples           Reta      Não        6       1              1               0   
2    Com Vítimas Feridas  Pleno dia    Crescente                    Sol      Dupla    Reta;Aclive      Sim        5       0              3               0   
3    Com Vítimas Feridas  Pleno dia    Crescente              Céu Claro      Dupla           Reta      Não        5       0              1               0   
4    Com Vítimas Feridas  Pleno dia  Decrescente                  Chuva    Simples  Curva;Declive      Não        5       0              1               1   

   ilesos  ignorados  feridos  veiculos      latitude     longitude regional delegacia             uop  
0       0          1        1         2  -23,48586772  -46,54075317  SPRF-SP  DEL01-SP  UOP01-DEL01-SP  
1       1          4        1         6     -7,812288  -39,08333306  SPRF-CE  DEL05-CE  UOP03-DEL05-CE  
2       2          0        3         2    -23,182565    -50,637228  SPRF-PR  DEL07-PR  UOP05-DEL07-PR  
3       4          0        1         2  -25,36517687  -49,04223028  SPRF-PR  DEL01-PR  UOP02-DEL01-PR  
4       1          2        2         4  -16,46801304  -43,43121303  SPRF-MG  DEL12-MG  UOP01-DEL12-MG
```

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

---

### Resultado

```text
/tmp/ipykernel_3993/1744622856.py:5: FutureWarning: 

Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.

  sns.barplot(x='UF', y='Numero de Acidentes', data=uf_accident_counts, palette='viridis')
```

```text
<Figure size 1200x600 with 1 Axes>
```

![Resultado 1](imagens_readme/resultado_1.png)

---

### Resultado

```text
['id', 'data_inversa', 'dia_semana', 'horario', 'uf', 'br', 'km', 'municipio', 'causa_acidente', 'tipo_acidente', 'classificacao_acidente', 'fase_dia', 'sentido_via', 'condicao_metereologica', 'tipo_pista', 'tracado_via', 'uso_solo', 'pessoas', 'mortos', 'feridos_leves', 'feridos_graves', 'ilesos', 'ignorados', 'feridos', 'veiculos', 'latitude', 'longitude', 'regional', 'delegacia', 'uop']
```

---

### Resultado

```text
Colunas faltantes: []
```

---

### Resultado

```text
Dimensões: (72529, 30)
Linhas: 72529
Colunas: 30
```

```text
id data_inversa    dia_semana   horario  uf   br     km              municipio                            causa_acidente              tipo_acidente  \
0  652493   2025-01-01  quarta-feira  06:20:00  SP  116    225              GUARULHOS  Reação tardia ou ineficiente do condutor                 Tombamento   
1  652519   2025-01-01  quarta-feira  07:50:00  CE  116  546,2              PENAFORTE                          Pista esburacada            Colisão frontal   
2  652522   2025-01-01  quarta-feira  08:45:00  PR  369   88,2      CORNELIO PROCOPIO  Reação tardia ou ineficiente do condutor           Colisão traseira   
3  652544   2025-01-01  quarta-feira  11:00:00  PR  116     74  CAMPINA GRANDE DO SUL  Reação tardia ou ineficiente do condutor  Saída de leito carroçável   
4  652549   2025-01-01  quarta-feira  09:30:00  MG  251    471           FRANCISCO SA                   Velocidade Incompatível            Colisão frontal   

  classificacao_acidente   fase_dia  sentido_via condicao_metereologica tipo_pista    tracado_via uso_solo  pessoas  mortos  feridos_leves  feridos_graves  \
0    Com Vítimas Feridas  Pleno dia  Decrescente              Céu Claro   Múltipla   Reta;Declive      Sim        2       0              1               0   
1                    NaN  Pleno dia    Crescente              Céu Claro    Simples           Reta      Não        6       1              1               0   
2    Com Vítimas Feridas  Pleno dia    Crescente                    Sol      Dupla    Reta;Aclive      Sim        5       0              3               0   
3    Com Vítimas Feridas  Pleno dia    Crescente              Céu Claro      Dupla           Reta      Não        5       0              1               0   
4    Com Vítimas Feridas  Pleno dia  Decrescente                  Chuva    Simples  Curva;Declive      Não        5       0              1               1   

   ilesos  ignorados  feridos  veiculos      latitude     longitude regional delegacia             uop  
0       0          1        1         2  -23,48586772  -46,54075317  SPRF-SP  DEL01-SP  UOP01-DEL01-SP  
1       1          4        1         6     -7,812288  -39,08333306  SPRF-CE  DEL05-CE  UOP03-DEL05-CE  
2       2          0        3         2    -23,182565    -50,637228  SPRF-PR  DEL07-PR  UOP05-DEL07-PR  
3       4          0        1         2  -25,36517687  -49,04223028  SPRF-PR  DEL01-PR  UOP02-DEL01-PR  
4       1          2        2         4  -16,46801304  -43,43121303  SPRF-MG  DEL12-MG  UOP01-DEL12-MG
```

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

```text
id data_inversa    dia_semana   horario  uf   br    km   municipio                                     causa_acidente              tipo_acidente  \
6366   691804   2025-03-15        sábado  12:30:00  ES  101    67  SAO MATEUS  Condutor desrespeitou a iluminação vermelha do...        Colisão transversal   
9405   704622   2025-07-13       domingo  22:30:00  PE  423  74,1        JUPI  Condutor deixou de manter distância do veículo...           Colisão traseira   
26102  663260   2025-02-23       domingo  18:10:00  BA  242   231   ITABERABA                                   Animais na Pista    Atropelamento de Animal   
28616  667036   2025-03-13  quinta-feira  19:55:00  DF   20   9,9    BRASILIA           Reação tardia ou ineficiente do condutor              Engavetamento   
1696   660353   2025-02-09       domingo  19:05:00  MA  222   665  ACAILANDIA                           Pedestre andava na pista  Atropelamento de Pedestre   

      classificacao_acidente     fase_dia  sentido_via condicao_metereologica tipo_pista  tracado_via uso_solo  pessoas  mortos  feridos_leves  \
6366     Com Vítimas Feridas    Pleno dia    Crescente                    Sol    Simples    Rotatória      Sim        4       0              0   
9405             Sem Vítimas  Plena Noite  Decrescente              Céu Claro    Simples  Aclive;Reta      Sim        2       0              0   
26102    Com Vítimas Feridas  Plena Noite  Decrescente              Céu Claro    Simples         Reta      Sim        1       0              1   
28616    Com Vítimas Feridas  Plena Noite    Crescente              Céu Claro      Dupla         Reta      Não        6       0              4   
1696     Com Vítimas Feridas  Plena Noite  Decrescente              Céu Claro    Simples      Declive      Não        3       0              1   

       feridos_graves  ilesos  ignorados  feridos  veiculos      latitude     longitude regional delegacia             uop  
6366                2       1          2        2         4  -18,72802869  -39,85997558  SPRF-ES  DEL04-ES  UOP02-DEL04-ES  
9405                0       2          0        0         2    -8,7160879   -36,4219923  SPRF-PE  DEL03-PE  UOP01-DEL03-PE  
26102               0       0          0        1         1    -12,511706    -40,324247  SPRF-BA  DEL06-BA  UOP02-DEL06-BA  
28616               0       2          0        4         3   -15,6502715   -47,7763723  SPRF-DF  DEL02-DF  UOP01-DEL02-DF  
1696                1       0          1        2         3   -4,89367779  -47,38426513  SPRF-MA  DEL04-MA  UOP03-DEL04-MA
```

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

---

### Resultado

```text
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
```

```text
tipo  qtd_colunas
0  object           20
1   int64           10
```

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

---

### Resultado

```text
qtd_nulos  perc_nulos
uop                            38    0.052393
delegacia                      22    0.030333
regional                        2    0.002758
classificacao_acidente          1    0.001379
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

---

### Resultado

```text
Duplicidades exatas: 0
```

---

### Resultado

```text
variavel  qtd_categorias
0                 latitude           69294
1                longitude           69237
2                       km            7655
3                municipio            1844
4                  horario            1412
5              tracado_via             605
6                      uop             395
7             data_inversa             365
8                delegacia             153
9           causa_acidente              69
10                regional              28
11                      uf              27
12           tipo_acidente              17
13  condicao_metereologica               9
14              dia_semana               7
15                fase_dia               4
16             sentido_via               3
17  classificacao_acidente               3
18              tipo_pista               3
19                uso_solo               2
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

---

### Resultado

```text
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
```

---

### Resultado

```text
data_inversa   ano  mes  trimestre  dia_semana_num  fim_de_semana
0   2025-01-01  2025    1          1               2              0
1   2025-01-01  2025    1          1               2              0
2   2025-01-01  2025    1          1               2              0
3   2025-01-01  2025    1          1               2              0
4   2025-01-01  2025    1          1               2              0
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

---

### Resultado

```text
horario  hora  turno
0  06:20:00     6  MANHA
1  07:50:00     7  MANHA
2  08:45:00     8  MANHA
3  11:00:00    11  MANHA
4  09:30:00     9  MANHA
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

---

### Resultado

```text
/tmp/ipykernel_3993/1055991364.py:4: FutureWarning: 

Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.

  sns.barplot(x='turno', y='mortos', data=mortos_por_turno, palette='viridis')
```

```text
<Figure size 1000x600 with 1 Axes>
```

![Resultado 2](imagens_readme/resultado_2.png)

---

### Resultado

```text
faixa_horaria
00h-02h     3959
03h-05h     4948
06h-08h    11517
09h-11h     9342
12h-14h     9678
15h-17h    12624
18h-20h    13473
21h-23h     6988
Name: count, dtype: int64
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

---

### Resultado

```text
Colunas textuais padronizadas: 0
```

---

### Resultado

```text
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
```

---

### Resultado

```text
mortos            0
feridos           0
feridos_leves     0
feridos_graves    0
pessoas           0
veiculos          0
dtype: int64
```

---

### Resultado

```text
acidente_fatal    qtd       perc
0               0  67319  92.816666
1               1   5210   7.183334
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

---

### Resultado

```text
Violações da regra do alvo: 0
```

---

### Resultado

```text
mortos  feridos_leves  feridos_graves  total_vitimas  indice_gravidade
0       0              1               0              1                 1
1       1              1               0              2                 4
2       0              3               0              3                 3
3       0              1               0              1                 1
4       0              1               1              2                 3
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

---

### Resultado

```text
uf              municipio   br br_formatada               chave_localidade
0  SP              GUARULHOS  116         None              SP_GUARULHOS_None
1  CE              PENAFORTE  116         None              CE_PENAFORTE_None
2  PR      CORNELIO PROCOPIO  369         None      PR_CORNELIO PROCOPIO_None
3  PR  CAMPINA GRANDE DO SUL  116         None  PR_CAMPINA GRANDE DO SUL_None
4  MG           FRANCISCO SA  251         None           MG_FRANCISCO SA_None
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

---

### Resultado

```text
{'linhas': 72529,
 'colunas': 44,
 'acidentes_fatais': 5210,
 'taxa_fatalidade': 0.07183333563126473,
 'total_mortos': 6043,
 'total_feridos': 83550}
```

---

### Resultado

```text
causa_acidente    qtd
0                     AUSÊNCIA DE REAÇÃO DO CONDUTOR  11469
1           REAÇÃO TARDIA OU INEFICIENTE DO CONDUTOR  10799
2  ACESSAR A VIA SEM OBSERVAR A PRESENÇA DOS OUTR...   7097
3  CONDUTOR DEIXOU DE MANTER DISTÂNCIA DO VEÍCULO...   4413
4                            VELOCIDADE INCOMPATÍVEL   4088
5                        MANOBRA DE MUDANÇA DE FAIXA   4016
6                   INGESTÃO DE ÁLCOOL PELO CONDUTOR   3685
7               DEMAIS FALHAS MECÂNICAS OU ELÉTRICAS   3385
8                             TRANSITAR NA CONTRAMÃO   2475
9                                  CONDUTOR DORMINDO   2116
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

```text
tipo_acidente    qtd
0                COLISÃO TRASEIRA  14360
1       SAÍDA DE LEITO CARROÇÁVEL  10209
2             COLISÃO TRANSVERSAL   9306
3   COLISÃO LATERAL MESMO SENTIDO   7885
4                      TOMBAMENTO   6351
5              COLISÃO COM OBJETO   5109
6                 COLISÃO FRONTAL   4739
7    QUEDA DE OCUPANTE DE VEÍCULO   3450
8       ATROPELAMENTO DE PEDESTRE   3057
9  COLISÃO LATERAL SENTIDO OPOSTO   2152
```

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

---

### Resultado

```text
tipo_acidente  qtd_acidentes  qtd_fatais  taxa_fatal
1        ATROPELAMENTO DE PEDESTRE           3057         902    0.295061
4                  COLISÃO FRONTAL           4739        1396    0.294577
6   COLISÃO LATERAL SENTIDO OPOSTO           2152         212    0.098513
11                EVENTOS ATÍPICOS            287          23    0.080139
0          ATROPELAMENTO DE ANIMAL           1133          68    0.060018
14       SAÍDA DE LEITO CARROÇÁVEL          10209         605    0.059261
3               COLISÃO COM OBJETO           5109         297    0.058133
2                      CAPOTAMENTO           1373          63    0.045885
7              COLISÃO TRANSVERSAL           9306         427    0.045884
8                 COLISÃO TRASEIRA          14360         619    0.043106
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

---

### Resultado

```text
<Figure size 640x480 with 1 Axes>
```

![Resultado 3](imagens_readme/resultado_3.png)

---

### Resultado

```text
Base analítica: (72529, 44)
Colunas: ['id', 'data_inversa', 'dia_semana', 'horario', 'uf', 'br', 'km', 'municipio', 'causa_acidente', 'tipo_acidente', 'classificacao_acidente', 'fase_dia', 'sentido_via', 'condicao_metereologica', 'tipo_pista', 'tracado_via', 'uso_solo', 'pessoas', 'mortos', 'feridos_leves', 'feridos_graves', 'ilesos', 'ignorados', 'feridos', 'veiculos', 'latitude', 'longitude', 'regional', 'delegacia', 'uop', 'ano', 'mes', 'trimestre', 'dia_semana_num', 'fim_de_semana', 'hora', 'turno', 'faixa_horaria', 'acidente_fatal', 'total_vitimas', 'acidente_grave', 'indice_gravidade', 'br_formatada', 'chave_localidade']
```

---

### Resultado

```text
<IPython.core.display.HTML object>
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

```text
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
```

```text
uf   br     km              municipio                            causa_acidente              tipo_acidente classificacao_acidente   fase_dia  sentido_via  \
0  SP  116    225              GUARULHOS  Reação tardia ou ineficiente do condutor                 Tombamento    Com Vítimas Feridas  Pleno dia  Decrescente   
1  CE  116  546,2              PENAFORTE                          Pista esburacada            Colisão frontal                    NaN  Pleno dia    Crescente   
2  PR  369   88,2      CORNELIO PROCOPIO  Reação tardia ou ineficiente do condutor           Colisão traseira    Com Vítimas Feridas  Pleno dia    Crescente   
3  PR  116     74  CAMPINA GRANDE DO SUL  Reação tardia ou ineficiente do condutor  Saída de leito carroçável    Com Vítimas Feridas  Pleno dia    Crescente   
4  MG  251    471           FRANCISCO SA                   Velocidade Incompatível            Colisão frontal    Com Vítimas Feridas  Pleno dia  Decrescente   
5  MT   70    669                CACERES                    Transitar na contramão            Colisão frontal     Com Vítimas Fatais  Pleno dia    Crescente   
6  RS  116    376                  TAPES            Ausência de reação do condutor  Saída de leito carroçável    Com Vítimas Feridas  Pleno dia  Decrescente   
7  SC  101  207,4               SAO JOSE            Ausência de reação do condutor           Colisão traseira    Com Vítimas Feridas  Pleno dia    Crescente   
8  MG  116  708,5                 MURIAE                   Velocidade Incompatível                 Tombamento     Com Vítimas Fatais  Anoitecer    Crescente   
9  PE  407    7,4                AFRANIO      Demais falhas mecânicas ou elétricas                   Incêndio            Sem Vítimas  Pleno dia    Crescente   

  condicao_metereologica tipo_pista    tracado_via uso_solo    dia_semana   horario  acidente_fatal  
0              Céu Claro   Múltipla   Reta;Declive      Sim  quarta-feira  06:20:00               0  
1              Céu Claro    Simples           Reta      Não  quarta-feira  07:50:00               1  
2                    Sol      Dupla    Reta;Aclive      Sim  quarta-feira  08:45:00               0  
3              Céu Claro      Dupla           Reta      Não  quarta-feira  11:00:00               0  
4                  Chuva    Simples  Curva;Declive      Não  quarta-feira  09:30:00               0  
5              Céu Claro    Simples           Reta      Não  quarta-feira  10:40:00               1  
6              Céu Claro      Dupla           Reta      Não  quarta-feira  12:23:00               0  
7                Nublado      Dupla           Reta      Sim  quarta-feira  17:45:00               0  
8                Nublado    Simples          Curva      Não  quarta-feira  18:40:00               1  
9              Céu Claro    Simples   Aclive;Curva      Não  quarta-feira  17:00:00               0
```

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

```text
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
```

```text
variavel classificacao                                             motivo
0                       id      ANALISAR     Necessita avaliação antes de entrar no modelo.
1             data_inversa      ANALISAR     Necessita avaliação antes de entrar no modelo.
2               dia_semana     PERMITIDA  Variável explicativa disponível antes ou duran...
3                  horario     PERMITIDA  Variável explicativa disponível antes ou duran...
4                       uf     PERMITIDA  Variável explicativa disponível antes ou duran...
5                       br     PERMITIDA  Variável explicativa disponível antes ou duran...
6                       km     PERMITIDA  Variável explicativa disponível antes ou duran...
7                municipio     PERMITIDA  Variável explicativa disponível antes ou duran...
8           causa_acidente     PERMITIDA  Variável explicativa disponível antes ou duran...
9            tipo_acidente     PERMITIDA  Variável explicativa disponível antes ou duran...
10  classificacao_acidente     PERMITIDA  Variável explicativa disponível antes ou duran...
11                fase_dia     PERMITIDA  Variável explicativa disponível antes ou duran...
12             sentido_via     PERMITIDA  Variável explicativa disponível antes ou duran...
13  condicao_metereologica     PERMITIDA  Variável explicativa disponível antes ou duran...
14              tipo_pista     PERMITIDA  Variável explicativa disponível antes ou duran...
15             tracado_via     PERMITIDA  Variável explicativa disponível antes ou duran...
16                uso_solo     PERMITIDA  Variável explicativa disponível antes ou duran...
17                 pessoas      DUVIDOSA  Pode representar informação relacionada ao des...
18                  mortos      PROIBIDA  Relacionada diretamente ao desfecho ou pode ca...
19           feridos_leves      PROIBIDA  Relacionada diretamente ao desfecho ou pode ca...
20          feridos_graves      PROIBIDA  Relacionada diretamente ao desfecho ou pode ca...
21                  ilesos      PROIBIDA  Relacionada diretamente ao desfecho ou pode ca...
22               ignorados      PROIBIDA  Relacionada diretamente ao desfecho ou pode ca...
23                 feridos      ANALISAR     Necessita avaliação antes de entrar no modelo.
24                veiculos      DUVIDOSA  Pode representar informação relacionada ao des...
25                latitude      ANALISAR     Necessita avaliação antes de entrar no modelo.
26               longitude      ANALISAR     Necessita avaliação antes de entrar no modelo.
27                regional      ANALISAR     Necessita avaliação antes de entrar no modelo.
28               delegacia      ANALISAR     Necessita avaliação antes de entrar no modelo.
29                     uop      ANALISAR     Necessita avaliação antes de entrar no modelo.
30          acidente_fatal          ALVO      Variável que a árvore de decisão deve prever.
```

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

```text
======================================================================
RESUMO — CONCEITO DE BASE MODELÁVEL
======================================================================





Total de registros: 72529
Total de variáveis explicativas: 15
Total de variáveis proibidas encontradas: 6
Total de variáveis duvidosas encontradas: 2
```

---

### Resultado

```text
Base modelável: (72529, 11)
```

---

### Resultado

```text
'OK — nenhuma variável proibida encontrada.'
```

---

### Resultado

```text
uf                0
municipio         0
dia_semana        0
fase_dia          0
causa_acidente    0
dtype: int64
```

---

### Resultado

```text
Arquivos exportados:
- dados_tratados/base_analitica_prf_2025.csv
- dados_tratados/base_modelavel_prf_2025.csv
```

---

### Resultado

```text
Analítica reaberta: (72529, 44)
Modelável reaberta: (72529, 11)
```

---

### Resultado

```text
variavel                                    descricao                uso
0    acidente_fatal            1 se mortos >= 1; 0 se mortos = 0               alvo
1     total_vitimas      mortos + feridos leves + feridos graves  analise/dashboard
2  indice_gravidade  mortos*3 + feridos_graves*2 + feridos_leves  analise/dashboard
3      br_formatada             BR padronizada no formato BR-000  analise/modelagem
4  chave_localidade                UF + município + BR formatada  analise/dashboard
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

---

### Resultado

```text
logs/decisoes_tratamento_modulo4.md
```

---

### Resultado

```text
README criado: README.md
```

---

### Resultado

```text
item         valor
0       linhas_base_analitica  72529.000000
1      colunas_base_analitica     44.000000
2       linhas_base_modelavel  72529.000000
3      colunas_base_modelavel     11.000000
4  taxa_global_acidente_fatal      0.071833
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

---

# Resumo

- Etapas encontradas: **0**
- Resultados encontrados: **37**
- Gráficos encontrados: **3**

Os resultados foram extraídos das células executadas no Google Colab.
