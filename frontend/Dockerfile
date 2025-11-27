FROM node:18-alpine AS build

WORKDIR /app
COPY package*.json ./
# avoid analytics prompt during docker build
ENV NG_CLI_ANALYTICS=false
RUN npm install

COPY . .
RUN npm run build

FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*

# ⬇️ IMPORTANT: use your actual project name here
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
