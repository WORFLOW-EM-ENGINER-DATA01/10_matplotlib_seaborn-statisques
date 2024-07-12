# Pandas - statistiques - graphiques et séries temporelles

## Pour utiliser pandas avec Docker 

```bash
# 258e68ed31235151b61a14edd3c8b94e71018d08423b2fa3
docker run -it --rm -p 10000:8888 -v "${PWD}":/home/jovyan/work quay.io/jupyter/datascience-notebook:2024-04-29

# Token et mot de passe
jupyter server list
# récupération du token et définition du mot de passe

docker run -p 1080:1080 -p 1025:1025 maildev/maildev
psql -h localhost -U admin -d db

docker exec -it docker_postgres psql -U admin 

docker build -t ui-app .
docker run -it --rm --name env-ui-app -p 5173:5173 -v "${PWD}":/app

```
## Plan de cours

Le plan du cours est [ici](./plan.md)