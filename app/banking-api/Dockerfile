FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

# 👈 هنا نضيف Postgres client
RUN apk add --no-cache postgresql-client

COPY . .

CMD ["node", "app.js"]