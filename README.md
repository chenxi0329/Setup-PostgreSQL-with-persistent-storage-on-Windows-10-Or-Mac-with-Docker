#### requirements
```
You need Windows 10, docker and virtualbox installed and linked well in cmd.
```
#### kickstart a docker with PostgreSQL on Windows 10
```
docker-machine create box
docker-machine env box
docker create -v c:\db\postgresql\data --name PostgresData alpine
docker run -p 5432:5432 --name dbContainer -e POSTGRES_PASSWORD=password -d --volumes-from PostgresData postgres
docker ps -a
```

#### connect to DB using psql
```
docker run -it --rm --link dbContainer:postgres postgres psql -h postgres -U postgres
```

#### remotely run a sql file
```
docker cp test.sql dbContainer:/tmp/test.sql
docker exec -u postgres dbContainer psql postgres postgres -f /tmp/test.sql
```

#### ssh into docker container
```
docker exec -it dbContainer bash
```

#### Reference:
https://elanderson.net/2018/02/setup-postgresql-on-windows-with-docker/