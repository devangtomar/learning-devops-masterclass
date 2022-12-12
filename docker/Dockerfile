FROM ubuntu:latest
LABEL version="1.8.0"
RUN apt-get update
WORKDIR /usr/src/app
COPY /source /usr/src/app
EXPOSE 80/tcp
CMD java hello