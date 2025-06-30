## Estrutura do Projeto

O projeto foi construido utilizando a linguagem Go e segue uma estrutura modularizada, facilitando a manutenção e escalabilidade.

Abaixo está a visão de cada módulo e suas responsabilidades:

- **`/internal`**: Contém a lógica de negócio principal do sistema, incluindo serviços, repositórios e modelos.

        internal

- **`/internal/bootstrap`**: Responsável pela inicialização do sistema, incluindo configuração de ambiente, conexão com o banco de dados e outras dependências.

        ├── internal
            ├── bootstrap
                ├── app.go
                ├── controllers.go
                ├── database.go
                ├── repositories.go
                ├── router.go
                └── usecases.go

- **`/internal/config`**: Contém as configurações do sistema, como variáveis de ambiente e parâmetros de configuração.

        ├── internal
            ├── config
                ├── databases
                    ├── mongodb.go
                └── routes
                    ├── telemetry_router.go

- **`/internal/controllers`**: Define os controladores que gerenciam as requisições HTTP e interagem com os serviços.

        ├── internal
            ├── controllers
                ├── commonController
                    ├── photo_controller.go
                    └── photo_controller_test.go
                └── telemetriesControllers
                    ├── gps_controller.go
                    ├── gps_controller_test.go
                    ├── gyroscope_controller.go
                    ├── gyroscope_controller_test.go
                    └── temeletries_test_helpers.go

- **`/internal/dtos`**: Contém os Data Transfer Objects (DTOs) utilizados para transferir dados entre as camadas do sistema.

        ├── internal
            ├── dtos
                └── telemetriesDtos
                    ├── gps_dto.go
                    ├── gyroscope_dto.go

- **`/internal/enums`**: Define os enums utilizados no sistema, como tipos de telemetrias.

        ├── internal
            ├── enums
                └── photo_entity_enum.go

- **`/internal/infra`**: Contém a infraestrutura do sistema, incluindo conexões com serviços externos e implementações de repositórios.

        ├── internal
            ├── infra
                ├── mongodb
                    ├── commonMongoRepositories
                        └── photo_repository.go
                    └── telemetriesMongoRepositories
                        ├── gps_repository.go
                        └── gyroscope_repository.go
                ├── storage
                    └── local_file_storage.go

- **`/internal/interfaces`**: Define as interfaces que os repositórios e serviços devem implementar, promovendo a inversão de dependência.

        ├── internal
            └── interfaces
                └── file_storage_interface.go   

- **`/internal/models`**: Contém os modelos de dados utilizados no sistema, como entidades e objetos de valor.

        ├── internal
            ├── models
                ├── commonModels
                    └── photo_model.go
                └── telemetriesModels
                    ├── gps_model.go
                    └── gyroscope_model.go

- **`/internal/repositories`**: Contém as interfaces dos repositórios, que definem as operações de acesso a dados.

        ├── internal
            ├── repositories
                ├── commonRepositories
                    └── photo_repository.go
                └── telemetriesRepositories
                    ├── gps_repository.go
                    └── gyroscope_repository.go

- **`/internal/usecases`**: Contém os casos de uso do sistema, que encapsulam a lógica de negócio e orquestram as interações entre os serviços e repositórios.

        ├── internal
            ├── usecases
                ├── commonUsecases
                    └── photo_usecase.go
                └── telemetriesUsecases
                    ├── gps_usecase.go
                    └── gyroscope_usecase.go

- **`/internal/validators`**: Contém os validadores utilizados para validar os dados de entrada, como DTOs e modelos.

        ├── internal
            ├── validators
                └── json_validator.go

- **`/tests`**: Contém os testes do sistema, incluindo testes de integração.

        ├── tests
            ├── integration
                ├── gps_test.go
                ├── gyroscope_test.go
                ├── helpers_test.go
                ├── photo_test.go
                └── setup_test.go

## 📦 Execução do Projeto

Para executar o projeto, você precisa ter o Go instalado em sua máquina. Siga os passos abaixo:

1. **Clone o repositório:**

   ```bash
   git clone
   ```

2. **Navegue até o diretório do projeto:**

   ```bash
   cd v3-test
   ```

3. **Crie um arquivo `.env` a partir do template:**

   ```bash
   cp env-template.env .env
   ```

4. **Execute o comando para rodar o docker-compose:**

   ```bash
   docker compose -f docker-compose.dev.yml up --build 
   ```

## 🧪 Testes

Este projeto possui dois tipos de testes:

- ✅ **Testes unitários** (`*_test.go` dentro de `internal/`)
- ✅ **Testes de integração** (`*_test.go` dentro de `tests/integration/`)

> **Pré-requisitos:** Para os testes de integração, é necessário ter o MongoDB rodando localmente ou via Docker (veja abaixo).

---

### ▶️ Executar todos os testes (unitários + integração)

```bash
./test.sh 
```

---

### 🧪 Executar apenas os testes unitários

```bash
go test -v ./internal/...
```

---

### 🔌 Executar apenas os testes de integração

```bash
go test -v ./tests/integration/...
```

> ⚠️ Lembre-se de que os testes de integração requerem que o Mongo esteja rodando. Para facilitar, utilize o `docker-compose.dev.test.yml`:

```bash
docker-compose -f docker-compose.dev.test.yml up -d mongo
```

---

### 🧹 Parar e remover serviços do Docker (testes)

```bash
docker-compose -f docker-compose.dev.test.yml down
```
