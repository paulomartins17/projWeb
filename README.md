# projWeb

Projeto de microsserviços em Java com Spring Boot e MongoDB, desenvolvido para a disciplina de Desenvolvimento Web — 7º semestre.

## Módulos

### projUsuario (porta 8081)
Microsserviço responsável pelo cadastro e consulta de usuários e endereços no MongoDB.

**Endpoints:**
| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/usuario` | Cadastra um usuário (salva endereço automaticamente) |
| GET | `/usuario` | Lista todos os usuários |
| POST | `/endereco` | Cadastra um endereço |
| GET | `/endereco` | Lista todos os endereços |

---

### projPlanilha (porta 8084)
Microsserviço responsável pelo gerenciamento de planilhas e comparações entre elas. Consome o `projUsuario` via REST.

**Endpoints:**
| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/planilha` | Cadastra uma planilha |
| GET | `/planilha` | Lista todas as planilhas |
| POST | `/comparacaoplanilha` | Registra uma comparação entre planilhas |
| GET | `/comparacaoplanilha` | Lista todas as comparações |
| POST | `/scorecomparacao` | Cadastra um score de comparação |
| GET | `/scorecomparacao` | Lista todos os scores |
| POST | `/historicocomparacaoservice` | Registra um histórico de comparação |
| GET | `/historicocomparacaoservice` | Lista todo o histórico |
| POST | `/usuario_planilha` | Proxy para cadastro de usuário via projUsuario |
| GET | `/usuario_planilha` | Proxy para listagem de usuários via projUsuario |

---

### projImportPlanilha
Módulo utilitário que lê um arquivo Excel (`.xlsx`) e importa os usuários para o `projUsuario` via REST.

**Endpoints:**
| Método | Rota | Descrição |
|--------|------|-----------|
| POST | `/import_planilha` | Recebe um arquivo Excel e importa os usuários |

**Formato esperado do Excel** (colunas na ordem):

| 0 - nome | 1 - telefone | 2 - logradouro | 3 - cidade | 4 - numero | 5 - cep | 6 - bairro |
|----------|-------------|----------------|------------|------------|---------|------------|

---

## Tecnologias

- Java 17
- Spring Boot 2.7.18
- Spring Data MongoDB
- Spring Web (RestTemplate)
- Apache POI 5.2.5 (leitura de Excel)
- springdoc-openapi (Swagger UI)
- Lombok

## Como rodar

1. Suba uma instância do MongoDB localmente (porta padrão `27017`)
2. Inicie os módulos na seguinte ordem:
   ```
   projUsuario      → porta 8081
   projPlanilha     → porta 8084
   projImportPlanilha → porta à sua escolha
   ```
3. Acesse o Swagger UI em `http://localhost:{porta}/swagger-ui/index.html`
