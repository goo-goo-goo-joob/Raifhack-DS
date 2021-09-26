# Raifhack-DS

# Финальное решение:
#### Данные из внешних источников

* Датасет 1 https://rosstat.gov.ru/labor_market_employment_salaries
Среднемесячная начисленная зарплата наемных работников в организациях, у ИП и физических лиц.
Информация о среднемесячной начисленной заработной плате наемных работников в организациях, у индивидуальных предпринимателей и физических лиц (среднемесячном доходе от трудовой деятельности).
Квартальная оценка среднемесячной начисленной заработной платы наемных работников в организациях, у индивидуальных предпринимателей и физических лиц.

* Датасет 2 https://rosstat.gov.ru/folder/12781
Оперативная информация.
Оценка численности постоянного населения на 1 января 2021 г. и в среднем за 2020 г.

* Датасет 3 https://rosstat.gov.ru/labor_market_employment_salaries
Просроченная задолженность по заработной плате работникам организаций, не относящихся к субъектам малого предпринимательства, по субъектам Российской Федерации c 2019 года.

* Датасет 4 https://rosstat.gov.ru/storage/mediabank/edn07_2021.htm лист t1_2.
ЕСТЕСТВЕННОЕ ДВИЖЕНИЕ НАСЕЛЕНИЯ В РАЗРЕЗЕ СУБЪЕКТОВ РОССИЙСКОЙ ФЕДЕРАЦИИ за июль 2021 года.

#### woe-скоры
woe-скоры определяют вероятность принадлежности объекта к одной из 10 ценовых категорий (один из самых фажных факторов)

#### гео-факторы
* аггрегаты по ценам объектов в радиусе 10 км от исследуемого
* pygeohash-фактор, построенный на широте и долготе

#### Обучение K-means модели и добавление кластера как фактора
* кластеризация на широте и долготе
* кластеризация на osm-факторах

#### Предобработка факторов этаж и улица

#### Добавление новых логических факторов

#### Обучение модели 
* на размеченных в ручную объектах (определено экспериментальным путем, в тестовой выборке представлены объекты только ручной разметки)
* на логарифмированный таргет (подобрано экспериментальным путем, ошибка в таком случае лучше минимизируется)
* на отобранных факторах (список факторов сокращен таким образом, чтобы модель на сокращенном списке факторов давала качество не хуже, чем на полном списке факторов)
* на подобранных гиперпараметрах (с помощью алгоритма optuna)

#### Что было попробовано, но не использовалось в итоговом решении
* LightAutoML
* Дополнительные источники данных и некоторые логические и гео-факторы не использовались финальной моделью
* Добавление в обучающую выборку объектов не ручной разметки с нулевой ошибкой после обучения модели

# Ключевые моменты публичного решения
* генерация гео-факторов
* предобработка факторов этаж и улица
* обучение модели только на размеченных в ручную объектах
* скор на лидерборде 1.7563 (с помощью небольших изменений полученного решения можно получить скор 1.4387)

# Описание

* requirements.txt - стандартный requirements для pip
```bash
pip install -r requirements.txt 
```
* additional_data - дополнительные данные с сайта Росстата

* woe_features.ipynb - генератор WOE признаков. Необходимо выполнить до запуска основного ноутбука
```bash
jupyter nbconvert --to notebook --execute woe_features.ipynb
```

* public_solution_final.ipynb - Ноутбук с обучением основной модели и получением предсказания
```bash
jupyter nbconvert --to notebook --execute public_solution_final.ipynb
```
* final_submision.csv - итоговый сабмит
* public_solution_final.nbconvert.ipynb - визуализированный ноутбук

# License
© [Aleksey Podchezertsev](https://github.com/AsciiShell),
  [Mariia Samodelkina](https://github.com/goo-goo-goo-joob), 2021. 
Licensed under the MIT License. See LICENSE file for more details.
