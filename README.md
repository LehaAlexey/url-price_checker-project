# Services Workspace

Монорепа с набором сервисов для парсинга цен, хранения пользователей и истории, и HTTP BFF.

## По оценке

Файл покрытый тестами - `services/parsing/internal/parser/extractor_test.go`.

## Состав

- `services/parsing` - читает `ParseRequested` из Kafka и пишет `PriceMeasured`
- `services/users` - пользователи + URL, scheduler публикует `ParseRequested`
- `services/history` - читает `PriceMeasured`, пишет в БД и кэширует в Redis
- `services/gateway` - HTTP BFF, проксирует users/history по gRPC

## Запуск

- Docker: `docker compose up -d --build`
- Локально: поднимаете инфраструктуру через Docker, а сервисы запускаете по отдельности

## Что нужно, чтобы поднять все сервисы

Коротко: нужен Docker, остальное уже в compose.

- PostgreSQL, Kafka и Redis поднимаются контейнерами из `docker-compose.yaml`
- Сервисам нужен только `config.yaml` (он лежит в каждом сервисе)

Порты по умолчанию:
- Gateway: `:8080`
- Parsing: `:8070`
- Users: `:8071` (gRPC `:50061`)
- History: `:8072` (gRPC `:50062`)
- Kafka UI: `:8081`
