# Solucionando problemas

Aqui estão as minhas anotações pessoais de raciocínio para resolver esse desafio.

## Primeiros passos com docker-compose

Primeiramente notei que o [docker-compose](./docker-compose.yaml) continha a rede `backend` declarada no final do arquivo e que os containers declarados utilizavam a mesma, percebi que alguns containers usavam a rede `frontend` mas ela não havia sido declarada como a anterior, portanto declarei ela.

## Mais um erro no docker-compose

Notei um typo no [docker-compose](./docker-compose.yaml), dessa vez tem a ver com o banco de dados em memória [Redis](https://redis.io/). A imagem docker está correta entretando o nome do serviço está como `reids`. Lendo o arquivo [main.go](./services/reader/main.go) é possível indentificar que ele tenta conectar com o host `redis`, logo esse deve ser o nome do service no arquivo docker-compose.
