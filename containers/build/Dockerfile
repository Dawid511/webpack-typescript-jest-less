# Wybierz obraz bazowy z Node.js do budowania aplikacji
FROM node:14 AS builder

RUN apt-get update -y && \
    apt-get upgrade -y

RUN npm install yarn -y

RUN git clone https://github.com/Dawid511/ping-pong-java

# Ustaw katalog roboczy w kontenerze
WORKDIR /usr/src/app

# Skopiuj plik package.json i package-lock.json (jeśli istnieje)
COPY package*.json ./

# Zainstaluj zależności
RUN npm install

# Skopiuj resztę plików aplikacji
COPY . .

# Zbuduj aplikację w trybie produkcyjnym
RUN npm run build:prod