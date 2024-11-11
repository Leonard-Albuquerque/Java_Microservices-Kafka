
# Java Microservices with Spring Boot and Kafka

Este repositório contém um conjunto de microserviços desenvolvidos em Java, utilizando o framework Spring Boot e a plataforma de mensageria Kafka para comunicação assíncrona entre os serviços. Este projeto visa demonstrar a construção de uma arquitetura de microserviços moderna e escalável, com integrações e manipulação de dados de maneira distribuída.

## Estrutura do Projeto

O projeto é composto por três microserviços principais:

1. **Inventory Service**: Gerencia o inventário de produtos, incluindo operações CRUD e sincronização com outros serviços.
2. **Order Service**: Processa pedidos de clientes, incluindo integração com o Inventory Service para validação de estoque e confirmação de pedido.
3. **Payment Service**: Realiza o processamento de pagamentos, com comunicação direta com o Order Service para a conclusão do fluxo de pedidos.

Cada microserviço possui sua própria base de dados, seguindo a prática de separação de dados para maior modularidade e independência.

## Tecnologias Utilizadas

- **Java 18**
- **Spring Boot 3.1.2**: Framework principal para construção de APIs e configuração dos microserviços.
- **Spring Data JPA**: Facilita a integração com bancos de dados relacionais.
- **Kafka**: Utilizado como sistema de mensageria para comunicação entre os microserviços de forma assíncrona.
- **PostgreSQL**: Banco de dados relacional utilizado por cada microserviço para persistência de dados.
- **Docker**: Contêinerização dos serviços para facilitar o deploy e a escalabilidade.
- **Gradle**: Gerenciador de dependências e build automation.

## Configuração e Variáveis de Ambiente

Cada serviço pode ser configurado com variáveis de ambiente para facilitar a integração e a implantação em diferentes ambientes. Abaixo estão os parâmetros configuráveis, com valores padrão fornecidos:

- `DB_HOST`: Endereço do banco de dados (default: `localhost`)
- `DB_PORT`: Porta do banco de dados (default: `5435`)
- `DB_NAME`: Nome do banco de dados específico para cada serviço (exemplo: `inventory-db`)
- `DB_USER`: Usuário do banco de dados (default: `postgres`)
- `DB_PASSWORD`: Senha do banco de dados (default: `postgres`)

### Exemplo de Configuração (`application.yml`)

```yaml
server:
  port: 8092

spring:
  datasource:
    driver-class-name: org.postgresql.Driver
    url: jdbc:postgresql://${DB_HOST:localhost}:${DB_PORT:5435}/${DB_NAME:inventory-db}
    username: ${DB_USER:postgres}
    password: ${DB_PASSWORD:postgres}

  jpa:
    hibernate:
      ddl-auto: create-drop
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
```

## Executando o Projeto

### Pré-requisitos

- **Docker**: Certifique-se de que o Docker está instalado e em execução.
- **Kafka**: Um broker Kafka deve estar configurado para comunicação entre os microserviços.

### Passo a Passo

1. **Clone o repositório**:
   ```bash
   git clone https://github.com/seu-usuario/seu-repositorio.git
   ```

2. **Configuração do Ambiente**: Certifique-se de configurar as variáveis de ambiente adequadas para o PostgreSQL e o Kafka.

3. **Build e Deploy**: Utilize o Docker Compose para subir todos os serviços e suas dependências.
   ```bash
   docker-compose up --build
   ```

4. **Acessando os Serviços**: Cada microserviço estará disponível em uma porta específica definida no `docker-compose.yml`. Por exemplo:
   - Inventory Service: `http://localhost:8092`
   - Order Service: `http://localhost:8093`
   - Payment Service: `http://localhost:8094`

## Estrutura de Comunicação

Os microserviços se comunicam de forma assíncrona via Kafka, o que garante que as mensagens entre eles sejam entregues de forma rápida e escalável. O fluxo de mensagens permite que o sistema processe pedidos e confirme pagamentos em diferentes etapas, garantindo alta disponibilidade e consistência eventual dos dados.

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues e pull requests para melhorar o projeto ou adicionar novas funcionalidades.

