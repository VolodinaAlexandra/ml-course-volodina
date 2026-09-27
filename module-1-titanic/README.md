# 🚢 Module 1 — Titanic: EDA + бинарная классификация

**Автор:** Володина А.А., ПКТб-23-1  
**Дата:** 2026-09-27

## 📊 Результаты

| Модель              | Accuracy | Precision | Recall | F1     | ROC-AUC |
| ------------------- | -------- | --------- | ------ | ------ | ------- |
| Logistic Regression | 0.8045   | 0.7833    | 0.6812 | 0.7287 | 0.8486  |
| Decision Tree       | 0.7821   | 0.7419    | 0.6667 | 0.7023 | 0.8132  |

**Время обучения:** 0.0073 сек (LR), 0.0027 сек (DT)

## 🚀 Быстрый старт

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/username/ml-course-volodina/main/module-1-titanic"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/lr_model.pkl").content))
```
