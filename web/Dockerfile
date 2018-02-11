FROM nginx:alpine

RUN apk add --no-cache git nodejs

WORKDIR /app

COPY default.conf /etc/nginx/conf.d/default.conf

RUN git clone https://github.com/mraatika/nearestdepartures.git .
RUN git checkout $branch

COPY .env.local /app

RUN npm install && npm run build

RUN rm ./build/service-worker.js

RUN cp -r ./build/* /usr/share/nginx/html

