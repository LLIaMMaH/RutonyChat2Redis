# Rutony Chat to Python (Minecraft Stream Events Handler)

Скрипт - Костыль. Этот проект предназначен для записи информации о различных событиях с различных стриминговых платформ (Twitch, Trovo, GoodGame, VKPlay и др.) и их передачи в хранения событий в **Redis** и **PostgreSQL**, а также для отправки сообщения о событии в **Minecraft** через **RCON**.  

[Почему так?](./WhyIsThat.md)  


## **📌 Функциональность**
- Получает параметры события из командной строки.
- В зависимости от типа события отправляет команду в **Minecraft** (RCON).
- Логирует все действия в файл (`loguru`).
- Сохраняет события в **Redis** (очередь для последующей обработки).
- Поддерживает конфигурацию через **.env**.

### **Поддерживаемые параметры**
| Параметр | Тип   | Обязателен | Описание |
| --- |-------| --- | --- |
| `event` | str | ✅ | Тип события: `donate`, `raid`, `new_viewer`, `tellraw` |
| `site` | str | ✅ | Платформа: `Twitch`, `Trovo`, `VKPlay`, `GoodGame` |
| `player_name` | str | ✅ | Ник игрока в Minecraft |
| `text` | str | ❌ | Текст сообщения |
| `donate` | float | ❌ | Сумма доната |
| `currency` | str | ❌ | Валюта доната |
| `qty` | int | ❌ | Количество зрителей при рейде |
| `command` | str | ❌ | Minecraft-команда для выполнения |

---

## **📦 Установка**

### **1. Установите Python 3.8+**  
Скачайте и установите Python, если он не установлен:  
[https://www.python.org/downloads/](https://www.python.org/downloads/)

### **2. Установите зависимости**  
Склонируйте репозиторий и установите зависимости:  
```sh
git clone https://github.com/LLIaMMaH/RutonyChat2Redis.git
cd RutonyChat2Redis
pip install -r requirements.txt
```

### **3. PostgreSQL**
Создать базу данных. Создать таблицу.
```sql
CREATE TABLE events (
    id SERIAL PRIMARY KEY,
    event_type TEXT NOT NULL,
    site TEXT NOT NULL,
    player_name TEXT NOT NULL,
    text TEXT,
    donate NUMERIC,
    currency TEXT,
    qty INT,
    redis BOOLEAN NOT NULL,
    timestamp TIMESTAMP DEFAULT NOW()
);
```

**PS:** Поскольку скрипт просто вызывается, то необходимо установить нужные зависимости в глобальное хранилище.