FROM openjdk:8-alpine
ENV SONAR_SCANNER_VERSION=2.8 \
    SONAE_URL=https://sonarsource.bintray.com/Distribution \
    SONAR_RUNNER_HOME=/opt/sonar-scanner

RUN apk add --no-cache gnupg unzip --update nodejs nodejs-npm \
    && npm install --unsafe-perm -g @angular/cli \
    && apk add --no-cache libressl wget \
    && mkdir /opt \
    && cd /opt \
    && wget -O sonarscanner.zip --no-verbose $SONAE_URL/sonar-scanner-cli/sonar-scanner-$SONAR_SCANNER_VERSION.zip \
    && unzip sonarscanner.zip \
    && mv sonar-scanner-$SONAR_SCANNER_VERSION sonar-scanner \
    && rm sonarscanner.zip
