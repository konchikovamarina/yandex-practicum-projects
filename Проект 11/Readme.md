# Проект
Создание дашборда по пользовательским событиям для агрегатора
новостей
# Направление деятельности
* Маркетинг-аналитик
* Data Analyst
* Аналитик (универсал)
* BI-аналитик
# СТЕК
* Python
* SQLAlchemy
* PostgreSQL
* dash
* Tableau
* продуктовые метрики
* построение дашбордов
# Задача проекта 
Используя данные Яндекс.Дзена построить дашборд с метриками взаимодействия пользователей с карточками статей
# Описание проекта
* Работу над этим проектом я провела на удаленной машине в сервисе Yandex.Cloud.
* Мной был установлен PostgreSQL, развернута база данных. 
* Затем я написала скрипт пайплайна,который позволил собирать данные за определенный временной период, и настроила его
автономную работу через crontab.
* Для визуализации собранных данных я написала скрипт дашборда с несколькими фильтрами и также запустила его на удаленной машине. 
* По результатам была подготовлена презентация с полученными графиками.

# Проект выполнен
В результате выполнения проекта автоматизирован сбор информации для менеджеров Дениса и Валерии.

* Представленные графики и таблицы отражают текущее поведение пользователей на 24 сентября 2019г..

* Автоматизация в виде дашборда позволяет визуализировать  основные показатели поведения пользователей. Это  позволяет быстрее достичь цели: провести анализ поведения пользователей . 

* Анализируя визиты по темам, установлено: количество визитов в карточках варьируется от 1485- Юмор до 4277- Наука.

* Анализируя относительные изменения внутри  тем  установлено, что изменения варьируются от 1% - тема «Шоу «до 9%- тема «История»

* Наибольшее количество  выпущенных карточек ,более 10 % ,в теме «Семейные отношения», а наименьшее, менее 1% - в теме «Финансы».

* Наибольшее количество соответствий темы и источника  у темы «Рассказы» и источника «Путешествия» - 4587, а наименьшее   у темы «Шоу» и источника  «Еда» - 1 .Но есть  и несколько  пересечений с отсутствующими данными, например  тема «Шоу» и источник «Технологии».
