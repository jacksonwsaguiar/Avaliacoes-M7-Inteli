# Docker file
FROM - Imagem de referencia para criação
WORKDIR - pasta destinada ao app docker
COPY - copia os arquivos para a pasta destinada
RUN - Executa um comando, proveniente de mais uma etapa na contrução da imagem, para ambos os casos é usado para instalar as dependencias.
CMD - Executa a linha de comando, é usado para inicializar a aplicação de forma padrão.
## Backend
docker hub: https://hub.docker.com/r/jacksonaguiar/backend-image-prova

Imagem base python:slim, é uma versão mais leve do python, com os pacotes mais basicos.
```bash
# Imagem base
FROM python:slim

WORKDIR /app

COPY ./requirements.txt /app/requirements.txt

RUN pip install --no-cache-dir -r /code/requirements.txt

COPY . /app

CMD ["uvicorn", "main:app", "--port", "80"]
```
## Frontend
docker hub: https://hub.docker.com/r/jacksonaguiar/frontend-image-prova

Imagem base node:14, é uma versão mais estável e que tem as funções minimas para executar qualquer aplicação NODE.
```bash
FROM node:14

WORKDIR /app

COPY package*.json ./app/

RUN npm install

COPY . .

CMD ["node", "server.js" ]
```

# Docker compose
VERSION - versão do docker compose
SERVICES - Todos os servições que construidos e executados
RESTART - caso ocorra qualquer erro, sempre reinicializar o container
BUILD (context) - Contexto ao  qual a aplicação faz parte
DEPENDS_ON: Aguarda a construção e inicialização de um serviço para iniciar o processo dele.
PORTS - Portas que serão expostas ao sistema
```bash
version: '1.0'
services:
  backend:
    restart: always
    build:
      context: ./backend

    ports:
      - "3000:3000"

  frontend:
    restart: always
    build:
      context: ./frontend
    depends_on:
      - backend
    ports:
      - "8000:8000"

```