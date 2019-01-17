
<!-- README.md is generated from README.Rmd. Please edit that file -->
rym
===

CRAN
====

[![Rdoc](http://www.rdocumentation.org/badges/version/rym)](http://www.rdocumentation.org/packages/rym)

Information for russian language users
======================================

Russian manuals ypu can find [here](https://selesnow.github.io/rym/)

rym package
===========

rym is an R interface to Yamdex.Metrica API.

rym work with next API:

1.  [Management API](https://tech.yandex.ru/metrika/doc/api2/management/intro-docpage/) - allows you to get tables with such objects as Yandex.Metrics sufficient counters, a list of configured goals, filters and segments, as well as a list of users who have access to the counter.
2.  [API ќтчЄтов](https://tech.yandex.ru/metrika/doc/api2/api_v1/intro-docpage/) - allows you to receive information on the statistics of site visits and other data without using the Yandex.Metrica interface.
3.  [API совместимый с Core API Google Analytics (v3)](https://tech.yandex.ru/metrika/doc/api2/ga/intro-docpage/) - allows you to query statistics using the names of the fields are the same as when working with Core Reporting API v3.
4.  [Logs API](https://tech.yandex.ru/metrika/doc/api2/logs/intro-docpage/) - allows you to get raw, ungrouped data about your visit to your site from Yandex.Metrica.

Installation
------------

CRAN: `install.packages('rym')` GitHub: `devtools::install_github("selesnow/rym")`

rym vignettes
=============

You can read vignette @Intro to rym by run next code: `vignette('intro-to-rym', package = 'rym')`

Code example
------------

``` r
# auth
rym_auth(login = "vipman.netpeak", token.path = "metrica_token")
rym_auth(login = "selesnow", token.path = "metrica_token")


# ManagementAPI
# получить список сч™тчиков
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
