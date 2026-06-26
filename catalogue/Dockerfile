FROM node:20.19.5-alpine3.22 as build 
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.19.5-alpine3.22
# Create a group and user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
WORKDIR /opt/server
EXPOSE 8080
LABEL com.project="roboshop"  \
      component="catalogue"   \
      created_by="vikas"
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
COPY --from=build --chown=roboshop:roboshop /opt/server /opt/server/
USER roboshop
CMD ["server.js" ]
ENTRYPOINT [ "node" ]   
#PID 1



# FROM node:20 
# WORKDIR /opt/server
# EXPOSE 8080
# COPY package.json .
# COPY *.js .
# RUN npm install 
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD [ "node", "server.js" ]