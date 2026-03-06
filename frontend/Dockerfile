# === ЭТАП 1: Сборка фронтенда ===
FROM node:18-alpine AS build

WORKDIR /app

# Копируем файлы зависимостей
COPY package*.json ./
COPY pnpm-lock.yaml* ./

# Устанавливаем зависимости
RUN npm install -g pnpm
RUN pnpm install --frozen-lockfile || npm install

# Копируем исходный код
COPY . .

# Собираем проект (Create React App)
RUN npm run build


# === ЭТАП 2: Сервер Nginx ===
FROM nginx:alpine

# Копируем собранные файлы из папки build (ВАЖНО!)
COPY --from=build /app/build /usr/share/nginx/html

# Копируем конфиг nginx
COPY nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]