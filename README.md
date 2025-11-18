# uber-database-4-3-8

## Start Container
```
docker compose up -d
```

## Connect
```
sqlcmd -S localhost -U SA -P 'YourStrong@Password123'
```

## Commands
The docker compose uses volumes which persist container restart/server reboot.
Deleting a docker container does not delete a Docker Volume.

- List docker containers
```
docker ps
```

- Delete docker container
```
docker rm -f <container_name>
```

- List docker volumes
```
docker volume ls
```

- Delete docker volume
```
docker volume rm <volume_name>
```

- Backup volume with database data
```
docker run --rm \
  -v uber_database_4_3_8_mssql_data:/volume_data \
  -v $(pwd):/backup \
  alpine \
  tar czvf /backup/mssql_backup.tar.gz -C /volume_data .
```

- Restore volume with database data
```
docker run --rm \
  -v uber-database_4_3_8_mssql_data:/volume_data \
  -v $(pwd):/backup \
  alpine \
  sh -c "cd /volume_data && tar xzvf /backup/mssql_backup.tar.gz --strip 1"
```

