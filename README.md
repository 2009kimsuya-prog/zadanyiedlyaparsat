# ruff-lab1-fintech

Лабораторная работа 1 (60 минут): «Антифрод-фильтр банковских переводов».

Модуль `fraud_filter.py` написан с нарушениями PEP 8 и содержит потенциальные баги.
Задача: вычистить код с помощью **Ruff**, убедиться, что тесты проходят, и оформить Pull Request.

> `test_fraud_filter.py` изменять запрещено.

## Установка

```bash
pip install -r requirements-dev.txt
```

## Этап 1. Ветка

```bash
git checkout -b refactor/clean-fraud-filter
```

## Этап 2. Диагностика и автоисправление

```bash
pytest
ruff check fraud_filter.py
ruff format --check fraud_filter.py
ruff check --fix fraud_filter.py
ruff format fraud_filter.py
git diff
```

## Этап 3. Ручной рефакторинг

```bash
ruff check fraud_filter.py
ruff rule F841
```

Исправьте вручную:

- удалите неиспользуемую переменную `audit_session` (F841);
- замените `== True` (E712) и `== None` (E711) на идиоматичные конструкции (`is None`, прямая проверка булевых флагов);
- замените голый `except:` (E722) на `except ZeroDivisionError:`;
- замените `for i in range(len(transfers)):` на `for tx in transfers:`.

## Этап 4. Верификация и отправка

Все три команды должны завершиться без ошибок:

```bash
ruff format --check . && ruff check . && pytest
```

```bash
git add fraud_filter.py
git commit -m "refactor: fix ruff lint and formatting issues"
git push -u origin refactor/clean-fraud-filter
```

Откройте Pull Request `refactor/clean-fraud-filter` → `main` и передайте преподавателю ссылку
(во вкладке **Files changed** должны быть видны все изменения).
