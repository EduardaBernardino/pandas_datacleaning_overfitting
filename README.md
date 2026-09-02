#  Análise e Tratamento de Dados: Preços de Aluguel em São Paulo (QuintoAndar)

Este projeto consiste na limpeza, tratamento e análise exploratória de uma base de dados sobre valores de aluguel de imóveis na cidade de São Paulo, coletados da plataforma QuintoAndar.

    Link dataset: https://www.kaggle.com/datasets/dantebarros/transformed-data-from-quinto-andars-platform
---

##  Visão Geral do Projeto

O objetivo principal deste notebook foi realizar a verificação de consistência e a limpeza inicial dos dados (*data wrangling*), preparando a base para análises estatísticas e possíveis modelagens preditivas de preços de imóveis.

###  Tecnologias e Ferramentas Utilizadas
* **Linguagem:** Python
* **Ambiente:** Databricks / Jupyter Notebook
* **Manipulação de Dados:** `pandas`
* **Visualização de Dados:** `matplotlib`

---

##  Estrutura da Base de Dados

A base conta originalmente com **2.775 registros** e **16 colunas**, abrangendo características físicas e custos associados aos imóveis:

| Coluna | Descrição | Tipo de Dado |
| :--- | :--- | :--- |
| `bairro` | Bairro onde o imóvel está localizado | Texto (`object`) |
| `aluguel` | Valor do aluguel (R$) | Numérico (`float64`) |
| `condominio` | Valor da taxa de condomínio (R$) | Numérico (`float64`) |
| `iptu` | Valor do IPTU (R$) | Numérico (`float64`) |
| `seguro_incendio` | Valor do seguro incêndio (R$) | Numérico (`float64`) |
| `taxa_serviço` | Taxa de serviço da plataforma (R$) | Numérico (`float64`) |
| `total` | Custo total mensal do imóvel (R$) | Numérico (`float64`) |
| `metragem` | Área útil do imóvel em m² | Numérico (`float64`) |
| `quarto` | Quantidade de quartos | Numérico (`float64`) |
| `banheiro` | Quantidade de banheiros | Numérico (`float64`) |
| `vaga_carro` | Quantidade de vagas de garagem | Numérico (`float64`) |
| `andar` | Andar do imóvel | Numérico (`float64`) |
| `aceita_pet` | Indicação se aceita pet (1 = Sim, 0 = Não) | Binário (`float64`) |
| `mobilia` | Indicação se o imóvel é mobiliado (1 = Sim, 0 = Não) | Binário (`float64`) |
| `metro_prox` | Indicação de proximidade ao metrô (1 = Sim, 0 = Não) | Binário (`float64`) |

---

##  Etapas do Tratamento de Dados (Data Cleaning)

1. **Tratamento de Valores Nulos:**
   * **Condomínio:** Foram identificados 7 registros com valor nulo na coluna `condominio`[cite: 1]. Como esses imóveis representavam casas ou locais sem taxa condominial, os valores nulos foram preenchidos com `0`[cite: 1].
   * **IPTU:** 8 registros nulos na coluna `iptu` foram removidos da análise[cite: 1].
2. **Seleção de Atributos:**
   * A coluna `url` foi descartada por não agregar valor analítico/estatístico ao modelo[cite: 1].
3. **Validação do Dataset:**
4. 
---
##  Modelagem com Regressão Linear e Alerta de Overfitting

Neste projeto, foi implementado um modelo de **Regressão Linear** para avaliar a relação entre as variáveis preditoras e a variável alvo.

###  Alerta de Overfitting (Superajuste)
Ao rodar o modelo de Regressão Linear, obteve-se uma pontuação de precisão/acurácia ($R^2$) de **0.99**. 

Esse resultado atipicamente alto acendeu um alerta para o risco de **Overfitting** (ou vazamento de dados/*Data Leakage*). 

#### Hipóteses para o valor de 0,99:
* **Vazamento de Dados (Data Leakage):** A presença de variáveis como `total`, `taxa_serviço` ou `seguro_incendio` no conjunto de treino pode ter fornecido a resposta quase exata do valor do `aluguel` para o algoritmo, gerando uma relação matemática direta/determinística.
* **Ajuste Excessivo:** O modelo memorizou os dados de treino em vez de aprender padrões generalizáveis.

---
   * Após a limpeza, o dataset resultou em **2.767 registros válidos** e **15 colunas**[cite: 1].

---
