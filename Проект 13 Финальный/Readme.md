# Проект
Выпускной проект
# Направление деятельности
* Data Analyst
* Аналитик (универсал)
# Задачи проекта
На основе всех полученных данных в курсе выполнить буткемп-проект по одной из выбранной областей:
- мобильные приложения;
# Описание проекта
Финальный проект включает в себя :
* работу над основным проектом «Ненужные вещи» — ваши ненужные вещи нужны кому-то другому!
* следует дать предложения по улучшению приложения для продажи ненужных вещей,
* задача по A/B-тестированию и SQL,
* и создание дашборда.

# Проект в 3 частях выполнен.

## Часть 1.По результатам исследования сделаны выводы.
* На их основании можно порекомендовать формировать данные для анализа с детализацией по воронке событий, это позволит точнее проанализировать поведение пользователей.

* Значительная масса пользователей (кластер 1 более 60 %) совершает незначительное количество действий, при этом показатель времени использования приложения в этой группе не самый низкий.Причина такого поведения требует дополнительного исследования. Возможно есть техническая проблема с зависанием.Рекомендация - проверить работу приложения.

В результате проверки гипотез 1 и 2 установлено:

* конверсия в просмотр контактов пользователей в приложении не зависит от браузера, через который они попали в приложение;

* конверсия в просмотр контактов пользователей в приложении зависит от количества времени проведённого в приложении.

## Часть 2.В результате настоящего исследования были проанализированы базы данных с информацией о книгах, издательствах, авторах, а также пользовательские обзоры книг и получены следующие результаты:

* результат запроса о количестве книг, вышедших после 1 января 2000 года - 819 единиц;

* выведена таблица о данных количества обзоров и средней оценки каждой книги ;

* Определено издательство, которое выпустило наибольшее число книг толще 50 страниц — Penguin Books выпустило 42 книги;

* Определён автора с самой высокой средней оценкой книг (учитены только книги с 50 и более оценками)- J.K. Rowling/Mary GrandPré, средний рейтинг её книг - 4.28;

* Посчитано среднее количество обзоров от пользователей, которые поставили больше 50 оценок - 24.33.

## Часть 3.В результате исследования данных в соответствии с Техническим заданием (далее ТЗ), установлено:

* данные не в полной мере соответствуют ТЗ в части даты остановки: 2021-01-04 по ТЗ - фактическая дата 30.12.2020;

* охват 15% пользователей европейской части - фактически 14,48%;

* время проведения теста совпало с проведением маркетинговой кампании Christmas&New Year Promo EU, N.America с 2020-12-25 по 2021-01-03;

* в данных final_ab_participants обнаружены не заявленные в ТЗ пользователи другого А/В теста interface_eu_test;

* пользователей, участвующих в двух группах теста не выявлено;

* выявлено 776 пользователей принявших учатие в двух тестах сразу;

* ожидаемое количество участников теста согласно ТЗ:6000, фактическое количество в группах до установления заданного лайфтайма-6351, после установленного лайфтайма осталось 3481, размеры групп А и В в отобранных для анализа данных различаются в 3 с лишним раза;

* показатели распределение количества событий на пользователя в группах А и В близки по значениям;

* динамика количество событий по дням в группах различна,но в обеих группах есть пик 21.12.2020, это может свидетельствовать о неравномерном распределении пользователей в группах;

* анализ воронки продаж показал, что конверсии в три события из 4 одинаковы, а конверсия в product_cart в группах теста различна.

В целом результаты А/В теста не обнаружили ожидаемого эффекта:" за 14 дней с момента регистрации пользователи покажут улучшение каждой метрики не менее, чем на 10%".

Результатам настояшего теста доверять конечно можно в той части, что значительного роста конверсии в контрольной группе не выявлено.Но что повлияло на пользователей контрольной и тестируемой групп и насколько равномерно они распределены, утверждать сложно. В дальнейшем при планировании проведения А/В тестов следует обратить внимание на следующие моменты:

* период проведения теста следует выбирать вне проведения маркетинговых кампаний и других тестов;

* формировать группы теста более равномерно как по времени так и по количеству;

* данные готовить в соответствии с ТЗ
