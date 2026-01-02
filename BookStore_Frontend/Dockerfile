# Stage 1: Build
FROM node:alpine AS build

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

RUN npm run build

# Stage 2: Preview (Run)
FROM node:18-alpine
WORKDIR /app

COPY --from=build /app/dist ./dist
COPY package*.json ./
COPY vite.config.ts ./

RUN npm install typescript vite --save-dev

EXPOSE 5173

CMD ["npm", "run", "preview", "--", "--host", "--port", "5173"]