# Étape de construction
FROM node:19-alpine AS build
WORKDIR /usr/src/app

# Copie des fichiers nécessaires pour l'installation des dépendances
COPY package.json package-lock.json ./
RUN npm install --legacy-peer-deps

# Copie du reste du code
COPY . .
RUN npm run build

# Étape de production avec Nginx
FROM nginx:1.23.2-alpine

# Changer les permissions des fichiers Nginx
RUN chmod -R 755 /usr/share/nginx/html

# Copier le fichier de configuration Nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copier les fichiers construits dans le répertoire Nginx
COPY --from=build /usr/src/app/dist /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80
