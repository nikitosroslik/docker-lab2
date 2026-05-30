# Лабораторная работа №2 — Docker Compose: ASP.NET Core + PostgreSQL

## Контрольные вопросы

**1. Как в Compose передать строку подключения к БД?**
Через переменную окружения в секции environment:

environment:
  - ConnectionStrings__DefaultConnection=Host=db;Database=mydb;Username=postgres;Password=postgres

**2. Зачем нужен volume для PostgreSQL?**

Без volume данные хранятся внутри контейнера — при его пересоздании (docker-compose down) все данные теряются. Volume сохраняет данные на хосте независимо от жизненного цикла контейнера.


**3. Как выполнить команду внутри контейнера (docker exec)?**
docker exec -it <имя_контейнера> <команда>
Пример — зайти в bash контейнера с API:
docker exec -it dotnetcompose-api-1 bash
