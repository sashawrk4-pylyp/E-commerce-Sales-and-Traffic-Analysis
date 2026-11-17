# E-commerce Sales and Traffic Analysis

## Project Overview

This project uses SQL, Python, and Tableau to analyze nearly 350,000 sessions from an online store. It examines which markets and product categories generated the most sales, how traffic and sales changed over time, and whether the share of sessions with a purchase differed by device.

## Objectives

- Identify the leading countries, product categories, and traffic channels by sales.
- Compare each device’s share of total sales with its purchase rate.
- Measure the relationship between daily traffic and sales and check how missing sales records affect the result.

## Dataset

The analysis covers 349,545 unique sessions from November 1, 2020 through January 31, 2021. A SQL query combines six tables from the `DA` training dataset in Google BigQuery into a dataset with 19 columns.

- `session` and `session_params` provide session dates, locations, device details, and traffic sources.
- `account_session` and `account` link sessions to registered accounts and provide email verification and subscription status.
- `order` and `product` identify purchased products, their categories, and prices.

Sales are calculated as the sum of recorded product prices. The source does not specify a currency. A purchasing session is a distinct session with at least one recorded product price. The dataset has no separate order identifier.

## Tools & Technologies

- Google BigQuery and SQL for extracting and joining data
- Python in Google Colab, with pandas, NumPy, and SciPy for data preparation and statistical analysis
- Matplotlib and seaborn for charts and heatmaps
- Tableau Public for interactive dashboards

## Analysis Process

1. Joined the six tables, retaining sessions without a linked account or purchase. Checked session identifiers, missing values, and date coverage.
2. Ranked countries and categories by sales, compared the US category mix with the global mix, and summarized sessions by traffic channel and device.
3. Used the Wilcoxon signed-rank test to compare daily sales by account status, the Friedman test to compare daily metrics across groups, and a chi-square test to examine the association between device type and purchasing.
4. Calculated Pearson and Spearman correlations between daily traffic and sales. Compared the 88 days with recorded sales against all 92 days, treating the final four days as zero-sales days in the second calculation.

## Key Findings

- Recorded sales totaled 31.97 million. The US accounted for about 44%. Sofas & armchairs, Chairs, and Beds together generated about 61% of sales both globally and in the US.
- December had the highest recorded sales at 12.42 million. Organic Search led all traffic channels by sales in each of the three months.
- Desktop accounted for 59% of sales. On days with recorded sales, 10.02% of desktop sessions included a purchase, compared with 9.94% on mobile and 9.58% on tablet. The chi-square test found no statistically significant association between device type and purchasing (p = 0.3716).
- Sessions continued on January 28–31, but no product prices were recorded. Pearson’s correlation between daily sessions and sales was 0.93 across the 88 days with recorded sales and 0.79 when the final four days were included with sales set to zero.

## Project Files

- [Analysis notebook](./Portfolio_Project_1%286%29.ipynb) — SQL query, Python analysis, charts, and statistical tests. Rerunning the query in Colab requires access to the BigQuery training dataset.
- [E-commerce Traffic & Sales Overview](https://public.tableau.com/app/profile/oleksandra.karpalova/viz/Book2_17946961792440/E-commerceTrafficSalesOverview) — daily traffic and sales, devices, browsers, and email verification.
- [Sales by Country & Product Category](https://public.tableau.com/app/profile/oleksandra.karpalova/viz/Book2_17946961792440/SalesbyCountryProductCategory) — country map and category sales for the selected market.

## Conclusions

The US accounted for nearly half of recorded sales, and its three leading product categories also led globally. Desktop generated the most sales, while desktop and mobile sessions had similar purchase rates. Before interpreting the change in sales from December to January, it is worth checking whether purchase records are complete for January 28–31.

---

# Аналіз продажів і трафіку інтернет-магазину

## Опис проєкту

У проєкті за допомогою SQL, Python і Tableau проаналізовано майже 350 тисяч сесій інтернет-магазину. Досліджено, які ринки й товарні категорії забезпечили найбільшу суму продажів, як змінювалися трафік і продажі та чи відрізнялася частка сесій із покупкою залежно від типу пристрою.

## Мета проєкту

- Визначити країни, товарні категорії та канали трафіку з найбільшою сумою продажів.
- Для кожного типу пристрою порівняти його внесок у загальну суму продажів із часткою сесій, під час яких відбулася покупка.
- Оцінити зв’язок між денною кількістю сесій і сумою продажів та перевірити, як на результат впливають дні без записів про продажі.

## Набір даних

Аналіз охоплює 349 545 унікальних сесій із 1 листопада 2020 року до 31 січня 2021 року. SQL-запит об’єднує шість таблиць навчального набору `DA` у Google BigQuery та формує вибірку з 19 колонок.

- `session` і `session_params` містять дати сесій, географічні дані, характеристики пристроїв і джерела трафіку.
- `account_session` і `account` пов’язують сесії з акаунтами та містять дані про підтвердження електронної адреси й підписку на розсилку.
- `order` і `product` містять дані про придбані товари, їхні категорії та ціни.

Суму продажів розраховано як суму зафіксованих цін товарів. Валюту в джерелі не зазначено. Сесією з покупкою вважається унікальна сесія, для якої є хоча б один товар із відомою ціною. Окремого ідентифікатора замовлення в наборі даних немає.

## Інструменти та технології

- Google BigQuery та SQL для отримання й об’єднання даних
- Python у Google Colab, pandas, NumPy та SciPy для підготовки даних і статистичного аналізу
- Matplotlib і seaborn для графіків і теплових карт
- Tableau Public для інтерактивних дашбордів

## Процес аналізу

1. Об’єднано шість таблиць зі збереженням сесій без прив’язаного акаунта або покупки. Перевірено ідентифікатори сесій, пропуски та охоплення дат.
2. Побудовано рейтинги країн і товарних категорій за сумою продажів, зіставлено структуру продажів у США із загальною та створено зведені таблиці за каналами трафіку й пристроями.
3. За допомогою критерію Вілкоксона порівняно денні продажі для сесій із прив’язаним акаунтом і без нього. Для порівняння денних показників між кількома групами застосовано критерій Фрідмана, а для перевірки зв’язку між типом пристрою та наявністю покупки — критерій хі-квадрат.
4. Обчислено кореляції Пірсона та Спірмена між денною кількістю сесій і сумою продажів. Розрахунок за 88 днів із зафіксованими продажами порівняно з розрахунком за всі 92 дні, у якому продажі за останні чотири дні прийнято за нуль.

## Основні результати

- Загальна сума зафіксованих продажів становила 31,97 млн. На США припало близько 44%. Дивани й крісла, стільці та ліжка разом забезпечили близько 61% продажів як у США, так і в усій вибірці.
- Найбільшу суму продажів зафіксовано у грудні — 12,42 млн. Органічний пошук лідирував за сумою продажів серед каналів трафіку в кожному з трьох місяців.
- На комп’ютери припало 59% продажів. У дні із зафіксованими продажами частка сесій із покупкою становила 10,02% на комп’ютерах, 9,94% на смартфонах і 9,58% на планшетах. Тест не виявив статистично значущого зв’язку між типом пристрою та наявністю покупки (p = 0,3716).
- 28–31 січня сесії продовжували реєструватися, але записів про товари з ціною не було. За 88 днів із зафіксованими продажами кореляція Пірсона між денною кількістю сесій і сумою продажів становила 0,93. Якщо врахувати останні чотири дні з нульовими продажами, коефіцієнт знижується до 0,79.

## Файли проєкту

- [Ноутбук з аналізом](./Portfolio_Project_1%286%29.ipynb) — SQL-запит, аналіз у Python, графіки та статистичні тести. Для повторного виконання запиту в Colab потрібен доступ до навчального набору даних у BigQuery.
- [E-commerce Traffic & Sales Overview](https://public.tableau.com/app/profile/oleksandra.karpalova/viz/Book2_17946961792440/E-commerceTrafficSalesOverview) — динаміка трафіку й продажів, пристрої, браузери та статус підтвердження електронної адреси.
- [Sales by Country & Product Category](https://public.tableau.com/app/profile/oleksandra.karpalova/viz/Book2_17946961792440/SalesbyCountryProductCategory) — карта країн і продажі за категоріями товарів на вибраному ринку.

## Висновки

На США припала майже половина зафіксованих продажів, а три провідні категорії на цьому ринку лідирували й у всій вибірці. Найбільша сума продажів припала на комп’ютери, хоча частка сесій із покупкою на комп’ютерах і смартфонах була майже однаковою. Перш ніж оцінювати зміну продажів із грудня до січня, варто перевірити повноту записів про покупки за 28–31 січня.
