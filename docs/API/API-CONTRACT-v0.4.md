# CTOR API Contract v0.4  
Авторизация, токены, роли и права доступа (JWT‑подобная модель)

Версия: **v0.4**  
Статус: **расширенный сетевой контракт**  
Совместим с: **v0.1**, **v0.2**, **v0.3**

---

# 1. Назначение документа

Версия v0.4 добавляет в CTOR полноценную систему авторизации:

- JWT‑подобные токены  
- роли клиентов  
- права доступа (permissions)  
- проверку токенов на WebSocket и HTTP  
- безопасное подключение UI, ботов, команд и наблюдателей  
- основу для федерации CTOR и международных турниров  

Это делает CTOR безопасной, масштабируемой онлайн‑платформой.

---

# 2. JWT‑подобный токен CTOR

Токен CTOR — это JSON‑объект, закодированный в Base64 и подписанный секретом сервера.

Пример полезной нагрузки токена:

```json
{
  "player_id": "BOT_1",
  "role": "BOT",
  "permissions": ["SEND_MOVE"],
  "exp": 1712345678
}
```

### Поля токена:

| Поле | Тип | Описание |
|------|-----|----------|
| player_id | строка | Уникальный ID игрока/бота |
| role | строка | Роль клиента |
| permissions | массив | Разрешённые действия |
| exp | число | Время истечения токена (UNIX timestamp) |

---

# 3. Роли (Roles)

CTOR использует следующие роли:

| Роль | Описание |
|------|----------|
| UI | Клиент пользовательского интерфейса |
| BOT | ИИ‑бот |
| TEAM_CLIENT | Клиент командного режима |
| OBSERVER | Наблюдатель |
| ADMIN | Администратор сервера |

---

# 4. Права доступа (Permissions)

Каждый токен содержит список разрешённых действий.

| Permission | Описание |
|------------|----------|
| SEND_MOVE | Отправлять ходы |
| REQUEST_HINT | Запрашивать подсказки |
| SEND_TEAM_SIGNAL | Отправлять командные сигналы |
| CREATE_MATCH | Создавать матчи |
| TERMINATE_MATCH | Завершать матчи |
| VIEW_LOGS | Просматривать логи |
| OBSERVE | Наблюдать за матчем |

---

# 5. Получение токена (HTTP)

Клиент получает токен через HTTP‑запрос:

**POST** `/auth/token`

```json
{
  "player_id": "BOT_1",
  "secret": "bot_password"
}
```

**Ответ:**

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6..."
}
```

---

# 6. Использование токена в HTTP

Клиент передаёт токен в заголовке:

```
Authorization: Bearer <token>
```

Пример:

```
GET /matches/MATCH_001
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

---

# 7. Использование токена в WebSocket

Подключение:

```
wss://ctor-server/ws?token=eyJhbGciOiJIUzI1NiIs...
```

Сервер проверяет:

- подпись токена  
- срок действия  
- роль  
- права  

Если проверка не пройдена — соединение отклоняется.

---

# 8. Расширенный WebSocket‑протокол

## 8.1 Сообщение авторизации (Server → Client)

После подключения сервер отправляет:

```json
{
  "type": "auth_ok",
  "payload": {
    "player_id": "BOT_1",
    "role": "BOT",
    "permissions": ["SEND_MOVE"]
  }
}
```

Если токен неверный:

```json
{
  "type": "auth_error",
  "payload": {
    "code": "INVALID_TOKEN",
    "message": "Token is invalid or expired."
  }
}
```

---

# 9. Проверка прав доступа

Перед выполнением любого действия сервер проверяет:

- роль клиента  
- список permissions  

Пример:

Если клиент отправляет ход:

```json
{
  "type": "move",
  "payload": { }
}
```

Сервер проверяет:

```
permissions.includes("SEND_MOVE")
```

Если нет:

```json
{
  "type": "error",
  "payload": {
    "code": "PERMISSION_DENIED",
    "message": "Client is not allowed to send moves."
  }
}
```

---

# 10. Расширение HTTP API с авторизацией

## 10.1 Создание матча (только ADMIN)

**POST** `/matches`

Заголовок:

```
Authorization: Bearer <admin_token>
```

Если нет права `CREATE_MATCH`:

```json
{
  "error": "PERMISSION_DENIED"
}
```

---

# 11. Расширение WebSocket API с авторизацией

## 11.1 UI‑клиент

Разрешения:

- `SEND_MOVE`
- `REQUEST_HINT`
- `RESIGN`

## 11.2 Бот

Разрешения:

- `SEND_MOVE`
- `RESIGN`

## 11.3 Командный клиент

Разрешения:

- `SEND_TEAM_SIGNAL`

## 11.4 Наблюдатель

Разрешения:

- `OBSERVE`

## 11.5 Администратор

Разрешения:

- `CREATE_MATCH`
- `TERMINATE_MATCH`
- `VIEW_LOGS`

---

# 12. Пример полного токена

```json
{
  "player_id": "TEAM_ALPHA_CLIENT",
  "role": "TEAM_CLIENT",
  "permissions": ["SEND_TEAM_SIGNAL", "OBSERVE"],
  "exp": 1712345678
}
```

---

# 13. Пример отказа в доступе

Если бот пытается отправить командный сигнал:

```json
{
  "type": "team_signal",
  "payload": { "signal": "ATTACK_RIGHT" }
}
```

Сервер отвечает:

```json
{
  "type": "error",
  "payload": {
    "code": "PERMISSION_DENIED",
    "message": "Client does not have SEND_TEAM_SIGNAL permission."
  }
}
```

---

# 14. Применение API v0.4 в модулях CTOR

| Модуль | Авторизация | Токены | Роли | Права |
|--------|-------------|--------|------|--------|
| CTOR-UI | Да | Да | UI | SEND_MOVE, REQUEST_HINT |
| CTOR-Engine | Да | Да | ADMIN | Все |
| CTOR-AI-AI | Да | Да | BOT | SEND_MOVE |
| CTOR-H-AI | Да | Да | UI + BOT | Разные |
| CTOR-H-H | Да | Да | UI | SEND_MOVE |
| CTOR-TEAM-TEAM | Да | Да | TEAM_CLIENT | SEND_TEAM_SIGNAL |

---

# 15. Статус документа

Версия: **v0.4**  
Статус: **расширенный контракт (авторизация + токены)**  
Назначение:  
- безопасность  
- масштабируемость  
- онлайн‑турниры  
- удалённые боты  
- мобильные и веб‑клиенты  
- федерация CTOR  

Совместим с v0.1, v0.2, v0.3.

---
