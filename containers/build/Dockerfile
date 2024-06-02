# Wybierz obraz bazowy z Node.js do budowania aplikacji
FROM node:14 AS builder

RUN apt-get update -y && \
    apt-get upgrade -y

RUN npm install yarn -y

RUN git clone https://github.com/Dawid511/webpack-typescript-jest-less

# Ustaw katalog roboczy w kontenerze
RUN ls 
RUN pwd

WORKDIR /app

# Zainstaluj zależności
RUN yarn install

RUN ls 
RUN pwd
# Zbuduj aplikację w trybie produkcyjnym
RUN yarn build:prod