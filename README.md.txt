# deteccao-fraude-cartao

## O problema, e por que o desbalanceamento muda a forma de avaliar
Base real com 284.807 transações, só 0,17% fraude. Modelo que sempre diz "não é fraude" tem 99,83% de acurácia e 0 de utilidade. Por isso acurácia engana. Foco na classe fraude: recall, precisão e F1.

## O que fiz na preparação
- Dataset lido direto pelo link https://storage.googleapis.com/download.tensorflow.org/data/creditcard.csv
- Log_Amount com np.log1p e StandardScaler em Time e Amount
- Mantive V1-V28 (PCA)
- train_test_split com stratify

## Comparação entre modelos
- Regressão Logística balanced: baseline
- Random Forest balanced: melhora recall
- XGBoost scale_pos_weight: melhor recall e F1, escolhido final
Avaliado por classification_report, matriz confusão, ROC e Precision-Recall.

## Limiar e SHAP
Limiar 0.5 perde fraude. Testei 0.3 e 0.2. Escolhi 0.3 porque aumenta recall com pouca perda de precisão.
SHAP mostrou V14, V17, V12, V10 e Amount como mais importantes.

## O que mudei da Expert
Adicionei log no Amount, testei 3 limiares, usei XGBoost como final e GridSearchCV com scoring=recall.