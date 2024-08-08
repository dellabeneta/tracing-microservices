<img src="https://drive.google.com/uc?export=view&id=1KhgXrd0uwGaHQ58K9cdrWQHWzih-AV6J" width="1000">


# Stack de Observabilidade para Microsserviços com OpenTelemetry

Este repositório demonstra uma configuração de uma stack de observabilidade para microsserviços usando Docker Compose. Inclui Jaeger, Zipkin, Prometheus e OpenTelemetry Collector para coleta de métricas e rastreamento. Além disso, três microsserviços de demonstração (`goapp`, `goapp2` e `goapp3`) são incluídos para simular uma aplicação distribuída.

## Sumário

- [Pré-requisitos](#pré-requisitos)
- [Configuração](#configuração)
- [Serviços](#serviços)
  - [Jaeger](#jaeger)
  - [Zipkin](#zipkin)
  - [Prometheus](#prometheus)
  - [OpenTelemetry Collector](#opentelemetry-collector)
  - [Microsserviços de Demonstração](#microsserviços-de-demonstração)
- [Executando o Projeto](#executando-o-projeto)
- [Acessando os Serviços](#acessando-os-serviços)
- [Licença](#licença)

## Pré-requisitos

- Docker
- Docker Compose
- **Go** (necessário para a construção dos microsserviços durante o build)

## Configuração

1. Clone este repositório:

   ```bash
   git clone https://github.com/dellabeneta/tracing-microservices.git
   cd tracing-microservices
   ```

2. Certifique-se de que os arquivos de configuração do Prometheus e do OpenTelemetry Collector estão no lugar:

   - `./.docker/prometheus.yaml`
   - `./.docker/otel-collector-config.yaml`

## Serviços

### Jaeger

- **Imagem**: `jaegertracing/all-in-one:latest` - Aqui talvez você possa travar em uma release específica; seria uma boa prática.
- **Portas**: 
  - `16686:16686` (Jaeger UI)
  - `14268` (Jaeger collector HTTP)
  - `14250` (Jaeger collector gRPC)

### Zipkin

- **Imagem**: `openzipkin/zipkin:latest` - Aqui talvez você possa travar em uma release específica; seria uma boa prática.
- **Portas**:
  - `9411:9411` (Zipkin UI e API)

### Prometheus

- **Imagem**: `prom/prometheus:latest` - - Aqui talvez você possa travar em uma release específica; seria uma boa prática.
- **Portas**: `9090:9090` (Prometheus UI)
- **Configuração**: A configuração do Prometheus é montada a partir de `./.docker/prometheus.yaml`.

### OpenTelemetry Collector

- **Imagem**: `otel/opentelemetry-collector:0.103.0` - Essa versão em especṕifico é requerida. 
- **Portas**:
  - `1888:1888` (extensão pprof)
  - `8888:8888` (métricas Prometheus)
  - `8889:8889` (métricas do Prometheus exporter)
  - `13133:13133` (verificação de integridade)
  - `4317:4317` (OTLP gRPC receiver)
  - `55679:55679` (extensão zPages)

### Microsserviços de Demonstração

Três microsserviços estão incluídos nesta configuração:

1. **goapp**
   - **Porta**: `8080:8080`
   - **Variáveis de Ambiente**: 
     - `TITLE=Microservice Demo 1`
     - `BACKGROUND_COLOR=green`
     - `RESPONSE_TIME=500ms`

2. **goapp2**
   - **Porta**: `8181:8181`
   - **Variáveis de Ambiente**:
     - `TITLE=Microservice Demo 2`
     - `BACKGROUND_COLOR=blue`
     - `RESPONSE_TIME=1000ms`

3. **goapp3**
   - **Porta**: `8282:8282`
   - **Variáveis de Ambiente**:
     - `TITLE=Microservice Demo 3`
     - `BACKGROUND_COLOR=green`
     - `RESPONSE_TIME=1000ms`

Esses microsserviços estão conectados à stack de observabilidade e se comunicam entre si para simular um sistema distribuído.

## Executando o Projeto

Para iniciar toda a stack, basta executar:

```bash
docker compose up -d 
```

Este comando irá construir os microsserviços e iniciar todos os containers definidos no `compose.yml`.

## Acessando os Serviços

- **Jaeger UI**: [http://localhost:16686](http://localhost:16686)
- **Zipkin UI**: [http://localhost:9411](http://localhost:9411)
- **Prometheus UI**: [http://localhost:9090](http://localhost:9090)
- **Microsserviços**:
  - `goapp`: [http://localhost:8080](http://localhost:8080)
  - `goapp2`: [http://localhost:8181](http://localhost:8181)
  - `goapp3`: [http://localhost:8282](http://localhost:8282)

## Licença

Este projeto é licenciado sob a Licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

Lembre-se que você pode efetuar um fork do respositório e ter o projeto dentro do seu próprio Github, uma excelente prática.
