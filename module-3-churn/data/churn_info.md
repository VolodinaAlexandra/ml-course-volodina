# Telco Customer Churn

Источник задания: [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).
Использованная копия: [IBM CSV](https://github.com/IBM/telco-customer-churn-on-icp4d/blob/master/data/Telco-Customer-Churn.csv).
Файл telco_churn.csv, скачан 2026-10-27.
SHA-256: 16320c9c1ec72448db59aa0a26a0b95401046bef5d02fd3aeb906448e3055e91

7043 строки, 21 столбец: 19 объясняющих признаков, customerID и Churn.
No — 5174 (73,46%), Yes — 1869 (26,54%). Цель Yes=1, No=0.
По смыслу 3 непрерывных числовых признака и 16 категориальных, включая SeniorCitizen.
После to_numeric обнаруживаются 11 NaN в TotalCharges у клиентов с tenure=0.

Демография: gender, SeniorCitizen, Partner, Dependents.
Услуги: PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup,
DeviceProtection, TechSupport, StreamingTV, StreamingMovies.
Аккаунт: tenure, Contract, PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges.

ID исключён. Доли train/test сохраняются через stratify. Медиана и LabelEncoder обучаются
только на train и отдельно внутри каждого CV-блока. Это учебный срез, а не временной ряд.
