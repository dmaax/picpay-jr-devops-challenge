# Solucionando problemas

Aqui estão as minhas anotações pessoais de raciocínio para resolver esse desafio.

## Primeiros passos com docker-compose

Primeiramente notei que o [docker-compose](./docker-compose.yaml) continha a rede `backend` declarada no final do arquivo e que os containers declarados utilizavam a mesma, percebi que alguns containers usavam a rede `frontend` mas ela não havia sido declarada como a anterior, portanto declarei ela.
