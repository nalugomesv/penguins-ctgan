# Geração de Dados Sintéticos com CTGAN no Conjunto Palmer Penguins

## Objetivo
Este projeto investiga o uso da **Conditional Tabular GAN (CTGAN)**, implementada por meio da [SDV – Synthetic Data Vault](https://sdv.dev/), para gerar dados sintéticos realistas a partir do conjunto **Palmer Penguins**.  
O objetivo principal é avaliar se modelos generativos conseguem preservar a **fidelidade estatística** e a **plausibilidade biológica** de dados tabulares reais, possibilitando seu uso em contextos de pesquisa com coleta limitada ou de alto custo.

## Contexto e Motivação
A escassez de dados é um desafio recorrente em estudos biológicos e ecológicos, onde a coleta amostral pode ser cara, restrita ou logisticamente inviável.  
A geração de dados sintéticos surge como alternativa para:  
- Ampliar conjuntos de dados, preservando estrutura e privacidade.  
- Apoiar o treinamento de modelos de aprendizado de máquina com maior capacidade de generalização.  
- Viabilizar experimentos reprodutíveis sem depender exclusivamente de dados sensíveis ou de difícil acesso.  

## Dataset Utilizado
Foi utilizado o [Palmer Penguins dataset](https://allisonhorst.github.io/palmerpenguins/), composto por medidas morfológicas e informações categóricas de três espécies de pinguins (*Adélie, Chinstrap e Gentoo*) do Arquipélago Palmer (Antártida).  

## Pipeline
1. **Análise Exploratória (EDA)**  
   – Inspeção visual e estatística descritiva das variáveis.  
2. **Pré-processamento**  
   – Tratamento de valores ausentes (imputação pela moda).  
3. **Treinamento do CTGAN**  
   – Configuração de hiperparâmetros (épocas, batch size, discriminator steps).  
   – Aplicação de **restrições morfológicas e biogeográficas** para garantir plausibilidade ecológica.  
4. **Avaliação**  
   – **Relatórios SDV**: validade, cobertura e similaridade estatística.  
   – **Originalidade**: métrica *New Row Synthesis*.  
   – **Classifier Two-Sample Test (C2ST)** com **AUROC**.  
   – **Testes de generalização**: TRTS (Train on Real, Test on Synthetic) e TSTR (Train on Synthetic, Test on Real).  

## Principais Resultados
- **Validade estrutural**: 100%.  
- **Similaridade univariada (Column Shapes)**: ~95%.  
- **Similaridade multivariada (Column Pair Trends)**: ~89%.  
- **Originalidade**: ~99,6% das instâncias são inéditas.  
- **AUROC (C2ST)**: ~0,55 ± 0,03 → dados sintéticos estatisticamente próximos aos reais.  
- Restrições eliminaram **combinações biologicamente incoerentes**, como espécies em ilhas incompatíveis.  

## Próximos Passos
- Expandir a abordagem para outros conjuntos biológicos.  
- Avaliar modelos alternativos (TVAE, TabDDPM, modelos baseados em difusão).  
- Incorporar restrições adicionais com base em informações ecológicas e filogenéticas.  
- Incluir métricas de privacidade, como Distance to Closest Record (DCR).  
- Testar impacto da inclusão de dados sintéticos em modelos preditivos.  

## Estrutura do Repositório

├── data/

│ ├── dados_sinteticos.json # primeiro dataset sintético gerado

│ └── metadata.json # metadados do dataset

├── notebooks/

│ ├── eda_palmer_penguins.ipynb # análise exploratória

│ ├── sdv_palmer_penguins.ipynb # treinamento do CTGAN

│ └── evaluation/ # notebooks de avaliação

│ ├── auroc.ipynb # implementação do AUROC (C2ST)

│ └── avaliacao_penguins_sintetico.ipynb # avaliação complementar dos dados

├── LICENSE # licença do projeto

└── README.md # documentação principal

## Referências
- Inflammatix (2023). *Lessons learned for generative AI for tabular data*.  
  Disponível em: [https://inflammatix.com/lessons-learned-for-generative-ai-for-tabular-data-blog/](https://inflammatix.com/lessons-learned-for-generative-ai-for-tabular-data-blog/)  
- Patki, N.; Wedge, R.; Veeramachaneni, K. (2016). *The Synthetic Data Vault*. IEEE DSAA.  
- Xu, L.; Skoulakis, M.; Cuesta-Infante, A.; Veeramachaneni, K. (2019). *Modeling tabular data using conditional GAN*. NeurIPS.  
- Gorman, K.B.; Williams, T.D.; Fraser, W.R. (2014). *Ecological sexual dimorphism and environmental variability within a community of Antarctic penguins (genus Pygoscelis)*. PLoS ONE.  
- Kang, H.Y.J. et al. (2023). *Synthetic tabular data in healthcare: validation using GANs*. JMIR Medical Informatics.
