<h2>Описание работы</h2>
Приложение работает с mysql БД example_schema, в которой содержится единственная таблица users1 (userId, name). 

Пользователю предлагается произвести поиск по userId. Для этого нужно ввести один из знаков **(>, <, =)** и само значение **userId**. 

Всего записей в таблице 5

Время хранения кэша в Redis установлено на 20 секунд. 

Если вывод произведен из кэша рэдиса, пользователю выводятся данные по запросу с комментарием: "FROM REDIS: "

Если в кэше запрашиваемых данных нет, то выводятся данные из таблицы бд с комментарием "FROM MYSQL: "

<h2>Для запуска</h2>
docker run -d —name redis -p 6379:6379 redis

docker run —name mysql -e MYSQL_ROOT_PASSWORD=1234 -d mysql

docker build . -f Dockerfile -t app

docker run -ti —name app -p 8080:8080 —link redis:redis —link mysql:mysql app
