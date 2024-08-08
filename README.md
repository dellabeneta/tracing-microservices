# tracing-microservices
Lab simples com base no https://www.youtube.com/watch?v=LGhrGg-CJ5Y


# Projeto Go com Docker

Este projeto é uma aplicação Go containerizada usando Docker, com configuração adicional para o OpenTelemetry Collector.

## Pré-requisitos

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Go](https://golang.org/) (opcional para desenvolvimento)

## Estrutura do Projeto

- **Dockerfile**: Arquivo de configuração para a construção da imagem Docker da aplicação Go.
- **compose.yaml**: Arquivo de configuração do Docker Compose para orquestrar múltiplos containers.
- **otel-collector-config.yaml**: Arquivo de configuração para o OpenTelemetry Collector.

## Configuração e Uso

### 1. Construir a Imagem Docker

Para construir a imagem Docker da aplicação Go, execute:

```bash
docker build -t nome-da-imagem .
```

### 2. Executar com Docker Compose

Para iniciar os containers definidos no `compose.yaml`, execute:

```bash
docker-compose -f compose.yaml up
```

### 3. OpenTelemetry Collector

O `otel-collector-config.yaml` define a configuração para o OpenTelemetry Collector. Ele pode ser usado para monitoramento e rastreamento distribuído. Para iniciar o Collector, certifique-se de que ele está configurado corretamente no `compose.yaml`.

## Personalização

Você pode personalizar o projeto editando os arquivos Go, Dockerfile, e as configurações no `compose.yaml` e `otel-collector-config.yaml` conforme suas necessidades.

## Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para abrir um *issue* ou enviar um *pull request*.
