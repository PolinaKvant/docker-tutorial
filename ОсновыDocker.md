# Основы Docker

## Введение

**Docker** — это платформа для разработки, доставки и запуска приложений в контейнерах. Контейнеры позволяют упаковать приложение со всеми его зависимостями в единый образ, который можно запускать на любой системе, поддерживающей Docker. Это обеспечивает **переносимость**, **изоляцию** и **эффективность** приложений.

## Основные концепции Docker

### 1. Образ (Image)
**Образ Docker** — это шаблон, содержащий все необходимые файлы, зависимости и настройки для запуска приложения. Образы создаются на основе **Dockerfile**, который описывает, как собрать образ.

Пример Dockerfile:
```dockerfile
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y python3
COPY . /app
WORKDIR /app
CMD ["python3", "app.py"]
```

### 2. Контейнер (Container)
**Контейнер** — это запущенный экземпляр образа. Контейнеры изолированы друг от друга и от хостовой системы, но могут взаимодействовать через сеть или общие тома.

Пример запуска контейнера:
```bash
docker run -it ubuntu:20.04
```

### 3. Реестр (Registry)
**Реестр Docker** — это хранилище образов. Наиболее популярный реестр — [Docker Hub](https://hub.docker.com). Вы можете загружать (push) и скачивать (pull) образы из реестра.

Пример загрузки образа:
```bash
docker pull nginx
```

### 4. Docker Compose
**Docker Compose** — это инструмент для управления многоконтейнерными приложениями. Он позволяет описывать контейнеры, сети и тома в файле `docker-compose.yml`.

Пример `docker-compose.yml`:
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
```

## Установка Docker

### Для Linux
1. Обновите пакеты:
   ```bash
   sudo apt-get update
   ```
2. Установите Docker:
   ```bash
   sudo apt-get install docker.io
   ```
3. Запустите Docker:
   ```bash
   sudo systemctl start docker
   ```

### Для Windows и macOS
Скачайте и установите [Docker Desktop](https://www.docker.com/products/docker-desktop).

## Основные команды Docker

### Работа с образами
- **Сборка образа**:
  ```bash
  docker build -t my-image .
  ```
- **Просмотр образов**:
  ```bash
  docker images
  ```
- **Удаление образа**:
  ```bash
  docker rmi my-image
  ```

### Работа с контейнерами
- **Запуск контейнера**:
  ```bash
  docker run -d --name my-container my-image
  ```
- **Просмотр запущенных контейнеров**:
  ```bash
  docker ps
  ```
- **Остановка контейнера**:
  ```bash
  docker stop my-container
  ```
- **Удаление контейнера**:
  ```bash
  docker rm my-container
  ```

### Работа с томами
- **Создание тома**:
  ```bash
  docker volume create my-volume
  ```
- **Просмотр томов**:
  ```bash
  docker volume ls
  ```
- **Удаление тома**:
  ```bash
  docker volume rm my-volume
  ```

## Пример использования Docker

### Запуск веб-сервера Nginx
1. Скачайте образ Nginx:
   ```bash
   docker pull nginx
   ```
2. Запустите контейнер:
   ```bash
   docker run -d -p 80:80 --name my-nginx nginx
   ```
3. Откройте браузер и перейдите по адресу `http://localhost`.

## Преимущества Docker

- **Изоляция**: Каждое приложение работает в своем контейнере, что исключает конфликты зависимостей.
- **Переносимость**: Образы Docker можно запускать на любой системе, поддерживающей Docker.
- **Масштабируемость**: Контейнеры легко масштабируются с помощью инструментов, таких как Kubernetes.

## Заключение

Docker — это мощный инструмент для разработки и развертывания приложений. Он упрощает процесс создания, тестирования и доставки программного обеспечения, обеспечивая высокую степень изоляции и переносимости.

![Docker Logo](data:image/png;base64,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)

Для более подробного изучения Docker, посетите [официальную документацию](https://docs.docker.com/).
```