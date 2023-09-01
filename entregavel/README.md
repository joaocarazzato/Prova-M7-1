# Avaliação Módulo 7 - 1
## Criação de Dockerfiles e docker-compose para uma aplicação web
Esse repositório tem como objetivo criar um docker-compose e dois Dockerfiles(que podem ser encontrados em nosso [Docker Hub](https://hub.docker.com/repository/docker/joaocarazzato/provamodulo7/general)) para as partes de frontend e backend da aplicação, possuindo nesse caso, dois containers.

Os Dockerfiles podem ser encontrados em suas respectivas pastas:
- Frontend - O Dockerfile do Frontend foi realizado dessa maneira pela seguinte questão: Precisávamos de uma imagem do node para conseguirmos rodar a aplicação do node, então, pegamos a imagem oficial do Docker Hub responsável por aplicações node, após isso, criamos um diretório de trabalho dentro do container, copiamos todos os arquivos da pasta frontend para dentro do container, instalamos as dependências do node com ```npm i```, copiamos mais uma vez o que instalamos para ter certeza que tudo está dentro do container, então, executamos usando o comando ```CMD``` e seus argumentos necessários.
- Backend - O Dockerfile do Backend foi realizado dessa maneira pela seguinte questão: Tinhamos que executar nossa aplicação utilizando o serviço Python, para isso, instalamos a ultima versão do Python(que pode ser substituida pelo Alpine caso queira algo mais leve) e criamos outro diretório de trabalho para os códigos não ficarem em uma mesma pasta, após isso copiamos todos os arquivos da pasta para o container e executamos a instalação dos requerimentos fornecidos(bibliotecas utilizadas na criação do projeto), então copiamos os arquivos mais uma vez para ter certeza que está tudo certo e em seguida executamos a aplicação com o comando ```CMD``` e seus argumentos necessários.

### Agora, por que o docker-compose foi estruturado dessa forma?

Ambos containers estão bem parecidos no docker-compose, de forma geral, o que fazemos é a criação de dois containers, um nomeado ```application-back``` e outro ```application-front```, puxamos as imagens de ambos containers do nosso Docker Hub(porém é possível buildar através dos Dockerfiles), definimos o modo da rede como host a fim de atrelá-los com o sistema original(a própria máquina) e facilitar a conexão de ambos por estarem na mesma rede, em seguida habilitamos o auto restart caso o container pare, expomos as portas designadas para cada container e mapeamos elas a uma porta do sistema principal, e por fim, definimos os nomes dos containers. A única diferença de um para outro, é que o container ```application-front```, depende da inicialização do ```application-back``` para se iniciar.

## Como executar a aplicação?

É muito simples, para executar a aplicação, primeiro se direcione ao diretório onde o docker-compose está localizado, e em seguida digite:

```
docker compose up
```

A partir dai, sua aplicação já está sendo executada, e pode ser acessada tanto o front em [localhost:3000](http://localhost:3000), quanto o back em [localhost:8000](http://localhost:8000). Caso queira parar a aplicação, apenas aperte as teclas ```Ctrl + C```. 

Após isso, caso queira apagar os containers, apenas digite:
```
docker compose down
```