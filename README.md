# Trabalho Final – Sistemas Inteligentes

Este repositório contém um experimento de classificação supervisionada usando Naive Bayes e K-Nearest Neighbors (KNN) com validação cruzada e comparação de métricas, implementado em um notebook Jupyter (`main.ipynb`).

## Objetivo
- Avaliar o desempenho de modelos clássicos de classificação (Naive Bayes e KNN) em um dataset público com 50 features.
- Aplicar pré-processamento adequado, dividir o conjunto em treino/validação/teste e usar K-Fold (k=5) para avaliação mais robusta.
- Comparar métricas (Acurácia, Precisão, Recall e F1-Score) e visualizar resultados (matrizes de confusão, barras e boxplots).

## Dataset
- O notebook baixa (ou utiliza localmente) o arquivo `dataset.csv` a partir da URL pública informada.
- A coluna-alvo (target) é automaticamente identificada como a primeira coluna do CSV.
- Caso a célula de download falhe ou você esteja sem internet, certifique-se de que `dataset.csv` esteja no diretório raiz do projeto.

## Pipeline do Notebook
1. Carregamento e inspeção do dataset.
2. Identificação do target e separação de features (`X`) e rótulos (`y`).
3. Pré-processamento:
   - Codificação de variáveis categóricas (LabelEncoder) quando necessário.
   - Padronização das features (StandardScaler).
4. Divisão dos dados: 60% treino, 20% validação e 20% teste (estratificada, `random_state=42`).
5. Modelagem:
   - Naive Bayes (GaussianNB).
   - KNN com busca simples do melhor `k` (ímpar entre 1 e 20) usando o conjunto de validação.
6. Avaliação:
   - Métricas no conjunto de validação e teste (Acurácia, Precisão, Recall, F1-Score; `average='weighted'`).
   - K-Fold Cross Validation (k=5) para cada modelo, reportando médias e desvios.
7. Visualizações:
   - Barras com Acurácia e F1 no teste.
   - Boxplots das acurácias no K-Fold.
   - Matrizes de confusão (Naive Bayes e KNN).
8. Resumo final com a comparação e indicação do melhor modelo (por F1-Score).

## Como Executar
Abaixo um passo a passo em Windows PowerShell.

### 1) (Opcional) Criar ambiente virtual
```powershell
py -m venv .venv
. .\.venv\Scripts\Activate.ps1
py -m pip install --upgrade pip
```

### 2) Instalar dependências
```powershell
py -m pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

### 3) Abrir o notebook
Opção A – Jupyter Notebook/Lab:
```powershell
jupyter notebook
# ou
jupyter lab
```
Abra o arquivo `main.ipynb` e execute as células em ordem (Kernel adequado ao ambiente). 

Opção B – VS Code (recomendado):
- Abra a pasta do projeto no VS Code.
- Abra `main.ipynb` e selecione o kernel Python correto (o da sua venv, se criada).
- Execute as células de cima para baixo (Run All).

### Observações importantes
- A primeira célula do notebook baixa o `dataset.csv` via `curl`. Garanta conexão com a internet. Se preferir, mantenha `dataset.csv` localmente e pule o download.
- O código usa `random_state=42` e `stratify` nas divisões para reprodutibilidade.

## Estrutura do Repositório
```
TrabalhoFinalSistemasInteligentes/
├─ dataset.csv          # dataset (pode ser baixado pela 1ª célula)
├─ main.ipynb           # notebook com todo o experimento
└─ README.md            # este arquivo
```

## Resultados
- As métricas e relatórios (incluindo `classification_report`) são exibidos no output do notebook.
- As figuras mostram a comparação entre modelos e as matrizes de confusão.
- O “Melhor modelo” é apontado pelo maior F1-Score no conjunto de teste.

## Próximos Passos (sugestões)
- Adicionar `GridSearchCV` para KNN e explorar outros classificadores (SVM, Random Forest, Logistic Regression).
- Persistir modelos treinados (pickle/joblib) e criar script de inferência.
- Criar um `requirements.txt` para facilitar a instalação reprodutível das dependências.
