# 🏠 Module 2 — House Prices: предобработка и регрессия

**Автор:** Володина А.А., ПКТб-23-1\
**Дата:** 2026-10-13

## 📊 Результаты

| Модель            | RMSE (log) |  MAE (log) |         R² |   RMSE ($) |
| ----------------- | ---------: | ---------: | ---------: | ---------: |
| Linear Regression |     0.1243 |     0.0881 |     0.9173 |     22 887 |
| Ridge             |     0.1230 |     0.0861 |     0.9189 |     22 362 |
| **Lasso**         | **0.1199** | **0.0823** | **0.9229** | **21 859** |
| ElasticNet        |     0.1206 |     0.0831 |     0.9220 |     21 965 |

**Лучшая модель:** Lasso (`alpha=0.002`), выбрана по кросс-валидации на обучающей выборке. Метрики в таблице рассчитаны на отложенной выборке; R² относится к `log1p(SalePrice)`.\
**Время обучения и подбора:** 0.13 сек (Linear Regression), 0.95 сек (Ridge), 7.03 сек (Lasso), 17.47 сек (ElasticNet).

## 🚀 Быстрый старт

```python
import json
from io import BytesIO

import joblib
import requests

BASE_URL = "https://raw.githubusercontent.com/VolodinaAlexandra/ml-course-volodina/main/module-2-house-prices"

def download(path):
    response = requests.get(f"{BASE_URL}/{path}", timeout=30)
    response.raise_for_status()
    return response.content

model = joblib.load(BytesIO(download("models/best_model.pkl")))
scaler = joblib.load(BytesIO(download("models/scaler.pkl")))
preprocessor = joblib.load(BytesIO(download("models/preprocessor.pkl")))
feature_cols = json.loads(download("models/feature_cols.json").decode("utf-8"))
```

Функция `predict_price()` и пять примеров её использования находятся в [ноутбуке](./notebook.ipynb). Удалённые прогнозы для трёх домов проверены в разделе 11.
