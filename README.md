<h1>
    <a href="https://www.dio.me/">
     <img width="40px" src="https://hermes.digitalinnovation.one/assets/diome/logo-minimized.png"></a>
    <span> Curso oeferecido pela DIO XP Inc. - Full Stack Developer</span>
</h1>

> ## 📕 O repositório tem como objetivo armazenar resumos e o conteúdo passado em aula sobre ASP.NET Minimals APIs com C#.

## 🚀 ``Trabalhando com ASP.NET Minimals APIs``

#### 📍 O que precisa ter instalado para começar:
* ``dotnet --version``
* ``mysql --version``
> [Site do MySQL](https://dev.mysql.com/downloads/mysql/)

> Se conectar ao mysql: mysql -u root -p

#### 📍 Criando projeto e entendendo o código boilerplate:

**Criando projeto a partir do terminal no Windows:**
* ``dotnet new web -o minimal-api``: comando para criar um novo projeto
* ``cd minimal-api``: Entrar na pasta do projeto
* ``code .``: abrir projeto no VS Code

#### 📍 Definição do que teremos no projeto:

* CRUD do veículo
* Autenticação do administrador e regra de administrador

#### 📍 Criando uma rota login para validação em memória:

* ``dotnet run`` ver aplicação no localhost
> **Link:** http://localhost:5044/
* ``dotnet watch run``: ver aplicação em tempo real
* Também podemos rodar pelo debuger do VS Code

~~~~C#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Olá pessoal");

// Login e senha
app.MapPost("/login", (LoginDTO loginDTO) =>{
    if(loginDTO.Email == "adm@teste.com" && loginDTO.Senha == "123456")
        return Results.Ok("Login com sucesso");
    else
        return Results.Unauthorized();
});
app.Run();

//LoginDTO (Data Transfer Object)
public class LoginDTO
{
    public string Email {get;set;} = default;
    public string Senha {get;set;} = default;
}
~~~~

* Executar o debugger do VS Code
* Acessar o site postman -> baixar o Postman Agent
> Link: [Postman](https://web.postman.co/workspace/88c8b9a9-cad2-4ac3-8210-880855cf4897/request/create?requestId=e4122fde-ea7a-4a4f-bf6b-dd00f7f5735e)
* Inserir JSON com email e senha
* Enviar
> JSON:
~~~~json
{
    "email": "adm@teste.com",
    "senha": "123456"
}
~~~~

* Isso faz com que os dados de login da API sejam preenchidos e inicia uma requisição, depois é só continuar debug e checar a resposta no Postman.

#### 📍Configurando o projeto com Entity Framework e tabela de administradores:

* Acessar o site do [Nuget⬇](https://www.nuget.org/)
* Pesquisar por **Entity Framework**
> ⬇️ Microsoft.EntityFrameworkCore<br>
> ⬇️ Microsoft.EntityFrameworkCore.Design<br> 
> ⬇️ Microsoft.EntityFrameworkCore.Tools<br>
> ⬇️ Pomelo.EntityFrameworkCore.MySql<br>
* Copiar e colar os códigos no terminal -> Enter

**Usaremos os tipos de arquitetura**
* Clean architecture
* oninion architecture

**Organização das patas**

* /Infraestrutura/: conexão com banco de dados (Entity Framework) que irá incluir nosso contexto.
* /Dominio/: regras de negócio.
* /Servicos/.

* Dominio/DTOs/: criamos um arquivo LoginDTOs.cs:
~~~~c#
namespace MinimalApi.DTOs;

//LoginDTO (Data Transfer Object)
public class LoginDTO
{
    public string Email {get;set;} = default;
    public string Senha {get;set;} = default;
}
~~~~

* Atualizamos o Program.cs:
~~~~c#
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Olá pessoal");

// Login e senha
app.MapPost("/login", (MinimalApi.DTOs.LoginDTO loginDTO) =>{ // ~
    if(loginDTO.Email == "adm@teste.com" && loginDTO.Senha == "123456")
        return Results.Ok("Login com sucesso");
    else
        return Results.Unauthorized();
});
app.Run();

// -
~~~~

* Podemos acessar o site [Gitignore](https://www.toptal.com/developers/gitignore/) para inserir os arquivos que desejamos incluir no .gitignore.
> Inserimos: windows, linux, macos, dotnetcore, visual studio code.