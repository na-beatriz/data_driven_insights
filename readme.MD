# 📊 Projeto de Análise de Vendas

## 🚀 Descrição

Este projeto realiza uma análise de vendas utilizando dados de um e-commerce. O objetivo é explorar o comportamento de compras ao longo dos meses e gerar visualizações para identificar padrões e tendências.

-----

## 🎯 Objetivo do Projeto

  * Analisar a distribuição de vendas ao longo dos meses.
  * Identificar quais meses tiveram maior e menor volume de pedidos.
  * Visualizar a relação entre o mês e a quantidade de compras através de um gráfico de dispersão.

-----

## 🛠️ Tecnologias e Ferramentas

  * Python 3
  * Pandas
  * Matplotlib
  * Searborn
  * Jupyter Notebook (ambiente de desenvolvimento)
  * Kaggle API (para extração dos dados)

-----

## 📦 Pipeline de Análise

### 🔍 Extração (Extract)

  * Os dados foram extraídos de um dataset do Kaggle utilizando a API da plataforma.
  * O arquivo `kaggle.json` contendo as credenciais é necessário para a extração e deve ser armazenado em um diretório seguro (e.g., `../secrets/kaggle.json`).

<!-- end list -->

```python
import pandas as pd
from kaggle.api.kaggle_api_extended import KaggleApi

# Configuração e autenticação da API Kaggle
api = KaggleApi()
api.authenticate()

# Download e leitura do dataset
# api.dataset_download_files('...caminho do dataset...', path='./data', unzip=True)
# df_vendas = pd.read_csv('./data/dataset.csv')
```

-----

### 🔧 Transformação e Análise

1.  ✅ **Agrupamento dos dados**: O DataFrame de vendas foi agrupado por `id_mes` para contar o número de pedidos em cada mês.
2.  ✅ **Criação de DataFrame**: Um novo DataFrame `df_agrupado` foi criado para armazenar a contagem de pedidos por mês.
3.  ✅ **Visualização**:
      * Foi gerado um gráfico de dispersão (`plt.scatter`) para visualizar a relação entre o mês e a quantidade de pedidos.
      * Títulos, rótulos e a grade foram adicionados para melhorar a legibilidade do gráfico.
      * O gráfico foi salvo como `grafico_dispercao.jpg` na pasta `../img/`.

<!-- end list -->

```python
df_agrupado = df_vendas.groupby('id_mes')['numero_pedido'].count().reset_index(name='qtd_pedidos')

plt.figure(figsize=(10, 6))
plt.scatter(df_agrupado['id_mes'], df_agrupado['qtd_pedidos'], alpha=0.6, color='mediumvioletred')
plt.title('Dispersão: Mês vs Quantidade de Compras', fontsize=14, weight='bold')
plt.xlabel('Mês (ID)', fontsize=12)
plt.ylabel('Quantidade de Pedidos', fontsize=12)
plt.xticks(range(1, 13))
plt.grid(True, linestyle='--', alpha=0.5)
plt.savefig('../img/grafico_dispercao.jpg', format='jpg', dpi=300)
```

-----

## 📑 Estrutura de Diretórios

```
📁 data_driven_insights/
├──📁 data/                                 # Dados brutos
│   ├── sales_data_sample.csv
│   └── (outros arquivos de dados)
├──📁 dictionary/                           # Dicionários de dados e metadados
├──📁 img/                                  # Visualizações geradas
│   └── grafico_dispercao.jpg
│   └── (outras imagens)
├──📁 scripts/                              # Código-fonte e notebooks
│   └── script.ipynb
├──📁 secrets/                              # Credenciais da API Kaggle
│   └── kaggle.json
├── .gitignore                              # Arquivos a serem ignorados pelo Git
└── README.md                               # Documentação do projeto
```

-----

## 📈 Resultados e Insights

O gráfico de dispersão mostra a quantidade de pedidos para cada mês do ano. A partir da imagem, podemos extrair os seguintes insights:

  * **Pico de vendas em Dezembro:** Há um claro pico de compras no último mês do ano (`id_mes=12`), o que é consistente com a temporada de festas e compras de fim de ano. A quantidade de pedidos neste mês é significativamente maior do que nos outros.
  * **Vendas Consistentes:** A maioria dos meses (de 1 a 11) apresenta uma quantidade de pedidos relativamente consistente, variando em um intervalo específico.
  * **Aumento Gradual:** Embora as vendas sejam mais estáveis, parece haver um leve aumento na quantidade de pedidos nos últimos meses antes do pico de dezembro, sugerindo um crescimento sazonal no segundo semestre.

Esses insights são valiosos para o planejamento de estoque, campanhas de marketing e alocação de recursos em diferentes períodos do ano.

-----

## 🔗 Dependências

  * pandas
  * matplotlib
  * kaggle

Instalação:

```bash
pip install pandas matplotlib kaggle
```

-----

## 🤝 Contribuição

Sinta-se à vontade para sugerir melhorias ou colaborar com o projeto.

-----

## 🏷️ Licença

Este projeto está licenciado sob a licença MIT.