# Задача: простой REST API

Требуется разработать простой REST API для взаимодествия с БД, которая хранит
информацию об автомобилях.

## Требования

- Сервис должен подключаться к базе данных PostgreSQL, которая хранит информацию
об автомобилях. О каждом автомобиле в БД хранится следующая информация:
  - Уникальный идентификатор - номер автомобиля;
  - Модель автомобиля;
  - Владелец автомобиля (серия-номер паспорта);
  - Пробег автомобиля в километрах;
- Сервис должен предоставлять REST API для взаимодействия с базой данных (CRUD):
  - GET `/car/{id}` - получить информацию об автомобиле по идентификатору;
  - GET `/car?page=&per_page=` - получить информацию о всех автомобилях, с
    учетом пагинации из query-параметров запроса, т.е. чтобы отправлять
    информацию не о всех автомобилях (т.к. их может быть очень много), нужно
    отправлять информацию об автомобилях из некоторого последовательного куска
    из списка автомобилей в БД;
  - POST `/car` - сохранить в БД информацию об автомобиле. Если автомобиль уже
    есть в БД, то заменить. Информация об автомобиле в теле запроса;
  - UPDATE `/car` - обновить информацию об автомобиле. В теле запроса передается
    сущность автомобиля, с единственным обязательным полем - идентификатором.
    Все остальные поля опциональные и если не присутствуют, то не обновляются в
    БД. Если автомобиля для обновления в базе нет, вернуть 404 NOT FOUND;
  - DELETE `/car/{id}` - удалить автомобиль по идентификатору. Если автомобиля
    нет, то вернуть 404 NOT FOUND;
  - Запросы валидируются средствами `pydantic`;
  - API должен сопровождаться OpenAPI документацией, с описаниями для каждого
    запроса;
- Сервис должен быть написан с использованием технологий:
  - `fastapi`;
  - `pydantic` (shipped with FastAPI);
  - `sqlalchemy`;
- Код должен быть качественно отформатирован и должен следовать требованями
`flake8`, `isort`. В качестве форматтера должен быть использован `black`;
- Сервис должно быть возможно запустить посредством вызова команды
  `docker-compose up` из корня репозитория;

## Дополнительные требования

Эти требования не входят в базовую конфигурацию задания, но особо ценятся 
дополнительно.

- Настроить логгирование всех запросов приходящих в систему в stdout/stderr, а так 
  же в файл. Для логов в файл нужно настроить retention и rotation;
- Настроить сборку логов в Graylog/Prometheus + Graphana;
- Обернуть сервис в прокси nginx, при это допускаются запросы проходящие только 
  через nginx;
- Добавить проверку на формат номера автомобиля, покрыть эту проверку тестами и
  автоматизировать тестирование посредством CI/CD (GitHub Actions);

## Полезные ссылки

- [Документация FastAPI](https://fastapi.tiangolo.com/)
- [Документация Pydantic](https://pydantic-docs.helpmanual.io/)
- [Документация Loguru](https://loguru.readthedocs.io/en/stable/index.html)
- [Docker-образ PostgreSQL](https://hub.docker.com/_/postgres)
- [Graylog в Docker](https://docs.graylog.org/docs/docker)
- [Setup Grafana with Prometheus for Python projects using Docker](https://thepylot.dev/setup-grafana-with-prometheus-for-python-projects-docker-included/)
