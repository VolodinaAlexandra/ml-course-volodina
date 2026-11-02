# 🛒 Module 4 — Online Shoppers: инженерия признаков

**Автор:** Володина А.А., ПКТб-23-1  
**Дата:** 2026-11-02

## 📊 Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC | Время fit, с |
|---|---:|---:|---:|---:|---:|---:|
| Random Forest | 0.8726 | 0.5617 | 0.8455 | 0.6750 | 0.9332 | 1.621 |
| XGBoost | 0.8791 | 0.5893 | 0.7513 | 0.6605 | 0.9300 | 0.717 |
| LightGBM | 0.8714 | 0.5632 | 0.7932 | 0.6587 | 0.9321 | 0.396 |
| CatBoost | 0.8734 | 0.5662 | 0.8168 | 0.6688 | 0.9328 | 2.135 |
| LightGBM (Optuna) | 0.8664 | 0.5470 | 0.8534 | 0.6667 | 0.9365 | 0.361 |

**Optuna:** 30 trials, 5-fold train CV, 0.9269 → 0.9352. Время поиска **54.90 с**.

Тест не используется в подборе параметров; классы вычисляются с порогом 0,5. Из 12 330 строк исключены 125 полных повторов. Новые признаки: восемь обязательных и MonthSin/MonthCos. One-Hot обучается только по train; scaler сохранён, но не применяется к деревьям.

**Проверка Feature Engineering:** CV AUC исходных признаков 0.926775, расширенных 0.926886; заметного выигрыша не показано. Без PageValues/AvgPageValue — 0.7724. Итоговые сессионные агрегаты требуют проверки доступности при реальном прогнозе.

## 🚀 Быстрый старт

```powershell
cd module-4-features
python -m pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

Если Jupyter ещё не установлен, установите пакет notebook. Последняя ячейка ноутбука содержит полный код и результаты.

Загрузка из опубликованной ветки main:

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/VolodinaAlexandra/ml-course-volodina/main/module-4-features"
response = requests.get(f"{BASE_URL}/models/best_model.pkl", timeout=30)
response.raise_for_status()
model = joblib.load(BytesIO(response.content))
```

Для исходных сессий загрузите также encoder.pkl, preprocessor.json, feature_cols.json и используйте transform_sessions() из ноутбука. Статус проверки хранится в models/load_verification.json.

## 📁 Структура

- notebook.ipynb — 14 разделов, выполненные ячейки и приложение;
- data/ — исходный CSV и dataset_info.md;
- models/ — пять моделей, One-Hot, scaler, метрики и история Optuna;
- examples/ — EDA, таблица метрик, ROC, матрица ошибок, важности и четыре SHAP-графика;
- requirements.txt — проверенные версии Python-пакетов.

Источник данных: [UCI, Sakar & Kastro, 2018](https://doi.org/10.24432/C5F88Q), CC BY 4.0.

Проверка raw-загрузки выполнена: классы и вероятности для трёх исходных сессий совпали с локальными. Последняя ячейка выполнена с сохранением всех результатов.
