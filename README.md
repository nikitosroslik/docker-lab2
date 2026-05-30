# Лабораторная работа №2 — Docker Compose: ASP.NET Core + PostgreSQL

## Структура репозитория

```
MyApi/                  — ASP.NET Core Web API
  Models/Product.cs     — модель продукта
  Data/AppDbContext.cs  — контекст Entity Framework
  Program.cs            — эндпоинты и конфигурация
  Dockerfile
docker-compose.yml      — api + db (PostgreSQL) + pgadmin
```

## Запуск

```bash
docker-compose up -d --build
```

Swagger UI: http://localhost:5000/swagger  
pgAdmin: http://localhost:8888 (admin@admin.com / admin)

---

## Контрольные вопросы

**1. Как в Compose передать строку подключения к БД?**

Через переменную окружения в секции `environment`:

```yaml
environment:
  - ConnectionStrings__DefaultConnection=Host=db;Database=mydb;Username=postgres;Password=postgres
```

В `Program.cs` она читается через `builder.Configuration.GetConnectionString("DefaultConnection")`.
Двойное подчёркивание `__` — это разделитель вложенных секций в ASP.NET Core конфигурации.

---

**2. Зачем нужен volume для PostgreSQL?**

Без volume данные хранятся внутри контейнера — при его пересоздании (`docker-compose down`) все данные теряются. Volume сохраняет данные на хосте независимо от жизненного цикла контейнера.

---

**3. Как выполнить команду внутри контейнера (`docker exec`)?**

```bash
docker exec -it <имя_контейнера> <команда>
```

Пример — зайти в bash контейнера с API:

```bash
docker exec -it dotnetcompose-api-1 bash
```

Пример — запустить миграции EF:

```bash
docker exec -it dotnetcompose-api-1 dotnet ef database update
```
