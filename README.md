# Minimal Laravel Docker Container

Ambiente de Desenvolvimento com o Mínimo Necessário para Desenvolvimento com Laravel e Docker

## Pré-requisitos

- Docker
- Docker Compose

## Configurações Iniciais

Como este projeto tem a intenção de oferecer o mínimo necessário para executar uma aplicação Laravel em ambiente de desenvolvimento, não há nada de Laravel neste repositório. Então é necessário que você baixo o Laravel diretamente do repositório oficial. Observe que se não for especificado, será instalada a última versão do Laravel, caso deseje utilizar uma versão mais antiga deve-se especificar a versão que deseja usar quando for baixar o Laravel.

Após baixar o Laravel copie o conteúdo deste repositório para dentro do diretório do Laravel que você acabou de baixar.

### Versão do PHP e do Laravel

Verifique qual a versão do PHP mais apropriada para a versão do Laravel que deseja instalar/utilizar e altere esta versão (se necessário) no Dockerfile.

Por exemplo, para alterar a versão do PHP de 7.1 para 7.4 basta altera linha abaixo no Dockerfile

```
FROM php:7.1-apache
```

para a versão desejada:

```
FROM php:7.4-apache
```

### Nome do Projeto

É possível alterar o nome do projeto. Por padrão o nome do projeto é laravel, mas é possível alterar o nome do projeto no Dockerfile. Por exemplo, vamos criar um projeto em laravel que se chamará blogapp:

### Variáveis de Ambiente

Para definir as variáveis de ambiente da aplicação (porta, nome da aplicação, credenciais de acesso, etc) copie o arquivo `.env.example` e renomei-o para `.env`.

```
APP_NAME=laravel
APP_PORT=8000
```

Se você trocou o nome do projeto no Dockerfile altere o nome da variável `APP_NAME` para o mesmo valor de `PROJECTNAME` em Dockerfile.

## Acessando Containers

Após clonar o projeto acesse o diretório do projeto (não esqueça de copiar e renomear o `.env.example` para `.env` antes) execute o comando a seguir:

```
docker compose up -d
```

Após executar o comando anterior é possível visualizar os containers e demais informações dele com o comando:

```
docker container ls
```

Para acessar o conteúdo do container execute o comando:

```
docker exec -it laravel_app bash
```

Este comando executa o bash dentro do container. Para sair do bash execute o comando `exit`. Também é possível executar comandos de dentro do container sem executar o bash, por exemplo para ver a versão do PHP execute o comando:

```
docker exec laravel_app php -v
```

Para executar, por exemplo, o composer execute o comando:

```
docker exec laravel_app composer
```

> **Observe que para executar o bash é necessário informar os parâmetros -it. Este parâmetro habilita o terminal interativo, sem informar esse parâmetro o Docker executará o bash e sairá imediatamente, impedindo que sejam executados comandos nele.**