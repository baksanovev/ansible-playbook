# Ansible Playbook: ClickHouse, Vector, LightHouse

Домашнее задание по теме «Работа с roles».

Playbook устанавливает и настраивает:

- ClickHouse
- Vector
- LightHouse
- nginx

## Infrastructure

Используются три целевых хоста:

- `clickhouse` — установка ClickHouse
- `vector` — установка Vector
- `lighthouse` — установка LightHouse и nginx

## Roles

### ClickHouse

Используется готовая роль:

`AlexeySetevoi/ansible-clickhouse`

Версия:

`1.13`

### Vector

Собственная роль:

`baksanovev/vector-role`

Версия:

`1.0.0`

### LightHouse

Собственная роль:

`baksanovev/lighthouse-role`

Версия:

`1.0.0`

## Установка ролей

Перед запуском playbook необходимо установить зависимости:

```bash
ansible-galaxy install -r requirements.yml -p roles
```

## Проверка inventory

```bash
ansible-inventory --graph
```

## Проверка доступности хостов

```bash
ansible all -m ping
```

## Проверка синтаксиса

```bash
ansible-playbook playbook.yml --syntax-check
```

## Запуск playbook

```bash
ansible-playbook playbook.yml
```

## Проверка идемпотентности

При повторном запуске playbook изменений нет:

```text
PLAY RECAP
clickhouse-01  : ok=26 changed=0 unreachable=0 failed=0
lighthouse-01  : ok=7  changed=0 unreachable=0 failed=0
vector-01      : ok=6  changed=0 unreachable=0 failed=0
```

## Результат

В результате выполнения playbook:

- ClickHouse установлен и запущен на `clickhouse-01`;
- Vector установлен и запущен на `vector-01`;
- LightHouse установлен на `lighthouse-01`;
- nginx настроен для публикации интерфейса LightHouse;
- повторный запуск playbook не вносит изменений.

## Репозитории ролей

Vector role:

`https://github.com/baksanovev/vector-role`

LightHouse role:

`https://github.com/baksanovev/lighthouse-role`
