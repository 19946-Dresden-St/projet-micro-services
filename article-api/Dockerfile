# docker build -t article-api .

FROM node:20-alpine

WORKDIR /build

RUN npm install -g prisma

ENV DATABASE_URL="file:./dev.db"
ENV AUTH_API_URL="auth-api:4000"

COPY package.json .
COPY package-lock.json .

COPY tsconfig.build.json .
COPY tsconfig.json .

COPY src src
COPY prisma prisma

COPY nest-cli.json .

RUN npm install

RUN npx prisma migrate dev --name init

RUN npm run build

EXPOSE 3000

CMD [ "npm" ,"run", "start" ]