# Простой Selenium Bot
Этот бот нужен для перехода по страницам целевого сайта
с заданным временем сессии и количеством кликов по тегу <a>

Этот бот умеет:
менять юзерагент,
менять прокси,
менять разрешение браузера в соответствии с типом устройства,
может запускаться с отображением браузера и без него,
может переходить по одной из target-ссылок (точки входа на сайт),
может искать заданный узел на поисковых машинах google и yandex по ключевым словам,
может искать как по target-ссылке так и  по ключевым названиям в ввыводе поисковика,
может кликать заданное количество раз по ссылкам на сайте (в случайном диапазоне от и до),
тратит случайное время на сессию (в диапазоне от и до)
использует для смены юзерагента и разрешения браузера список предустановленных конфигураций


## Установка

Для установки потребуется установить conda, python, geckodriver

conda - виртуальное окружение
python -  для непосредственного запуска
geckodriver - для библиотеки selenium (для использования движка браузера)

1. после установки conda нужно задать новое виртуальное окружение  
(Cоnda  устанавливается прсото - переходим на официальный сайт и качаем miniconda на компьютер)

```
conda create -n new_environment_name
```
где new_environment_name - имя окружения
2. переходим в новое окружение
```
для Windows: activate new_environment_name 
или для Linux: source activate new_environment_name 
```

3. устанавливаем python

```
conda install python 
``` 
после чего установится python3

можно проверить, запустив python в консоли (должен открыться интерфейс интепретатора с указанием версии, не ниже 3)

4. Устанавливаем geckodriver 

прсото скачиваем этот драйвер из интернета по инструкции из интернета =)
нам важно чтобы папка расположения драйвера была указана в системном пути для пользователя, под которым мы будем запускать бота

```
для Linux:
export PATH=$PATH:/home/alexander/geckodriver/
```
где /home/alexander/geckodriver/ - ваша папка с дравером
в виндовс нужно добавить путь в переменную path 

5. Клонируем образ бота на компьютер
```
git clone https://github.com/Alexander35/selenium_bot.git 
```
6. переходим в папку с ботом

## Настройка

1. в папке conf копируем .conf.json  в conf.json
2. открываем conf.json
3. устанавливааем нужные настройки
```
{
	"headless": "yes", // yes - запуск в режиме без показа браузера. любое другое значение запускает с показам браузера
	"project_name" : "project_name", // этот аргумент пока не используется
	"target_url" : [ // здесь в квадратных скобках через запятую указываем точки входа на сайт
			"http://smmm.com"
		],
	"search_keywords" : [ //здесь указываем ключевые слова, по которым будет осуществляться поиск через поисковые машины
		"smmmer",
		"smm"
	],
	"searched_link_titles" : [ // Здесь указываем конкретные заголовки в выдаче поисковых машин по указанным выше ключевым словам (заголовки, на которые можно кликнуть для перехода на сайт)
		"служба новостей",
		"новсти с характером"
	],
	"search_engines": [ // здесь пока ничего нельзя менять =(
		"https://www.google.com/search?q=",
		"https://yandex.ru/search/?text="
	],		
	"referer_url" : "https://youtube.com", // этот аргумент пока не используется
	"client_hosts": 6000, // этот аргумент пока не используется
	"clicks_per_user": {"from": 2, "to": 2000}, // диапазон кликов за одну сессию
	"time_on_session": {"from" : 100, "to" : 200}, // диапазон времени на одну сессию в секундах
	"device_type" : [ // типы устройств для случайного выбора
			"phone",
			"pc",
			"tablet"
		],
	"proxy_type": "no", // yes - использваить прокси, другое значение - не использовать
	"serch_in_the_web" : "no", // yes -искать через поисковые машины перед переходом на сайт, другое значение - не искать
	"start_time": "now" // этот аргумент пока не используется
}
```

4. В других файлах: proxy_list.json, screen_resolutions.json, user_agents.json находятся параметры прокси, разрешения браузера, юзерагенты . В эти файлы легко можно добавить другие варианты , которые потом выберет бот для работы.

## Запуск

для запуска в Linux можно использовать скрипт .selenium_bot_start.sh предварительно скопировав его в файл без точки в начале, дав разрешение на запуск и исправив внутри конфиграцию путей

1.Необходимо перейти в виртуальное окружение conda
2.запустить скрипт 
```
python selenium_bot.py

``` 
3. посмотреть логи в папке log
должен создаться файл geckodriver.log
и папка с таймстампом и урл-target для каждого запуска бота, в каждой из которых есть два файла: system_log.log и user_log.log

эти файлы почти не отличаются, за исключением того, что в system_log информации больше. 

необходимо убедиться что в логах нет явных ошибок 

Спасибо! 