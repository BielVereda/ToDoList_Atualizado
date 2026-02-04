# 📋 ToDoList_Atualizado

Este projeto é uma aplicação **Spring Boot** que implementa um sistema de gerenciamento de usuários e tarefas (**CRUD completo**) com relacionamento **1:N (Um-para-Muitos)** utilizando JPA/Hibernate.

---

## 🚀 Funcionalidades

### Usuário
- Criar usuário
- Listar usuários
- Buscar usuário por ID
- Deletar usuário
- Associar tarefas a um usuário

### Tarefa
- Criar tarefa vinculada a um usuário
- Listar tarefas de um usuário específico
- Atualizar tarefa
- Deletar tarefa

---

## 🔗 Relacionamento 1:N

- **Um Usuário pode ter várias Tarefas**  
- **Uma Tarefa pertence a apenas um Usuário**  
- **Não deve existir tarefa sem usuário associado**  

### Modelagem esperada

**Usuário**
- `id`
- `nome`
- `email`
- `password`
- `tarefas` (lista de tarefas)

**Tarefa**
- `id`
- `titulo`
- `descricao`
- `status`
- `beginDate`
- `endDate`
- `usuario` (referência ao usuário)

👉 A chave estrangeira (`user_id`) fica na tabela **task**.

---

## ⚙️ Configuração do Banco de Dados

No arquivo `application.properties`:

```properties
spring.application.name=ToDo
spring.datasource.url=jdbc:mysql://localhost:3306/ToDoList?useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=rootroot
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

server.port=8080

🌐 Endpoints
Usuários

    POST /usuarios → Criar usuário

    GET /usuarios → Listar usuários

    GET /usuarios/{id} → Buscar usuário por ID

    DELETE /usuarios/{id} → Deletar usuário

    POST /usuarios/{id}/tarefas → Criar tarefa vinculada a um usuário

    GET /usuarios/{id}/tarefas → Listar tarefas de um usuário específico

Tarefas

    POST /tarefas → Criar tarefa (sem vínculo direto, usado apenas se necessário)

    GET /tarefas → Listar todas as tarefas

    GET /tarefas/{id} → Buscar tarefa por ID

    PUT /tarefas/{id} → Atualizar tarefa

    DELETE /tarefas/{id} → Deletar tarefa

📬 Exemplos de Requisições (Postman/Insomnia)
Criar Usuário
http

POST /usuarios
Content-Type: application/json

{
  "name": "Gabriel",
  "email": "gabriel@email.com",
  "password": "123456"
}

Criar Tarefa vinculada a um Usuário
http

POST /usuarios/1/tarefas
Content-Type: application/json

{
  "name": "Estudar Spring Boot",
  "description": "Finalizar projeto To-Do List",
  "status": "PENDING",
  "beginDate": "2026-02-04",
  "endDate": "2026-02-10"
}

Listar Tarefas de um Usuário
http

GET /usuarios/1/tarefas

Atualizar Tarefa
http

PUT /tarefas/1
Content-Type: application/json

{
  "name": "Estudar Spring Boot",
  "description": "Finalizar projeto com relacionamento 1:N",
  "status": "DONE",
  "beginDate": "2026-02-04",
  "endDate": "2026-02-10"
}

Deletar Tarefa
http

DELETE /tarefas/1

🧪 Testes esperados

    Criar um usuário com várias tarefas.

    Listar tarefas de um usuário específico.

    Atualizar uma tarefa existente.

    Deletar uma tarefa.

    Erro ao tentar criar tarefa sem usuário → deve retornar Usuário não encontrado.
