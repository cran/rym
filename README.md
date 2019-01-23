
<!-- README.md is generated from README.Rmd. Please edit that file -->
rym
===

CRAN
====

[![Rdoc](http://www.rdocumentation.org/badges/version/rym)](http://www.rdocumentation.org/packages/rym)

Официальная документация к пакету rym
=====================================

Официальную русскоязычную документацию можно найти по этой [ссылке](https://selesnow.github.io/rym/)

Краткое описание
================

`rym` является R интерфейсом для работы с API Яндекс Метрики, его функции позволяют вам взаимодействовать со следующими API:

1.  [API Управления](https://tech.yandex.ru/metrika/doc/api2/management/intro-docpage/) - позволяет получить таблицы с такими объектами как достуные счётчики Яндекс.Метрики, список настроенных целей, фильтров и сегментов, а так же список пользователей у которых есть доступ к счётчику.
2.  [API Отчётов](https://tech.yandex.ru/metrika/doc/api2/api_v1/intro-docpage/) - позволяет получать информацию о статистике посещений сайта и другие данные, не используя интерфейс Яндекс.Метрики.
3.  [API совместимый с Core API Google Analytics (v3)](https://tech.yandex.ru/metrika/doc/api2/ga/intro-docpage/) - позволяет запрашивать статистические данные используя при этом название полей такие же как и при работе с Core Reporting API v3.
4.  [Logs API](https://tech.yandex.ru/metrika/doc/api2/logs/intro-docpage/) - позволяет получить сырые, несгруппированные данные о посещении вашего сайта из Яндекс.Метрики.

Установка
---------

Установить `rym` можно как с CRAN так и с GitHub

CRAN: `install.packages('rym')`

GitHub: `devtools::install_github("selesnow/rym")`

Виньетки
========

Помимо официальной документации у пакета есть 5 виньеток, вводная, и отдельно виньетка под каждый API, открыть их можно с помощью следующих команд:

-   Введение в пакет `rym`: `vignette('intro-to-rym', package = 'rym')`
-   API Управления: `vignette('rym-management-api', package = 'rym')`
-   API Отчётов: `vignette('rym-reporting-api', package = 'rym')`
-   API совместимый с Core API Google Analytics v3: `vignette('rym-ga-api', package = 'rym')`
-   Logs API: `vignette('rym-logs-api', package = 'rym')`

Пример кода
-----------

``` r
# auth
rym_auth(login = "vipman.netpeak", token.path = "metrica_token")
rym_auth(login = "selesnow", token.path = "metrica_token")


# ManagementAPI
# get counters list
selesnow.counters <- rym_get_counters(login      = "selesnow",
                                      token.path = "metrica_token")

vipman.counters   <- rym_get_counters(login      = "vipman.netpeak",
                                      token.path = "metrica_token")

# get goals list
my_goals <- rym_get_goals(counter = 10595804,
                          login      = "vipman.netpeak",
                          token.path = "metrica_token")

# пget filter list
my_filter <- rym_get_filters(counter = 10595804,
                             login      = "vipman.netpeak",
                             token.path = "metrica_token")

# get segment list
my_segments <- rym_get_segments(counter = 10595804,
                                login      = "vipman.netpeak",
                                token.path = "metrica_token")

# get counter list
users <- rym_users_grants(counter = 10595804,
                          login      = "vipman.netpeak",
                          token.path = "metrica_token")

# Reporting API
reporting.api.stat <- rym_get_data(counters   = "23660530,10595804",
                                   date.from  = "2018-08-01",
                                   date.to    = "yesterday",
                                   dimensions = "ym:s:date,ym:s:lastTrafficSource",
                                   metrics    = "ym:s:visits,ym:s:pageviews,ym:s:users",
                                   sort       = "-ym:s:date",
                                   login      = "vipman.netpeak",
                                   token.path = "metrica_token",
                                   lang = "en")

# Logs API
logs.api.stat      <- rym_get_logs(counter    = 23660530,
                                   date.from  = "2018-08-01",
                                   date.to    = "2018-08-05",
                                   fields     = "ym:s:date,
                                                 ym:s:lastTrafficSource,
                                                 ym:s:referer",
                                   source     = "visits",
                                   login      = "vipman.netpeak",
                                   token.path = "metrica_token")

# API compatible with Core API Google Analytics v3
ga.api.stat        <- rym_get_ga(counter    = "ga:22584910",
                                 dimensions = "ga:date,ga:source",
                                 metrics    = "ga:sessions,ga:users",
                                 start.date = "2018-08-01",
                                 end.date   = "2018-08-05",
                                 sort       = "-ga:date",
                                 login      = "selesnow",
                                 token.path = "metrica_token")
```

Автор: Алексей Селезнёв (Head of Analytics Dept. at Netpeak)
