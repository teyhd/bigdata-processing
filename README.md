# bigdata-processing
Parallel and distributed big data processing

### Установка (локально)
venv, Poetry и зависимости:
```
python -m venv venv
venv\Scripts\activate 
pip install poetry
poetry install --no-root
```
Запустить тесты:
```
poetry run pytest -v

Локальный запуск через spark-submit (client mode):
- На локальной машине без Docker (Spark master = local[*]):
```
python -m pip show pyspark
spark-submit --master local[*] --deploy-mode client src/main.py --n 10
```
- Подключаясь к мастер-ноде из Docker Compose:
```
docker compose up -d spark-master spark-worker
spark-submit --master spark://localhost:7077 --deploy-mode client src/main.py --n 10
```


### Запуск через Docker Compose
1) Поднять кластер Spark (master + worker) и клиент:
```
docker compose up -d spark-master spark-worker
```
2) Выполнить задачу из контейнера клиента в client-режиме (пример с N=10):
```
docker compose run --rm client /opt/bitnami/spark/bin/spark-submit --master spark://spark-master:7077 --deploy-mode client src/main.py --n 10
```

Остановить кластер:
```
docker compose down
```
