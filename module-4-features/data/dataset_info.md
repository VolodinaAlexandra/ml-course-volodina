# Online Shoppers Purchasing Intention Dataset

Авторы: C. Sakar и Y. Kastro (2018). DOI: [10.24432/C5F88Q](https://doi.org/10.24432/C5F88Q).
Источник: [UCI](https://archive.ics.uci.edu/dataset/468/online+shoppers+purchasing+intention+dataset).
Лицензия CC BY 4.0. Исходный CSV сохранён без изменения 2026-11-02.
SHA-256: b3055ee355f59134d851d32641183cb4a8b45def7124d2f50442a042f358e0d9

12 330 сессий; 17 признаков и Revenue. False — 10 422 (84,53%), True — 1908 (15,47%).
По смыслу 10 числовых полей, 7 категорий, включая Month и Weekend.
Пропусков нет. Технические коды OperatingSystems, Browser, Region и TrafficType — категории.
Month содержит Feb, Mar, May, June, Jul, Aug, Sep, Oct, Nov, Dec.
Полных повторов 125; для обучения они удаляются, CSV сохраняется исходным.
После очистки 12205 строк; train 9764, test 2441 с stratify.

Десять новых признаков: TotalPages, TotalDuration, AvgPageValue, BounceExitRatio, IsNewVisitor,
IsWeekend, MonthNum, IsHighTraffic, MonthSin, MonthCos. Формулы приведены в разделе 5.
OneHotEncoder обучается на train, отдельно внутри каждого CV-блока.
PageValues описывает транзакционную ценность страниц; проверена чувствительность без него.
Нет полной даты, событийного порядка, координат, свободного текста или повторной истории пользователя.
