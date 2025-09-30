# Atividade Prática: Desenvolvimento de API REST com NestJS

## Descrição da Atividade
Esta atividade prática tem como objetivo consolidar os conhecimentos adquiridos no [tutorial introdutório de API REST e NestJS](https://github.com/infoweb-pos/api-nest-notas-01-introducao) através da implementação de um CRUD completo para gerenciamento de tarefas.

## Objetivos de Aprendizado
Ao final desta atividade, o aluno será capaz de:
- Configurar um projeto NestJS do zero
- Implementar um CRUD completo com TypeORM
- Configurar banco de dados SQLite3
- Aplicar validações com Class Validator
- Testar endpoints de uma API REST
- Implementar boas práticas de desenvolvimento com NestJS

# Checklist de Progresso da Atividade

Use este checklist para acompanhar seu progresso durante a implementação da API de tarefas.

## ✅ Pré-requisitos e Configuração

### Verificação do Ambiente
- [x] Node.js (v18+) instalado e funcionando
- [x] npm instalado e funcionando
- [x] Git instalado e configurado
- [x] Editor de código (VS Code recomendado) configurado
- [x] Cliente REST (Postman/Insomnia/Thunder Client) instalado

### Configuração Inicial
- [x] Fork do repositório tutorial realizado
- [x] Repositório clonado localmente
- [x] NestJS CLI instalado globalmente (`npm install -g @nestjs/cli`)
- [x] Projeto NestJS criado (`nest new tasks-api`)
- [x] Dependências instaladas (TypeORM, SQLite, class-validator, etc.)

## 🗂️ Estrutura do Projeto

### Criação de Diretórios
- [x] Diretório `src/tasks` criado
- [x] Diretório `src/tasks/dto` criado
- [x] Estrutura de pastas organizada conforme especificação

### Arquivos Base
- [x] `app.module.ts` configurado com TypeORM
- [x] `main.ts` configurado com CORS e ValidationPipe
- [x] Configuração do banco SQLite implementada

## 📊 Implementação da Entity

### Task Entity (src/tasks/task.entity.ts)
- [x] Classe `Task` criada com decorator `@Entity()`
- [x] Campo `id` com `@PrimaryGeneratedColumn()`
- [x] Campo `title` com `@Column()`
- [x] Campo `description` com `@Column()`
- [x] Campo `status` com enum `TaskStatus` e configuração adequada
- [x] Campos `createdAt` e `updatedAt` com decorators de timestamp
- [x] Enum `TaskStatus` definido corretamente (aberto, fazendo, finalizado)

## 📝 Implementação dos DTOs

### CreateTaskDto (src/tasks/dto/create-task.dto.ts)
- [x] Classe `CreateTaskDto` criada
- [x] Validação `@IsString()` e `@IsNotEmpty()` no campo `title`
- [x] Validação `@IsString()` e `@IsNotEmpty()` no campo `description`
- [x] Validação `@IsEnum()` e `@IsOptional()` no campo `status`

### UpdateTaskDto (src/tasks/dto/update-task.dto.ts)
- [x] Classe `UpdateTaskDto` criada
- [x] Todos os campos opcionais com `@IsOptional()`
- [x] Validações adequadas mantidas para cada campo

## 🔧 Implementação do Service

### TasksService (src/tasks/tasks.service.ts)
- [x] Classe `TasksService` com decorator `@Injectable()`
- [x] Injeção do repositório com `@InjectRepository(Task)`
- [x] Método `findAll()` implementado
- [x] Método `findOne(id)` implementado com tratamento de erro 404
- [x] Método `create(createTaskDto)` implementado
- [x] Método `update(id, updateTaskDto)` implementado
- [x] Método `remove(id)` implementado
- [x] Tratamento adequado de erros em todos os métodos

## 🎮 Implementação do Controller

### TasksController (src/tasks/tasks.controller.ts)
- [x] Classe `TasksController` com decorator `@Controller('tasks')`
- [x] Injeção do service no construtor
- [x] Endpoint `GET /tasks` com decorator `@Get()`
- [x] Endpoint `GET /tasks/:id` com `@Get(':id')` e `ParseIntPipe`
- [x] Endpoint `POST /tasks` com `@Post()` e `@Body()`
- [x] Endpoint `PUT /tasks/:id` com `@Put(':id')` e validações
- [x] Endpoint `DELETE /tasks/:id` com `@Delete(':id')`
- [x] Status codes HTTP adequados configurados

## 📦 Configuração do Module

### TasksModule (src/tasks/tasks.module.ts)
- [x] Classe `TasksModule` com decorator `@Module()`
- [x] Importação do `TypeOrmModule.forFeature([Task])`
- [x] Controller adicionado ao array `controllers`
- [x] Service adicionado ao array `providers`
- [x] Módulo importado no `AppModule`

## 🚀 Execução e Testes

### Inicialização da Aplicação
- [x] Aplicação inicia sem erros (`npm run start:dev`)
- [x] Banco de dados SQLite criado automaticamente (tasks.db)
- [x] Console mostra "API rodando em http://localhost:3000"
- [x] Hot reload funcionando adequadamente

### Teste dos Endpoints - GET
- [x] `GET /tasks` retorna array vazio inicialmente (200 OK)
- [x] `GET /tasks/1` retorna 404 Not Found quando não há tarefas

### Teste dos Endpoints - POST
- [x] `POST /tasks` com dados válidos cria tarefa (201 Created)
- [x] `POST /tasks` retorna tarefa criada com ID, timestamps
- [x] `POST /tasks` com título vazio retorna 400 Bad Request
- [x] `POST /tasks` com status inválido retorna 400 Bad Request

### Teste dos Endpoints - GET com dados
- [x] `GET /tasks` retorna array com tarefa(s) criada(s)
- [x] `GET /tasks/1` retorna tarefa específica (200 OK)
- [x] `GET /tasks/999` retorna 404 Not Found

### Teste dos Endpoints - PUT
- [x] `PUT /tasks/1` com dados válidos atualiza tarefa (200 OK)
- [x] `PUT /tasks/1` retorna tarefa atualizada
- [x] `PUT /tasks/999` retorna 404 Not Found
- [x] Atualização parcial funciona (apenas alguns campos)

### Teste dos Endpoints - DELETE
- [x] `DELETE /tasks/1` remove tarefa (204 No Content)
- [x] `DELETE /tasks/999` retorna 404 Not Found
- [x] Tarefa removida não aparece mais em `GET /tasks`

## 📋 Testes de Validação

### Validação de Entrada
- [x] Campos obrigatórios (title, description) são validados
- [x] Status aceita apenas valores válidos (aberto, fazendo, finalizado)
- [x] Campos extras são ignorados (whitelist ativa)
- [x] Mensagens de erro são claras e específicas

### Validação de IDs
- [x] IDs não numéricos retornam 400 Bad Request
- [x] IDs decimais são tratados adequadamente
- [x] IDs negativos são tratados adequadamente

---

## ✅ Status: Atividade Concluída com Sucesso!

Todos os requisitos da atividade foram implementados e testados. A API REST para gerenciamento de tarefas está funcionando perfeitamente com todas as funcionalidades de CRUD, validações e tratamento de erros.