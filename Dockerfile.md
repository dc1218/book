FROM node:8.5-alpine  
MAINTAINER Test <Test@gmail.com>  
RUN npm install gitbook-cli -g  
ARG GITBOOK_VERSION=3.2.3  
RUN gitbook fetch $GITBOOK_VERSION  
ENV BOOKDIR /book  
VOLUME $BOOKDIR  
EXPOSE 4000  
WORKDIR $BOOKDIR  

CMD ["gitbook","-V"]