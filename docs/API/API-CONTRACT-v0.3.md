# CTOR API Contract v0.3  
Сетевой API‑контракт (HTTP + WebSocket) для UI, Engine, ботов и игровых платформ CTOR

Версия: **v0.3**  
Статус: **сетевой контракт**  
Совместим с: **v0.1**, **v0.2**

---

# 1. Назначение документа

Версия v0.3 расширяет API CTOR до сетевого уровня, добавляя:

- HTTP‑эндпоинты для управления матчами  
- WebSocket‑протокол для реального времени  
- сетевую модель для UI, ботов и команд  
- поддержку удалённых клиентов (браузер, мобильные, облачные боты)  

Цель: превратить CTOR в онлайн‑платформу, где:

- Engine работает как сервер  
- UI и боты подключаются как клиенты  
- матчи идут по сети  
- турниры проводятся удалённо  

---

# 2. Общая архитектура сети

Используются два протокола:

- **HTTP** — управление матчами, получение статуса, логов  
- **WebSocket** — реальное время: ходы, события, состояние игры  

Рекомендуемая схема:

- CTOR‑Server (на базе CTOR‑Engine) поднимает HTTP + WebSocket  
- UI, боты, командные клиенты подключаются по WebSocket  
- административные панели используют HTTP  

---

# 3. HTTP API

Базовый URL (пример):

```
https://ctor-server.example.com/api/v1
```

## 3.1 Создание матча

**POST** `/matches`

```json
{
  "mode": "AI-AI",
  "players": [
    { "id": "BOT_1", "type": "AI" },
    { "id": "BOT_2", "type": "AI" }
  ],
  "move_time_limit_ms": 2000
}
```

**Ответ:**

```json
{
  "match_id": "MATCH_001",
  "status": "CREATED"
}
```

---

## 3.2 Получение статуса матча

**GET** `/matches/{match_id}`

```json
{
  "match_id": "MATCH_001",
  "status": "RUNNING",
  "mode": "AI-AI",
  "current_player": "BOT_1",
  "turn": 5
}
```

---

## 3.3 Получение логов матча

**GET** `/matches/{match_id}/log`

```json
{
  "match_id": "MATCH_001",
  "moves": [
    { "turn": 1, "player_id": "BOT_1", "move": {} },
    { "turn": 2, "player_id": "BOT_2", "move": {} }
  ]
}
```

---

## 3.4 Завершение матча (административно)

**POST** `/matches/{match_id}/terminate`

```json
{
  "reason": "ADMIN_TERMINATED"
}
```

**Ответ:**

```json
{
  "match_id": "MATCH_001",
  "status": "TERMINATED"
}
```

---

# 4. WebSocket API

Базовый URL:

```
wss://ctor-server.example.com/ws
```

Подключение клиента:

```
wss://ctor-server.example.com/ws?match_id=MATCH_001&player_id=PLAYER_1&role=UI
```

Параметры:

- `match_id` — ID матча  
- `player_id` — ID игрока/бота/клиента  
- `role` — `UI`, `BOT`, `TEAM_CLIENT`, `OBSERVER`  

---

# 5. Формат WebSocket‑сообщений

Все сообщения имеют формат:

```json
{
  "type": "string",
  "payload": {}
}
```

---

# 6. Сообщения сервера (Server → Client)

## 6.1 Состояние игры

```json
{
  "type": "state",
  "payload": { }
}
```

---

## 6.2 Событие

```json
{
  "type": "event",
  "payload": {
    "event": "MATCH_STARTED"
  }
}
```

---

## 6.3 Ошибка

```json
{
  "type": "error",
  "payload": {
    "code": "ILLEGAL_MOVE",
    "message": "Move is not allowed in current state."
  }
}
```

---

## 6.4 Тайм-аут

```json
{
  "type": "timeout",
  "payload": {
    "player_id": "PLAYER_2"
  }
}
```

---

## 6.5 Подсказка

```json
{
  "type": "hint",
  "payload": { }
}
```

---

# 7. Сообщения клиента (Client → Server)

## 7.1 Ход

```json
{
  "type": "move",
  "payload": { }
}
```

---

## 7.2 Сдача

```json
{
  "type": "resign",
  "payload": {
    "player_id": "PLAYER_1"
  }
}
```

---

## 7.3 Запрос подсказки

```json
{
  "type": "request_hint",
  "payload": {
    "player_id": "PLAYER_1"
  }
}
```

---

## 7.4 Командный сигнал (TEAM-TEAM)

```json
{
  "type": "team_signal",
  "payload": {
    "team_id": "TEAM_ALPHA",
    "signal": "ATTACK_RIGHT"
  }
}
```

---

# 8. Роли клиентов

## 8.1 UI‑клиент (`role=UI`)

Получает:

- `state`
- `event`
- `error`
- `hint`
- `timeout`

Отправляет:

- `move`
- `request_hint`
- `resign`

---

## 8.2 Бот (`role=BOT`)

Получает:

- `state`
- `error`
- `timeout`

Отправляет:

- `move`
- `resign`
- `team_signal` (опционально)

---

## 8.3 Командный клиент (`role=TEAM_CLIENT`)

Получает:

- `state`
- `event`
- `team_signal`

Отправляет:

- `team_signal`

---

## 8.4 Наблюдатель (`role=OBSERVER`)

Получает:

- `state`
- `event`

Не отправляет сообщений.

---

# 9. Авторизация и идентификация

v0.3 использует упрощённую авторизацию:

- `player_id` и `role` передаются в query‑параметрах WebSocket  
- в будущем может быть добавлен `auth_token`  

Пример:

```
wss://ctor-server.example.com/ws?match_id=MATCH_001&player_id=BOT_1&role=BOT
```

---

# 10. Применение v0.3 в модулях CTOR

| Модуль | HTTP | WebSocket | Роль |
|--------|------|-----------|------|
| CTOR-UI | Да | Да | Клиент |
| CTOR-Engine (Server) | Да | Да | Сервер |
| CTOR-AI-AI | Частично | Да | Боты |
| CTOR-H-AI | Да | Да | UI + Bot |
| CTOR-H-H | Да | Да | Два UI |
| CTOR-TEAM-TEAM | Да | Да | Командные клиенты |

---

# 11. Статус документа

Версия: **v0.3**  
Статус: **сетевой контракт (черновой, прототипный)**  
Назначение:  
- подготовка CTOR к онлайн‑режиму  
- поддержка удалённых UI и ботов  
- основа для турниров и федерации CTOR  

Совместим с v0.1 и v0.2.

---
