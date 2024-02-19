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

## Rodando os serviços e bugfix (main.go)

Ao rodar o  [docker-compose](./docker-compose.yaml) com `docker-compose down; docker-compose up --build` notei que a aplicação `reader` retornava o seguinte erro: `./main.go:27:26: too many arguments in call to client.cmdable.Get`, para arrumar isso foi preciso apenas remover o primeiro argumento já que segundo o erro, esperamos apenas um argumento e não dois.

## Outra descoberta rodando o docker-compose

Outra coisa que acontece ao rodar o [docker-compose](docker-compose.yaml) é que o serviço web (frontend) reporta estar escutando na porta 3000 mas a porta declarada é a 5000. Solucionar esse problema é bem simples, será preciso mudar a propriedade `ports` do serviço `web` de `5000:5000` para `3000:3000`.

## Corrigindo o erro ao tentar rodar o writer

Rodando o [docker-compose](docker-compose.yaml) é possível perceber que o serviço `writer` não sobe, para corrigir isso foi necessaŕio adicionar o comando para baixar as dependências (redis) e alterar o comando para rodar a aplicação em si.
