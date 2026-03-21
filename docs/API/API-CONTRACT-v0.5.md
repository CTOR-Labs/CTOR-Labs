# CTOR API Contract v0.5  
Matchmaking, комнаты, лобби и управление сессиями

Версия: **v0.5**  
Статус: **расширенный игровой контракт**  
Совместим с: **v0.1–v0.4**

---

# 1. Назначение документа

Версия v0.5 добавляет в CTOR:

- систему лобби (lobbies)  
- комнаты (rooms)  
- матчмейкинг (matchmaking)  
- очереди ожидания  
- базовую модель рейтинга/уровня (для фильтрации матчей)  

Цель: превратить CTOR в полноценную онлайн‑игру с:

- быстрым подбором соперников  
- приватными и публичными комнатами  
- командными лобби  
- структурой, пригодной для турниров и федерации.

---

# 2. Новые сущности

v0.5 добавляет:

1. **Lobby** — лобби, в котором игроки собираются перед матчем  
2. **Room** — комната/сессия, связанная с матчем или подготовкой к нему  
3. **MatchmakingQueue** — очередь матчмейкинга  
4. **PlayerProfile** — профиль игрока (минимальный)  

---

# 3. PlayerProfile

Минимальный профиль игрока для матчмейкинга:

```json
{
  "player_id": "PLAYER_1",
  "rating": 1500,
  "region": "EU",
  "tags": ["casual", "mobile"]
}
```

### Поля:

| Поле | Тип | Описание |
|------|-----|----------|
| player_id | строка | Уникальный ID игрока |
| rating | число | Условный рейтинг (ELO‑подобный) |
| region | строка | Регион (EU, NA, ASIA и т.д.) |
| tags | массив | Теги (casual, ranked, mobile и т.п.) |

---

# 4. Lobby

Лобби — это место, где игроки собираются перед матчем.

```json
{
  "lobby_id": "LOBBY_001",
  "owner_id": "PLAYER_1",
  "mode": "H-H",
  "status": "OPEN",
  "players": [
    { "player_id": "PLAYER_1" },
    { "player_id": "PLAYER_2" }
  ],
  "max_players": 2,
  "is_public": true
}
```

### Поля:

| Поле | Тип | Описание |
|------|-----|----------|
| lobby_id | строка | ID лобби |
| owner_id | строка | Создатель лобби |
| mode | строка | H-H, H-AI, AI-AI, TEAM-TEAM |
| status | строка | OPEN / FULL / STARTED / CLOSED |
| players | массив | Список игроков |
| max_players | число | Максимум игроков |
| is_public | bool | Публичное или приватное |

---

# 5. Room

Room — это сущность, связанная с матчем или подготовкой к нему.

```json
{
  "room_id": "ROOM_001",
  "match_id": "MATCH_001",
  "lobby_id": "LOBBY_001",
  "status": "IN_PROGRESS"
}
```

### Поля:

| Поле | Тип | Описание |
|------|-----|----------|
| room_id | строка | ID комнаты |
| match_id | строка | ID матча (если создан) |
| lobby_id | строка | ID лобби (если есть) |
| status | строка | WAITING / IN_PROGRESS / FINISHED |

---

# 6. MatchmakingQueue

Очередь матчмейкинга:

```json
{
  "queue_id": "QUEUE_RANKED_EU",
  "mode": "H-H",
  "region": "EU",
  "min_rating": 1200,
  "max_rating": 1800
}
```

Игроки добавляются в очередь с профилем.

---

# 7. HTTP API для лобби и матчмейкинга

Базовый URL:

```text
https://ctor-server.example.com/api/v1
```

---

## 7.1 Создание лобби

**POST** `/lobbies`

```json
{
  "mode": "H-H",
  "max_players": 2,
  "is_public": true
}
```

**Ответ:**

```json
{
  "lobby_id": "LOBBY_001",
  "status": "OPEN"
}
```

---

## 7.2 Присоединение к лобби

**POST** `/lobbies/{lobby_id}/join`

```json
{
  "player_id": "PLAYER_2"
}
```

**Ответ:**

```json
{
  "lobby_id": "LOBBY_001",
  "players": [
    { "player_id": "PLAYER_1" },
    { "player_id": "PLAYER_2" }
  ],
  "status": "FULL"
}
```

---

## 7.3 Выход из лобби

**POST** `/lobbies/{lobby_id}/leave`

```json
{
  "player_id": "PLAYER_2"
}
```

---

## 7.4 Старт матча из лобби

**POST** `/lobbies/{lobby_id}/start`

Только `owner_id` или `ADMIN`.

**Ответ:**

```json
{
  "room_id": "ROOM_001",
  "match_id": "MATCH_001",
  "status": "IN_PROGRESS"
}
```

---

## 7.5 Добавление в очередь матчмейкинга

**POST** `/matchmaking/queues/{queue_id}/join`

```json
{
  "player_id": "PLAYER_3",
  "rating": 1450,
  "region": "EU",
  "tags": ["ranked"]
}
```

**Ответ:**

```json
{
  "queue_id": "QUEUE_RANKED_EU",
  "status": "QUEUED"
}
```

---

## 7.6 Выход из очереди матчмейкинга

**POST** `/matchmaking/queues/{queue_id}/leave`

```json
{
  "player_id": "PLAYER_3"
}
```

---

# 8. WebSocket‑события для лобби и матчмейкинга

Клиенты могут подписываться на события лобби и очередей через WebSocket.

---

## 8.1 Событие: обновление лобби

```json
{
  "type": "lobby_update",
  "payload": {
    "lobby_id": "LOBBY_001",
    "status": "FULL",
    "players": [
      { "player_id": "PLAYER_1" },
      { "player_id": "PLAYER_2" }
    ]
  }
}
```

---

## 8.2 Событие: матч создан из лобби

```json
{
  "type": "lobby_match_started",
  "payload": {
    "lobby_id": "LOBBY_001",
    "room_id": "ROOM_001",
    "match_id": "MATCH_001"
  }
}
```

---

## 8.3 Событие: найден матч (matchmaking)

```json
{
  "type": "match_found",
  "payload": {
    "queue_id": "QUEUE_RANKED_EU",
    "room_id": "ROOM_010",
    "match_id": "MATCH_777",
    "players": [
      { "player_id": "PLAYER_3" },
      { "player_id": "PLAYER_8" }
    ]
  }
}
```

---

# 9. Роли и права в контексте v0.5

Используются роли и permissions из v0.4.

### Примеры:

- Игрок (UI) должен иметь право `JOIN_LOBBY`, `JOIN_QUEUE`.  
- Администратор — `CREATE_LOBBY`, `TERMINATE_MATCH`, `MANAGE_QUEUES`.  

Можно расширить таблицу permissions:

| Permission | Описание |
|------------|----------|
| JOIN_LOBBY | Присоединяться к лобби |
| CREATE_LOBBY | Создавать лобби |
| JOIN_QUEUE | Вставать в очередь |
| MANAGE_QUEUES | Управлять очередями |
| START_LOBBY_MATCH | Стартовать матч из лобби |

---

# 10. Применение v0.5 в модулях CTOR

| Модуль | Лобби | Очереди | Роль |
|--------|-------|---------|------|
| CTOR-UI | Да | Да | Клиент игрока |
| CTOR-Engine (Server) | Да | Да | Сервер матчей |
| CTOR-AI-AI | Частично | Да | Боты могут участвовать в очередях |
| CTOR-H-AI | Да | Да | Игрок + бот через лобби |
| CTOR-H-H | Да | Да | Игроки через лобби и очереди |
| CTOR-TEAM-TEAM | Да | Да | Командные лобби и очереди |

---

# 11. Статус документа

Версия: **v0.5**  
Статус: **расширенный игровой контракт (лобби + матчмейкинг)**  
Назначение:  
- быстрый подбор соперников  
- поддержка лобби и комнат  
- подготовка к турнирам и федерации CTOR  
- основа для рейтинговых и казуальных режимов  

Совместим с v0.1–v0.4.

---
