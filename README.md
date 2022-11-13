# Инструменты для автоматического заполнения 3-НДФЛ на nalog.ru

Так как по дивидендам иностранных компаний налоговым агентом является физлицо, то приходится самостоятельно вносить информацию о них в декларацию 3-НДФЛ и самостоятельно платить налоги.

Для этого можно пытаться автоматически генерировать отчет в формате ПО "Декларация", либо вносить эту информацию в форму на nalog.ru, что умеет делать nalog.ipynb

## Автор

Alexander Gerasiov <a@gerasiov.net>

https://github.com/gerasiov/3ndfl

## Лицензия 
GPL версии 2 или более поздняя.

## Donate here

* BTC: bc1qjxet0e0u5gzufz40dvcl7nxu3jx7p0du7a5pgd
* ETH: 0xee37e2cb15af13e30409f33fd449138c9c649684
* Cards: https://www.tinkoff.ru/cf/4PWqTbN1xiv


## Инструменты

В этом репозитории содержится два инструмента: tinkoff.ipynb и nalog.ipynb.

Оба скрипта сделаны в виде jupyter notebook, во-первых, чтобы видеть код, который выполняется (всё-таки доступ к финансам и госуслугам), во-вторых, при необходимости такой вариант легче отладить.

Для простоты и надежности можно запускать ноутбуки в venv, чтобы не ставить зависимости в систему:
```
virtualenv 3ndfl-venv
. ./3ndfl-venv/bin/activate
pip install ipykernel
python -m ipykernel install --user --name=3ndfl-venv
jupyter notebook tinkoff.ipynb
```

После окончания работы можно удалить ipykernel и venv:
```
deactivate
jupyter kernelspec remove 3ndfl-venv
rm -rf 3ndfl-venv
```

## tinkoff.ipynb

Jupyter notebook с темплейтом кода, который подключается к Broker API Tinkoff и пытается забрать оттуда информацию о дивидендах.

Обратите внимание:

1. API Tinkoff довольно нестабильное, как минимум оно дублирует часть записей.
2. Для дохода от сделок РЕПО информация, которая возвращается из API, довольно неадекватная (кажется, по косвенным признакам можно понять детали, но я на это забил и пока вношу сделки РЕПО руками).
3. API может вернуть в том числе записи, не относящиеся к текущему году.

Поэтому проще всего сгенерировать файл, отсортировать его, проверить, что он соответствует отчету в PDF, который генерирует брокер и который у вас всё равно является первичным документом для отчета в ИФНС, и уже вручную проверенный файл скормить в nalog.ipynb

## nalog.ipynb

Jupyter notebook который умеет запускать Chrome/Chromium через selenium и заполнять в нем форму 3-НДФЛ на сайте nalog.ru

Обратите внимание, что для того, чтобы введенные данные сохранились, надо убедиться, что все доходы оформлены правильно. Но, если вы только начали заполнять декларацию, кнопка "Далее" откажется нажиматься из-за того, что надо выбрать вариант налогового вычета для доходов, эспортированных из 2-НДФЛ. Это можно сделать вручную в окне браузера и вручную же нажать кпопку "далее".
