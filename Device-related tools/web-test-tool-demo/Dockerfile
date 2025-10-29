# Stage 1: Build the application
FROM node:16 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run generate

# Stage 2: Create the final image
FROM node:16-alpine
WORKDIR /app
COPY --from=build /app/dist ./dist
COPY --from=build /app/nuxt.config.js ./
COPY --from=build /app/package.json ./
RUN npm install --production --legacy-peer-deps

EXPOSE 3000
CMD [ "npm", "start" ]
