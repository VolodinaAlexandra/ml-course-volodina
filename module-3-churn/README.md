# 📉 Module 3 — Customer Churn: ансамблевые методы

**Автор:** Володина А.А., ПКТб-23-1  
**Дата:** 2026-10-27

## 📊 Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Random Forest | 0.7601 | 0.5346 | 0.7433 | 0.6219 | 0.8388 |
| XGBoost | 0.7573 | 0.5335 | 0.6818 | 0.5986 | 0.8265 |
| LightGBM | 0.7573 | 0.5305 | 0.7433 | 0.6192 | 0.8366 |
| CatBoost | 0.7544 | 0.5263 | 0.7487 | 0.6181 | 0.8378 |
| **LightGBM (Optuna)** | 0.7452 | 0.5128 | 0.8021 | 0.6257 | 0.8502 |

**Время обучения:** Random Forest: 1.174 с, XGBoost: 0.401 с, LightGBM: 0.252 с, CatBoost: 1.262 с.

**Optuna:** 30 испытаний, 5-fold train CV; ROC-AUC 0.8405 → 0.8496. Поиск: 38.40 с. Финальный fit: 0.271 с.

Таблица показывает тестовые метрики при пороге 0,5. Параметры выбраны по train CV. Категории кодируются LabelEncoder по заданию; scaler сохраняется, но не применяется к деревьям.

## 🚀 Быстрый старт

```powershell
cd module-3-churn
python -m pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

Полный код и его результаты находятся в последней исполняемой ячейке notebook.ipynb. Для открытия Jupyter установите notebook, если он ещё не установлен.

Загрузка из опубликованной ветки main:

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/VolodinaAlexandra/ml-course-volodina/main/module-3-churn"
response = requests.get(f"{BASE_URL}/models/best_model.pkl", timeout=30)
response.raise_for_status()
model = joblib.load(BytesIO(response.content))
```

Для сырых клиентов нужны также label_encoders.pkl, preprocessor.json, feature_cols.json и функция transform_clients() из ноутбука. Локальная и raw-загрузка проверены на трёх клиентах: классы и вероятности совпали.

## 📁 Структура

- notebook.ipynb — 14 разделов и выполненные ячейки;
- последняя ячейка ноутбука — полный код с разделителями # %% и результатами;
- data/ — датасет и описание;
- models/ — пять моделей, scaler, кодировщики, метрики и история Optuna;
- examples/ — EDA, важности, ROC, матрица ошибок и четыре SHAP-графика;
- requirements.txt — версии выполненного окружения.
