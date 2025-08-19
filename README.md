# EShop - Microserviços em .NET 8

![.NET](https://img.shields.io/badge/.NET-8-blue)
![Docker](https://img.shields.io/badge/Docker-✓-blue)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-✓-orange)
![gRPC](https://img.shields.io/badge/gRPC-✓-brightgreen)

O EShop é uma plataforma de e-commerce construída com arquitetura de microserviços utilizando .NET 8 e diversas tecnologias modernas.

<img width="1476" height="746" alt="image" src="https://github.com/user-attachments/assets/1f1e199c-cdd7-4408-9a43-90961feb4daa" />


## 📌 Visão Geral

Este projeto demonstra a implementação de uma arquitetura de microserviços para um sistema de e-commerce, com os seguintes componentes:

- **API Gateway** (YARP)
- **Serviço de Catálogo**
- **Serviço de Carrinho**
- **Serviço de Pedidos**
- **Serviço de Pagamentos**
- **Serviço de Clientes**

## 🛠 Stack Tecnológica

- **.NET 8** - Plataforma principal de desenvolvimento
- **ASP.NET Web API** - Para construção dos microserviços
- **Docker** - Containerização dos serviços
- **RabbitMQ** - Mensageria entre serviços
- **MassTransit** - Abstração para RabbitMQ
- **gRPC** - Comunicação entre serviços
- **Yarp Gateway** - API Gateway
- **Redis** - Cache distribuído
- **SQL Server** - Banco de dados relacional

## 📐 Diagrama e Estrutura do Projeto

```
EShopMicroservices/
├── 📁 src/
│   ├── 📁 ApiGateways/          # Yarp Gateway
│   ├── 📁 Basket/               # Serviço de Carrinho
│   ├── 📁 Catalog/              # Serviço de Catálogo
│   ├── 📁 Customers/            # Serviço de Clientes
│   ├── 📁 Orders/               # Serviço de Pedidos
│   └── 📁 Payments/             # Serviço de Pagamentos
├── 📁 docker-compose.yml        # Configuração Docker
└── 📁 README.md                 # Documentação
```

### ADR (Architectural Decision Record): Registro de Decisão Arquitetural
- [ADR-001: Catalog Architecture](ADR-001-catalog-architecture.md)  
- [ADR-002: Basket Architecture](ADR-002-basket-architecture.md)  

### Diagrama de Arquitetura

```
[Client] ←HTTP→ [Yarp Gateway] ←HTTP/gRPC→ [Microservices]
                  ↑
                  ↓
           [Service Discovery]
                  ↑
                  ↓
[Microservices] ↔ [RabbitMQ] ↔ [Microservices]
    ↑                ↑
    |                |
[SQL Server]     [Redis Cache]
```

## 🚀 Como Rodar o Projeto

### Pré-requisitos

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Passos para Execução

1. **Clone o repositório**:
   ```bash
   git clone https://github.com/jacob-majesty/EShopMicroservices.git
   cd EShopMicroservices
   ```

2. **Suba os containers**:
   ```bash
   docker-compose up -d
   ```

   Isso irá subir:
   - SQL Server
   - RabbitMQ
   - Redis
   - Todos os microserviços
   - API Gateway

3. **Acesse os serviços**:

   - API Gateway: `http://localhost:5000`
   - RabbitMQ Management: `http://localhost:15672` (guest/guest)
   - Redis Commander: `http://localhost:8081` (se configurado)

4. **Para parar os serviços**:
   ```bash
   docker-compose down
   ```

## 🔍 Testando os Endpoints

Você pode testar os endpoints usando o Swagger UI de cada serviço:

- Catálogo: `http://localhost:5001/swagger`
- Carrinho: `http://localhost:5002/swagger`
- Pedidos: `http://localhost:5003/swagger`

Ou através do API Gateway em `http://localhost:5000/swagger`

## 🤝 Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.

## 📄 Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.
