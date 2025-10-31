# 1. Créer le réseau
docker network create todo-net

# 2. Lancer PostgreSQL
docker run -d \
  --name todo-db \
  --network todo-net \
  -e POSTGRES_DB=todo \
  -e POSTGRES_USER=todouser \
  -e POSTGRES_PASSWORD=supersecret \
  -v todo-db-data:/var/lib/postgresql/data \
  postgres:16-alpine

# 3. Construire l'image de l'API
docker build -t todo-api:2.2.0 .

# 4. Lancer l'API reliée à PostgreSQL
docker run -d \
  --name todo-api \
  --network todo-net \
  -e TODO_DB_URL=postgresql://todouser:supersecret@todo-db:5432/todo \
  -p 8000:8000 \
  todo-api:2.2.0

# 5. Tester l'API
curl -s http://127.0.0.1:8000/health | jq
curl -s -X POST http://127.0.0.1:8000/todos -H "Content-Type: application/json" -d '{"title":"Task 1"}' | jq
curl -s http://127.0.0.1:8000/todos | jq

# 6. Sauvegarde logs
mkdir -p logs
docker logs todo-api > logs/todo-api.log

# 7. Nettoyage (attention aux ressources utilisées)
docker stop todo-api todo-db
docker rm todo-api todo-db
docker network rm todo-net
docker volume rm todo-db-data
docker image prune


# 8. Rapport synthétique
Architecture finale

API : conteneur FastAPI todo-api

DB : conteneur PostgreSQL todo-db

Réseau : todo-net pour communication API ↔ DB

Volume : todo-db-data pour persistance PostgreSQL

Stratégie de tagging et rollback

major.minor.patch : versionnement sémantique (2.0.0, 2.1.0, 2.2.0)

latest : pointe toujours vers la dernière version stable

rollback : permet de revenir rapidement à une version précédente

Diagnostics réalisés

docker logs -f todo-api pour suivre le démarrage

docker inspect todo-api pour vérifier les variables d’environnement

docker stats todo-api todo-db pour surveiller l’usage CPU/mémoire

docker events --since 5m pour les événements récents

# 9. Requêtes de tests

C:\Users\robin>curl -s http://127.0.0.1:8000/health
{"status":"ok"}
C:\Users\robin>curl -s -X POST http://127.0.0.1:8000/todos -H "Content-Type: application/json" -d '{"title":"Task 1"}'
{"detail":[{"type":"json_invalid","loc":["body",0],"msg":"JSON decode error","input":{},"ctx":{"error":"Expecting value"}}]}
C:\Users\robin>curl -s http://127.0.0.1:8000/todos
{}