

```markdown
# Лабораторная работа 4

## Цель
Запуск Docker-контейнеров с установленными утилитами `aafire` и `ping`, настройка сети между контейнерами и проверка сетевого соединения.

## Шаги выполнения

### 1. Установка Docker
Убедись, что Docker установлен на твоей машине. Инструкции по установке можно найти на официальном сайте Docker для твоей операционной системы.

### 2. Создание Dockerfile
Создай файл `Dockerfile` в пустом каталоге. В файле определи образ, установи необходимые утилиты:
```Dockerfile
FROM ubuntu:latest

RUN apt-get update && apt-get install -y libaa-bin iputils-ping
```

### 3. Сборка образа
Выполни команду для сборки Docker-образа:
```bash
docker build -t myfire .
```

### 4. Запуск контейнеров
Запусти два контейнера в фоновом режиме:
```bash
docker run -d --name fire1 myfire aafire
docker run -d --name fire2 myfire aafire
```

### 5. Создание сети Docker
Создай сеть для контейнеров:
```bash
docker network create myNetwork
```

Подключи контейнеры к этой сети:
```bash
docker network connect myNetwork fire1
docker network connect myNetwork fire2
```

### 6. Проверка подключения
1. Введи команду для получения информации о сети:
   ```bash
   docker network inspect myNetwork
   ```

2. Подключись к одному из контейнеров:
   ```bash
   docker exec -it fire1 bash
   ```

3. Используй команду `ping` для проверки связи с другим контейнером (подставь IP-адрес):
   ```bash
   ping <IP-адрес второго контейнера>
   ```

## Скриншоты
1. Логи работы контейнеров:
   - `fire1` и `fire2` выполняют команду `aafire`.
2. Результат команды `ping` между контейнерами.

![ping](https://github.com/user-attachments/assets/d08e2b5e-c904-491c-ab72-65167f4a179d)
![fire2](https://github.com/user-attachments/assets/3d193b77-b530-4ff8-a99a-c88878fdfe5c)
![fire1](https://github.com/user-attachments/assets/8d31d954-26d4-4642-ae89-632d34d950e6)


## Завершение
После выполнения всех шагов, останови и удали контейнеры:
```bash
docker stop fire1 fire2
docker rm fire1 fire2
docker network rm myNetwork
```

