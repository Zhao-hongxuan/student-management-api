# Student Management API

**Фамилия:** Чжао  
**Имя:** ХунСюань  
**Класс:** 5132704/30701

## Быстрый старт

### 1. Клонирование проекта

```bash
git clone https://github.com/Zhao-hongxuan/student-management-api.git
cd student-management-api
```

### 2. Настройка переменных окружения

```bash
# Copy the example environment variables file
cp .env.example .env

# Edit the .env file and set your database password
# Modify the password in POSTGRES_PASSWORD and DATABASE_URL
```

### 3. Запуск базы данных

```bash
# Start the PostgreSQL database container
docker-compose up -d
```

### 4. Установка зависимостей

```bash
# Create and activate a virtual environment (Windows)
python -m venv venv
venv\Scripts\activate

# Install Python dependencies
pip install -r requirements.txt
```

### 5. Запуск приложения

```bash
cd app
python main.py
```

### 6. Доступ к документации API

После запуска приложения откройте следующие адреса для просмотра документации API:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

## Конечные точки API

### Управление студентами

| Метод | Конечная точка | Описание |
|-------|----------------|----------|
| POST | `/api/v1/students/` | Создать студента |
| GET | `/api/v1/students/` | Получить список всех студентов |
| GET | `/api/v1/students/{student_id}` | Получить детальную информацию о студенте |
| DELETE | `/api/v1/students/{student_id}` | Удалить студента |

### Управление группами

| Метод | Конечная точка | Описание |
|-------|----------------|----------|
| POST | `/api/v1/groups/` | Создать группу |
| GET | `/api/v1/groups/` | Получить список всех групп |
| GET | `/api/v1/groups/{group_id}` | Получить детальную информацию о группе |
| DELETE | `/api/v1/groups/{group_id}` | Удалить группу |

### Управление связями студент-группа

| Метод | Конечная точка | Описание |
|-------|----------------|----------|
| POST | `/api/v1/students/{student_id}/groups/{group_id}` | Добавить студента в группу |
| DELETE | `/api/v1/students/{student_id}/groups/{group_id}` | Удалить студента из группы |
| GET | `/api/v1/groups/{group_id}/students/` | Получить всех студентов в группе |
| POST | `/api/v1/students/{student_id}/transfer/` | Перевести студента из одной группы в другую |

## Развертывание с помощью Docker

### Полное развертывание через Docker

Чтобы развернуть всё приложение (включая базу данных и приложение) с использованием Docker:

1. Создайте Dockerfile (если требуется) и docker-compose.prod.yml
2. Выполните: `docker-compose -f docker-compose.prod.yml up -d`

### Развертывание только базы данных

По умолчанию проект использует Docker для развертывания базы данных, а приложение запускается локально:

```bash
docker-compose up -d # Запустить базу данных
cd app && python main.py # Локальный запуск приложения
```

### Инициализация базы данных

При первом запуске приложение автоматически создаст все необходимые таблицы в базе данных. Если требуется сбросить базу данных:

```bash
# Удалить и заново создать контейнер базы данных
docker-compose down -v
docker-compose up -d
```

## Примеры использования API

### Создание студента

```bash
curl -X POST "http://localhost:8000/api/v1/students/" \
  -H "Content-Type: application/json" \
  -d '{
    "first_name": "Сань Чжан",
    "last_name": "Чжан",
    "email": "zhangsan@example.com"
  }'
```

### Создание группы

```bash
curl -X POST "http://localhost:8000/api/v1/groups/" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Компьютерные науки",
    "description": "Группа по специальности «Компьютерные науки»"
  }'
```

### Добавление студента в группу

```bash
curl -X POST "http://localhost:8000/api/v1/students/1/groups/1"
