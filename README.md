# Solucionando problemas

Aqui estão as minhas anotações pessoais de raciocínio para resolver esse desafio.

## Primeiros passos com docker-compose

Primeiramente notei que o [docker-compose](./docker-compose.yaml) continha a rede `backend` declarada no final do arquivo e que os containers declarados utilizavam a mesma, percebi que alguns containers usavam a rede `frontend` mas ela não havia sido declarada como a anterior, portanto declarei ela.

## Mais um erro no docker-compose

Notei um typo no [docker-compose](./docker-compose.yaml), dessa vez tem a ver com o banco de dados em memória [Redis](https://redis.io/). A imagem docker está correta entretando o nome do serviço está como `reids`. Lendo o arquivo [main.go](./services/reader/main.go) é possível indentificar que ele tenta conectar com o host `redis`, logo esse deve ser o nome do service no arquivo docker-compose.

## Portas trocadas no docker-compose

Ao ler os arquivos [main.py](./services/writer/main.py) e [main.go](./services/reader/main.go), pude perceber que o `reader` deve escutar na porta 8080 e o `writer` deve escutar na porta 8081, o que não acontece no [docker-compose](./docker-compose.yaml), já que as portas estão trocadas, para corrigir foi necessário inverter as portas.

## Baixando dependências no Dockerfile (main.go)

Este [Dockerfile](./services/reader/Dockerfile) não continha os comandos para baixar as dependências usadas pelo [main.go](./services/reader/main.go), para solucionar foi preciso inicializar o go mod com `RUN ["go","mod","init"]` e adicionar as dependências com `RUN ["go","get","github.com/go-redis/redis"]` e `["go","get","github.com/rs/cors""]`.
