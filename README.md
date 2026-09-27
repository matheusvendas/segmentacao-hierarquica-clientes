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
4. **Definição de Clusters:** A formação final dos grupos foi realizada com a função `fcluster`. Durante a fase de análise, observou-se que cortar a árvore por distância (`criterion='distance', t=15`) ou por limite de grupos (`criterion='maxclust', t=3`) gerava exatamente o mesmo resultado para o volume atual de dados. No entanto, **optou-se formalmente pela abordagem `maxclust` devido ao contexto de aplicação corporativa:**
   * Se usássemos o critério de `distance`, o modelo ficaria dependente da variância estatística exata desta "fotografia" dos dados. Ao automatizar a execução deste algoritmo em produção (ex: rodando mensalmente com dados novos), pequenas oscilações de mercado fariam a distância `15` gerar subitamente 2, 4 ou 5 clusters, quebrando processos das áreas de negócio.
   * A escolha por `maxclust=3` traz **previsibilidade operacional**. As áreas de Marketing e CRM preparam "réguas de relacionamento" específicas (ex: campanhas para *VIPs, Regulares e Inativos*). Garantir sempre a saída estrita de 3 segmentos assegura que os fluxos de automação e as estratégias de comunicação da empresa nunca quebrem por flutuações matemáticas.

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
