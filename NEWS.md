# rym 1.0.5

* Исправлены ссылки в документации согласно требованиям CRAN.

# rym 1.0.4

* Исправил функцию `rym_get_data()`, ранее строка итогов убиралась, даже если пользователь не запрашивал никаких dimension, в таком случае вместо таблицы получали NULL.
* Функия `rym_get_my_logins()`, после процесса авторизации устанавливает опцию с именем пользователя.

# rym 1.0.1 - 1.0.2

* Сменилось приложение для авторизации
* Исправил ссылке в документации с http на https

# rym 1.0.0

Самый масштабный релизв истории пакета. Все обновления касаются API управления, и значительно расширяют возможности пакета `rym`.

С версии `1.0.0` пакет имеет возможность создавать в Яндекс Метрике цели и сегменты, а так же загружать данные об оффлайн конверсиях, телефонных звонках и расходах на рекламу из различных источников. 

* Создание объектов в ЯНдекс.Метрике
    * `rym_add_goal()` - Создать цель
    * `rym_add_segment()` - Создать сегмент, который будет использоваться в API
* Загрузка оффлайн конверсий
    * `rym_enable_offline_conversion()` - Включить учёт оффлайн конверсий
    * `rym_disable_off_offline_conversion()` - Выключить учёт оффлайн конверсий
    * `rym_allow_offline_conversion()` - Возвращает дату и время, начиная с которого конверсии могут быть привязаны к визитам для указанного счетчика.
    * `rym_get_uploadings_offline_conversions()` - Возвращает список загрузок оффлайн конверсий
    * `rym_upload_offline_conversion()` - Загрузка оффлайн конверсий в Яндекс.Метрику
* Загрузка звонков
    * `rym_enable_calls()` - Включить учёт звонков
    * `rym_disable_calls()` - Выключить учёт звонков
    * `rym_allow_calls()` - Возвращает дату и время, начиная с которого звонки могут быть привязаны к визитам для указанного счетчика.
    * `rym_get_uploadings_calls()` - Возвращает список загрузок информации о звонках
    * `rym_upload_calls()` - Загрузка информации о звонках конверсий в Яндекс.Метрику
* Загрузка расходов на рекламу
    * `rym_upload_expense()` - Загрузка расходов на рекламу в Яндекс.Метрику
    * `rym_delete_uploaded_expense()` - Удаление данных о расходах из Яндекс.Метрики
    * `rym_get_uploadings_expense()` - Список загрузок расходов

Исправлено авто обновление токена в функции `rym_auth()`.
---

# rym 0.6.0

В пакет добавлены опции и переменные среды.

* Опции помогают в рамках сессии легко переключаться между аккаунтами яндекс метрики:
    * rym.user - опция отвечающая за логин пользователя
	* rym.token_path - опция отвечает за путь к папке с учётными данными
	
* Переменные среды позволяют на глобальном уровне задать дефолтного пользователя Яндекс Метрики и путь к папаке с учётными данными
    * RYM_USER - Переменная для хранения дефолтного логина
	* RYM_TOKEN_PATH - Переменная для хранения пути к папке с учётными данными
	
Новая функция `rym_get_my_logins()` которая позволяет запросить список всех логинов под которыми вы прошли авторизайию, и переключится на нужный.	

---

# rym 0.5.6

Доработка `rym_get_data()`.

* Аргумент *include_undefined* переименован в *include.undefined*, согласно общим правилам синтаксиса пакета.
* Аргументы *counters*, *metrics* и *dimensions* теперь можно задавать через вектор, а не только строковым выражением.
* Теперь если оставить не заполненным аргумент *counters*, функция изначально зарпосит список всех доступных по заданному логину счётчиков, а потом по каждому запросит статистику.

---

# rym 0.5.5

Доработка `rym_get_counters()`.

В связи со сбоями вызванными отсутвием значений в некоторых полях, функция была доработана таким образом, что вместо не заполненных полей подставляет NA.

---

# rym 0.5.3, 0.5.4

Небольшие доработки функции `rym_get_counters()`.

* Ранее функция могла запрашивать данные только о 1000 счётчиков, теперь лимитов нет.
* Исправлена ошибка при загрузке счётчиков по которым не задано имя.
