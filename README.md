# 📘 SkillUp API

A **SkillUpPlus API** é uma aplicação backend desenvolvida em **.NET 8**, projetada para dar suporte a um aplicativo educacional que oferece trilhas de aprendizado, progresso do usuário, avaliações de habilidades e recomendações inteligentes.

Esta API segue uma arquitetura limpa e escalável, utiliza **Entity Framework Core**, autenticação **JWT**, e está pronta para ser integrada com qualquer front-end (React Native, Web, etc).

---

## 🚀 Tecnologias Utilizadas

* **.NET 8**
* **C#**
* **ASP.NET Core Web API**
* **Entity Framework Core (MySQL/MariaDB)**
* **JWT (JSON Web Token)**
* **Swagger / Swashbuckle**
* **Dependency Injection**
* **Clean architecture-inspired structure**

---

## 📂 Estrutura do Projeto

```
SkillUpPlus/
├── Controllers/
│   ├── AppUserController.cs
│   ├── SkillAssessmentController.cs
│   ├── UserProgressController.cs
│   └── AuthController.cs
│
├── Data/
│   ├── SkillUpPlusDbContext.cs
│
├── Dtos/
│   ├── AppUserDto.cs
│   ├── SkillAssessmentItemDto.cs
│   ├── UserProgressDto.cs
│
├── Models/
│   ├── AppUser.cs
│   ├── SkillAssessmentItem.cs
│   ├── AppUserProgress.cs
│   ├── LearningPath.cs
│
├── Services/
│   ├── JwtService.cs
│
├── Utils/
│   ├── PasswordUtils.cs
│
├── Program.cs
└── appsettings.json
```

---

## 🔐 Autenticação (JWT)

A API utiliza **autenticação JWT** para garantir segurança e estatelessness.

### Fluxo:

1. O usuário envia email/senha para `/api/v1/auth/login`
2. A API valida as credenciais
3. Um token JWT é retornado
4. O front-end deve enviar:

   ```
   Authorization: Bearer <token_aqui>
   ```
5. Endpoints com `[Authorize]` somente respondem com token válido

---

## 📌 Endpoints Principais

### 👤 Usuários (`/api/v1/AppUser`)

* **GET** `/api/v1/AppUser/{id}`
* **POST** `/api/v1/AppUser` — cria novo usuário
* **Senha é automaticamente hasheada**

---

### 📊 Progresso do Usuário (`/api/v1/UserProgress`)

* **PUT** para atualizar progresso
* **GET** para consultar progresso
* Utiliza DTOs para evitar overfetching

---

### 🧠 Avaliação de Habilidades (`/api/v1/SkillAssessment`)

* Criar item de avaliação
* Listar avaliação do usuário
* Deletar avaliação por AppUserId
* Retornar apenas os campos seguros (DTO)

---

### 🔑 Login e Token (`/api/v1/Auth/login`)

* Autentica o usuário
* Retorna JWT assinado com chave segura de 32 bytes

---

## 🛠️ Como Rodar o Projeto

### 1️⃣ Pré-requisitos

* .NET 8 instalado
* MySQL ou MariaDB
* Visual Studio ou VS Code
* Postman / Swagger para testes

### 2️⃣ Configurar banco no `appsettings.json`

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=...;Port=3306;Database=...;User=...;Password=..."
}
```

### 3️⃣ Configurar JWT

```json
"Jwt": {
  "Key": "chave_super_secreta_de_32_bytes",
  "Issuer": "http://localhost:5133/",
  "Audience": "http://localhost:5133/",
  "ExpiresInMinutes": 30
}
```

### 4️⃣ Aplicar Migrações

```
dotnet ef database update
```

### 5️⃣ Executar API

```
dotnet run
```

A API inicia em:

```
http://localhost:5133
```

Swagger em:

```
http://localhost:5133/swagger
```

---

## 🧱 Arquitetura

A API segue princípios de:

* Baixo acoplamento entre camadas
* Controllers → Services → Data
* DTOs para retornar apenas dados necessários
* Autenticação e autorização usando middleware
* Stateless server usando JWT

<img width="9071" height="3642" alt="image" src="https://github.com/user-attachments/assets/544b0037-c5de-4dca-a12d-aad890b06872" />
---

## 🛡️ Segurança

✔ Senhas são hasheadas usando BCrypt
✔ JWT com chave de 32 bytes
✔ Token valida issuer, audience e assinatura
✔ ClockSkew = 0 (token expira exatamente no tempo indicado)
✔ CORS liberado somente quando necessário

---

## 📌 Próximos Passos da API

* Implementar refresh token
* Criar camadas de service separadas para cada controller
* Versionamento mais avançado
* Adicionar testes unitários com xUnit
* Implementar logs estruturados

---

## 📄 Licença

Distribuído sob a licença MIT.
Sinta-se livre para usar no seu projeto!

