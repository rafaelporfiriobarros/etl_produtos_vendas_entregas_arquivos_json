# ETL Pipeline para Consolidação e Cálculo de KPI de Vendas

Este repositório contém um pipeline ETL (Extract, Transform, Load) que consolida dados de arquivos JSON, calcula o KPI de vendas e exporta os resultados em formatos CSV e/ou Parquet.

## 📂 Estrutura do Projeto

```
📦 projeto-etl
 ┣ 📂 data              # Pasta contendo os arquivos JSON de entrada
 ┣ 📜 etl.py            # Script principal do ETL
 ┣ 📜 pipeline.py       # Script que executa o pipeline
 ┣ 📜 README.md         # Documentação do projeto
```

## 📌 Dependências

Este projeto requer as seguintes bibliotecas Python:

- pandas

Instale as dependências com:

```bash
pip install pandas
```

## 🛠️ Funcionalidades

### 🔹 `etl.py`

Este arquivo contém as funções para cada etapa do processo ETL.

- **`extrair_dados_e_consolidar(pasta: str) -> pd.DataFrame`**
  - Lê e consolida todos os arquivos JSON dentro da pasta especificada.
  - Retorna um `DataFrame` com os dados combinados.

- **`calcular_kpi_de_total_de_vendas(df: pd.DataFrame) -> pd.DataFrame`**
  - Calcula o total de vendas multiplicando `Quantidade` por `Venda` e adiciona uma nova coluna `Total`.
  - Retorna um `DataFrame` atualizado.

- **`carregar_dados(df: pd.DataFrame, format_saida: list)`**
  - Salva o `DataFrame` nos formatos especificados: CSV, Parquet ou ambos.
  - Parâmetro `format_saida`: lista contendo `"csv"`, `"parquet"` ou ambos.

- **`pipeline_calcular_kpi_de_vendas_consolidado(pasta: str, formato_de_saida: list)`**
  - Executa todas as etapas ETL: extração, transformação e carregamento.

### 🔹 `pipeline.py`

Este arquivo executa o pipeline ETL chamando a função principal do `etl.py`.

```python
from etl import pipeline_calcular_kpi_de_vendas_consolidado

pasta_argumento: str = 'data'
formato_de_saida: list = ["csv"]

pipeline_calcular_kpi_de_vendas_consolidado(pasta_argumento, formato_de_saida)
```

## 🚀 Como Executar

1. Certifique-se de que os arquivos JSON estejam na pasta `data/`.
2. Execute o script `pipeline.py`:

```bash
python pipeline.py
```
3. O resultado será salvo nos arquivos `dados.csv` e/ou `dados.parquet`, dependendo do formato especificado.

## 📌 Exemplo de Uso

Se houver arquivos JSON dentro da pasta `data/` no seguinte formato:

```json
{
    "Produto": "Notebook",
    "Quantidade": 2,
    "Venda": 2500
}
```

O resultado salvo em `dados.csv` será:

```
Produto,Quantidade,Venda,Total
Notebook,2,2500,5000
```

