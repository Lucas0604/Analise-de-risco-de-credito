# Análise de Risco de Crédito — Carteira de Empréstimos Pessoais

Projeto de Exploratory Data Analysis (EDA) desenvolvido como parte de uma trilha prática de Data Analytics com foco no setor de Bancos/Fintechs.

## 📌 Contexto de Negócio

O time de Risco de Crédito de um banco precisa investigar por que a inadimplência da carteira de empréstimos pessoais subiu no último trimestre. Este projeto simula a primeira etapa desse trabalho: um raio-x exploratório da base de clientes, para orientar a diretoria antes de qualquer modelagem preditiva mais robusta.

## ❓ Perguntas de Negócio

1. Clientes mais jovens (< 25 anos) têm proporção maior de crédito "ruim"?
2. O propósito do empréstimo (carro, negócios, eletrodomésticos etc.) influencia o risco?
3. Empréstimos de valor mais alto e duração mais longa concentram mais risco?
4. Quais são os KPIs essenciais da carteira (taxa de inadimplência geral, por perfil, e ticket médio)?

## 🗂️ Dataset

*German Credit Risk - With Target* (Leonardo Ferreira, base derivada do UCI Statlog German Credit Data)
Fonte: https://www.kaggle.com/datasets/kabure/german-credit-data-with-risk

Colunas principais: Age, Sex, Job, Housing, Saving accounts, Checking account, Credit amount, Duration, Purpose, Risk (good/bad).

> A coluna Risk utilizada é a label real do dataset (derivada do desfecho histórico de pagamento), e não uma regra construída manualmente — ponto importante detalhado na seção "Lições Aprendidas" abaixo.

## 🧪 Metodologia

1. *Limpeza e tratamento de dados*
   - Tratamento de nulos em Saving accounts e Checking account (preenchidos como 'not specified', tratando ausência de conta como categoria de negócio, não como dado faltante aleatório)
   - Conversão de tipos (category para variáveis categóricas)
   - Verificação de duplicatas
2. *Análise Exploratória (EDA)* guiada pelas 3 hipóteses de negócio acima
3. *Visualizações* (matplotlib / seaborn): distribuição de idade por risco, dispersão de valor de crédito por risco, taxa de inadimplência por propósito
4. *Cálculo de KPIs*: taxa de inadimplência geral, por faixa etária e por propósito; ticket médio geral e por categoria de risco
5. *Tratamento de desafios de produção*: verificação de desbalanceamento de classes e detecção/tratamento de outliers via IQR

## ⚠️ Lições Aprendidas (parte importante do processo)

Uma versão inicial deste projeto cometeu um erro clássico de análise de risco: a coluna Risk foi construída manualmente a partir das mesmas variáveis usadas depois para "testar" as hipóteses (ex: valor do crédito e duração), gerando *raciocínio circular* — a conclusão já estava embutida na definição da label. O projeto foi corrigido para usar a label real do dataset. Documentar esse tipo de erro faz parte do processo de aprendizado em Data Analytics e é um problema real que acontece em ambientes de produção.

## 📁 Estrutura do Projeto


├── data/
│   └── german_credit_data.csv
├── analise_corrigida.ipynb
└── README.md


## ▶️ Como Executar

bash
pip install pandas numpy matplotlib seaborn
jupyter notebook analise_corrigida.ipynb

## 🚀 Próximos Passos

- Modelagem preditiva (classificação) com tratamento de desbalanceamento (ex: class_weight, oversampling)
- Validação estatística das diferenças encontradas entre grupos (ex: teste qui-quadrado)
- Comparação com dados públicos de inadimplência do Banco Central (SGS/BACEN) para contextualizar os achados

## 👤 Autor

Projeto desenvolvido como parte de uma trilha de estudos prática em Data Analytics, nível iniciante/intermediário em Python.
