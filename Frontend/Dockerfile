# define a imagem base como o alpine ( versao mais leve para rodar o node.js)
FROM node:alpine

# define o diretorio de trabalho onde todos os outro comandos vao ser executados
WORKDIR /usr/src/app

# copia os arquivos do diretorio para insatalar as dependecias do node js
COPY package*.json ./

# executa o comando para instalar as dependencias
RUN npm install

#instala o angular cli dentro do conteirar para poder usar o comando ng
RUN npm install -g @angular/cli

# copia todos os arquivos do diretorio atual para o diretorio de trabalho
COPY . .

# informa o docker em qual porta o conteiner sera executado
EXPOSE 4201

#define os comandos padroes para quando o contanier for executado
CMD ["ng", "serve", "--host", "0.0.0.0"]

