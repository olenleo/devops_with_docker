# Backend Dockerfile

FROM golang:latest

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN go build

ENV REQUEST_ORIGIN=http://localhost:5000

CMD ./server

# Frontend Dockerfile


FROM node:14

WORKDIR /usr/src/app

EXPOSE 5000

COPY . .

ENV REACT_APP_BACKEND_URL="http://localhost:8080"

RUN npm install
RUN npm run build
RUN npm install -g serve

CMD serve -s -l 5000 build
