# meltano-poc

Start project
```bash
docker run -v $(pwd):/meltano -w /meltano -u $(id -u):$(id -g) meltano/meltano init meltano-project
```

Create a alias for meltano docker image:
```bash
alias meltano='docker run -it -v $(pwd)/meltano-project:/meltano -w /meltano/meltano-project -u $(id -u):$(id -g) -p 5000:5000 meltano/meltano'
```

Configure tap:
```bash
meltano add  extractor tap-gitlab
meltano config tap-gitlab set projects meltano/meltano
meltano config tap-gitlab set start_date 2022-06-01T00:00:00Z
meltano select tap-gitlab tags
```

Start a local database:
```bash
docker run --name postgres -e POSTGRES_PASSWORD=meltano -e POSTGRES_USER=meltano -e POSTGRES_DB=warehouse -d -p 5432:5432 postgres
```

Configure target:
```bash
meltano add loader target-postgres
meltano config target-postgres set postgres_user meltano
meltano config target-postgres set postgres_password meltano
meltano config target-postgres set postgres_database warehouse
```

Run pipeline:
```
meltano elt tap-gitlab target-postgres
```


Change entrypoint to bash for debugging, if necessary:
```bash
docker run -it -v $(pwd):/meltano -w /meltano -u $(id -u):$(id -g) --entrypoint bash meltano/meltano
```
