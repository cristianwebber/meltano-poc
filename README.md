# meltano-poc

Start project
```bash
docker run -v $(pwd):/meltano -w /meltano -u $(id -u):$(id -g) meltano/meltano init meltano-project
```

```bash
alias meltano='docker run -it -v $(pwd):/meltano -w /meltano/meltano-project -u $(id -u):$(id -g) meltano/meltano'
```

```bash
meltano add --custom extractor tap-covid-19
```

```bash

```

```bash

```


Change entrypoint to bash for debugging
```bash
docker run -it -v $(pwd):/meltano -w /meltano -u $(id -u):$(id -g) --entrypoint bash meltano/meltano
```
