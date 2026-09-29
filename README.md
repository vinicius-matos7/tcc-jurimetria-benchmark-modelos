# Modelagem Preditiva de Decisões Judiciais nas Varas de Relações de Consumo da Comarca de Salvador com Aprendizado de Máquina

> **Linha Metodológica (Abordagem 1):** Avaliação comparativa de algoritmos supervisionados sob representação única e paridade de covariáveis (*One-Hot Encoding* e *Target Encoding* com 74 atributos).

Este repositório contém a pesquisa, os datasets, os scripts de coleta da API DataJud (CNJ), os notebooks de experimentação e o artigo em LaTeX (padrão IEEE) referente ao Trabalho de Conclusão de Curso (TCC) no curso de Análise e Desenvolvimento de Sistemas (ADS) do Instituto Federal da Bahia (IFBA - Salvador).

---

## 📁 Estrutura do Repositório

```text
tcc-jurimetria-benchmark-modelos/
├── jurimetria_comparacao.ipynb        # NOTEBOOK MESTRE (Pipeline Jurimétrico, Treinamento e Diagnósticos)
├── overleaf_main.tex                  # Artigo científico diagramado em LaTeX (IEEEtran Conference)
├── arvore.png                         # Figura 2 referenciada no artigo científico
├── vies_variancia.png                 # Figura 1 referenciada no artigo científico
├── requirements.txt                   # Dependências e bibliotecas Python
├── README.md                          # Documentação e instruções de execução
├── .env.example                       # Modelo de configuração de variáveis de ambiente
├── .gitignore                         # Regras de exclusão (bibliografia/ e dados sensíveis)
│
├── data/                              # Datasets processuais extraídos da API pública do DataJud
│   ├── dataset_relacoes_consumo.csv   # Base primária consolidada (2020 a 2024)
│   └── dataset_processado.csv         # Base higienizada com filtragem de mérito
│
├── resultados/                        # Gráficos analíticos oficiais exportados em alta resolução (300 DPI)
│   ├── comparacao_feature_importance_3_modelos.png
│   ├── curva_aprendizado_volume_dados.png
│   ├── curva_calibracao_3_modelos.png
│   ├── curva_pr_3_modelos.png
│   ├── curva_roc_3_modelos.png
│   ├── matrizes_confusao_3_modelos.png
│   ├── top15_coeficientes_regressao_logistica.png
│   └── xgboost_curva_aprendizado.png
│
└── scripts/
    └── extrair_datajud.py             # Script de extração automatizada da API pública do DataJud (TJBA)
```

---

## 🏛️ Metodologia e Modelagem (Abordagem 1)

1. **Base Empírica:** Quase 80 mil litígios de relações de consumo da Comarca de Salvador (TJBA) distribuídos entre 2020 e 2024.
2. **Divisão Temporal Estrita (Anti-Leakage):** Treinamento nos anos históricos (2020 a 2023) e teste cego na safra futura (2024) via `TimeSeriesSplit`.
3. **Representação Tabular Única:** Matriz dimensionalmente simétrica de 74 covariáveis para todos os modelos, aplicando *One-Hot Encoding* para atributos sazonais (mês, dia da semana, trimestre) e assuntos TPU, combinada com *Target Encoding Out-of-Fold* (OOF).
4. **Algoritmos Avaliados:**
   * **Regressão Logística Penalizada (ElasticNet):** Linha de base linear interpretável (*White-Box*).
   * **Random Forest:** Comitê não-paramétrico com redução de variância via *Bagging*.
   * **XGBoost:** Algoritmo de gradiente impulsionado com regularização estrutural via *Boosting*.
5. **Critério de Seleção:** Avaliação de métricas de discriminação (ROC-AUC, Precisão Média, F1-Score) e calibração de probabilidades, fundamentando a decisão final sob o **Princípio da Parcimônia (Navalha de Ockham)**.

---

## 🚀 Como Executar o Projeto

### 1. Clonar e Acessar o Repositório
```bash
git clone https://github.com/SEU_USUARIO/tcc-jurimetria-benchmark-modelos.git
cd tcc-jurimetria-benchmark-modelos
```

### 2. Configurar o Ambiente Virtual e Instalar Dependências
```bash
python -m venv .venv
# No Windows:
.venv\Scripts\activate
# No Linux/Mac:
source .venv/bin/activate

pip install -r requirements.txt
```

### 3. Extração da API DataJud (Opcional)
Para executar nova coleta de dados:
1. Copie o arquivo `.env.example` para `.env`:
   ```bash
   cp .env.example .env
   ```
2. Insira sua chave pública da API DataJud no `.env`.
3. Execute o script:
   ```bash
   python scripts/extrair_datajud.py
   ```

### 4. Executar o Notebook
```bash
jupyter notebook jurimetria_comparacao.ipynb
```

---

## ✒️ Autoria e Afiliação Institucional
* **Autor:** Vinícius Matos dos Santos (`viniciusmatoslyon@gmail.com`)
* **Orientador:** Prof. Pablo Vieira Florentino (`pablovf@ifba.edu.br`)
* **Instituição:** Instituto Federal de Educação, Ciência e Tecnologia da Bahia (IFBA - Campus Salvador)
* **Curso:** Bacharelado em Análise e Desenvolvimento de Sistemas (ADS)
