# faz a build com maven 
FROM maven:3.8.4-openjdk-11 AS build
WORKDIR /app

# copia ops arquivos de configuração maven
COPY pom.xml .
COPY src ./src

# faz a build e copia as dependencias
RUN mvn clean package -DskipTests && \
    mkdir -p dependency-jars && \
    mvn dependency:copy-dependencies -DoutputDirectory=dependency-jars

# parte 2: cria a imagem final com tomcat
FROM tomcat:10.1-jdk11-openjdk-slim

# remove as aplicatções default do tomcat
RUN rm -rf /usr/local/tomcat/webapps/*

# copia o arquivo war da build pro diretorio de webapps do tomcat
COPY --from=build /app/target/SmartShop-0.0.1-SNAPSHOT.war /usr/local/tomcat/webapps/ROOT.war

# copia as dependecias da build pra biblioteca do tomcat
COPY --from=build /app/dependency-jars /usr/local/tomcat/lib/

# copia o arquivo context.html para o tomcat
COPY src/main/webapp/META-INF/Context.xml /usr/local/tomcat/conf/context.xml

# abre as portas
EXPOSE 8080

# inicia o tomcat
CMD ["catalina.sh", "run"]
