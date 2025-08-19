
**ADR-001: Catalog Microservice Architecture**  

### **1. Status**  
✅ **Aceito**  

### **2. Contexto**  
Microsserviço para gerenciamento de catálogo de produtos com:  
- **Escalabilidade** (Docker + PostgreSQL).  
- **Separação clara de responsabilidades** (Vertical Slice + CQRS).  
- **Integrações externas** (Client via REST).  

### **3. Decisão**  
- **Arquitetura Interna**:  
  - **Vertical Slice** (por feature) + **CQRS** (MediatR).  
  - **Cross-cutting**:  
    - Validação (FluentValidation).  
    - Logging/Tratamento global de erros (ASP.NET Core).  
    - Health Checks (PostgreSQL).  
    - Paginação (GetProducts).  
- **Banco de Dados**: PostgreSQL (Marten para seeding).  
- **Containerização**:  
  - **Portas**:  
    - Local: `5000–5050` (dev).  
    - Docker Host: `6000–6060`.  
    - Container: `8080–8081`.  
  - **Orquestração**: Docker-compose.  

### **4. Alternativas Consideradas**  
1. **MongoDB**: Não atendia a requisitos de transações complexas.  
2. **SQL Server**: Overhead de licença.  

### **5. Consequências**  
- ✅ **Prós**:  
  - Isolamento de features (Vertical Slice).  
  - Desempenho (PostgreSQL + CQRS).  
- ❌ **Contras**:  
  - Curva de aprendizado (MediatR/Marten).  

### **6. Implementação**  
- **Endpoints REST (Catalog.API)**:  
  ```plaintext
  GET    /products              → Lista todos.  
  GET    /products/{id}         → Detalhes.  
  GET    /products/category     → Filtro por categoria.  
  POST   /products              → Cria novo.  
  PUT    /products/{id}         → Atualiza.  
  DELETE /products/{id}         → Remove.  
  ```  
- **Pilha**:  
  - ASP.NET Core + PostgreSQL.  
  - Docker (compose para orquestração).  


---  
