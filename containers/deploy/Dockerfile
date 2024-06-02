# Wybierz obraz bazowy z Node.js do uruchomienia aplikacji
FROM node:16

# Ustaw katalog roboczy w kontenerze
WORKDIR /usr/src/app

# Skopiuj zależności produkcyjne z etapu budowania
COPY --from=builder /usr/src/app/package*.json ./

# Zainstaluj zależności produkcyjne
RUN npm install --only=production

# Skopiuj zbudowane pliki aplikacji z etapu budowania
COPY --from=builder /usr/src/app/dist ./dist
COPY --from=builder /usr/src/app/public ./public

# Ekspozycja portu, na którym będzie działać aplikacja
EXPOSE 8080

# Uruchom aplikację
CMD ["npm", "start"]
