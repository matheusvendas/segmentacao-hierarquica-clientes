# 📊 Segmentação de Clientes (Customer Clustering)

Este projeto tem como objetivo realizar a **Segmentação de Clientes** de um e-commerce/varejo utilizando algoritmos de aprendizado de máquina não-supervisionado. Através do histórico de transações, agrupamos os clientes em perfis de comportamento semelhantes.

## 🎯 Objetivo
Analisar a base de vendas (`fato_vendas.csv`), extrair métricas de comportamento baseadas no modelo **RFM** (Recência, Frequência e Valor Monetário), e utilizar **Agrupamento Hierárquico** para descobrir padrões e segmentos naturais na base de clientes.

## 🛠️ Tecnologias Utilizadas
* **Python 3**
* **Pandas & NumPy:** Manipulação e agregação de dados.
* **Scikit-Learn (`PowerTransformer`):** Normalização e padronização para corrigir assimetria (skewness) dos dados e lidar com outliers.
* **SciPy (`linkage`, `dendrogram`, `fcluster`):** Cálculo de distâncias e construção do Agrupamento Hierárquico.
* **Matplotlib & Seaborn:** Visualização de dados e plotagem do Dendrograma.

## 📂 Estrutura do Repositório
* `bases/`: Diretório contendo os dados brutos.
  * `fato_vendas.csv`: Tabela transacional com o histórico de compras dos clientes.
* `distancia.ipynb`: Notebook principal contendo toda a pipeline de dados, desde a agregação até a geração e interpretação dos clusters.
* `.gitignore`: Configuração para ignorar arquivos desnecessários no controle de versão.

## 🧠 Metodologia Aplicada
1. **Agregação de Dados:** Conversão da tabela de transações (vendas) para uma tabela de dimensão de clientes (`dim_clientes`), calculando:
   * **Recência:** Dias desde a última compra.
   * **Frequência:** Quantidade de compras realizadas.
   * **Valor (Monetário):** Soma do valor total gasto pelo cliente.
2. **Feature Scaling:** Aplicação do `PowerTransformer` para lidar com *outliers* e assimetria forte na Recência, garantindo que todas as variáveis tenham exatamente o mesmo peso matemático no cálculo de distâncias.
3. **Clustering:** Aplicação do método de **Ward** (Agrupamento Hierárquico), que foca em minimizar o aumento da variância dentro de cada cluster a cada passo da junção.
4. **Definição de Clusters:** Análise visual do Dendrograma e corte determinístico (`maxclust`) para gerar perfis distintos e acionáveis de clientes.

## 🚀 Como Executar
1. Certifique-se de ter o Python e o Jupyter Notebook instalados em seu ambiente.
2. Instale as bibliotecas dependências necessárias:
   ```bash
   pip install pandas numpy scipy scikit-learn matplotlib seaborn
   ```
3. Inicie o Jupyter e abra o notebook:
   ```bash
   jupyter notebook distancia.ipynb
   ```
4. Execute as células sequencialmente para observar a transformação dos dados, a formação da árvore de clusters e a distribuição final dos clientes.
