# Базовый образ
FROM python:3.9-slim

# Рабочая директория
WORKDIR /app

# Системные пакеты: curl и vim
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl vim && \
    rm -rf /var/lib/apt/lists/*

# Копируем requirements
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Копируем приложение
COPY app.py .

# Создаём пользователя appuser с UID=1000
RUN groupadd -g 1000 appuser && \
    useradd -u 1000 -g appuser -m -s /usr/sbin/nologin appuser && \
    chown -R appuser:appuser /app

# Переключаемся на пользователя
USER appuser

# Порт и переменная окружения
EXPOSE 5000
ENV FLASK_ENV=production

# Команда запуска
CMD ["python", "app.py"]