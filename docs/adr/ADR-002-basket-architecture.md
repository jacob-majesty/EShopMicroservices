**ADR-002: Basket Microservice Architecture**  

### **1. Status**  
✅ **Aceito**  

### **2. Contexto**  
Microsserviço para gerenciamento de carrinho de compras (Basket) com:  
- Alta performance em operações de leitura (Redis Cache).  
- Persistência transacional com PostgreSQL (Marten como Document DB).  
- Arquitetura modular para evolução contínua.  

### **3. Decisão**  
- **Arquitetura**: Vertical Slice + CQRS (MediatR).  
- **Banco de Dados**:  
  - **Marten** (PostgreSQL como Document DB para persistência principal).  
  - **Redis** (cache distribuído para alta performance em leituras).  
- **Tecnologias**:  
  - ASP.NET Core Minimal APIs (.NET 8 + C# 12).  
  - Carter para definição de endpoints.  
  - FluentValidation para validações.  
- **Padrões**:  
  - Repository Pattern (abstração de dados).  
  - Dependency Injection (nativo do ASP.NET Core).  
- **Containerização**:  
  - **Portas**:  
    - Local: `5001–5051` (dev).  
    - Docker Host: `6001–6061`.  
    - Container: `8080–8081`.  

### **4. Alternativas Consideradas**  
1. **Entity Framework Core**: Menos adequado para modelo de documentos (Marten é mais eficiente para JSONB).  
2. **MongoDB**: Oferece desempenho, mas sem transações ACID robustas (PostgreSQL + Marten garante consistência).  

### **5. Consequências**  
- ✅ **Prós**:  
  - Alta escalabilidade (Redis + PostgreSQL).  
  - Código organizado por feature (Vertical Slice).  
  - Desempenho otimizado para operações de carrinho.  
- ❌ **Contras**:  
  - Complexidade de configuração (Marten + Redis).  

### **6. Implementação**  
- **Endpoints REST**:  
  ```plaintext
  GET    /basket/{userName}     → Obtém carrinho por usuário.  
  POST   /basket/{userName}     → Adiciona/atualiza carrinho.  
  DELETE /basket/{userName}     → Remove carrinho.  
  POST   /basket/checkout       → Finaliza compra.  
  ```  
- **Estrutura de Dados**:  
  - Dados persistidos como documentos JSON no PostgreSQL (Marten).  
  - Cache em Redis para consultas frequentes.  
- **Validações**: FluentValidation integrado ao pipeline do MediatR.  
