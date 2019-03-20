FROM alpine:edge
RUN apk update && apk add --update nodejs nodejs-npm
RUN npm install --unsafe-perm -g @angular/cli
RUN apk add --no-cache chromium
RUN mkdir -p /opt/cp-frontend
