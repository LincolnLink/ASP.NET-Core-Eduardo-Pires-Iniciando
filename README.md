# ASP.NET-Core-Eduardo-Pires-Iniciando
### ASP.NET-Core-Eduardo-Pires-Iniciando


# Comandos basicos do DotNet

 - Comando para criar uma solution!

  <blockquete>
    dotnet new sln --name CSharpBasico
  </blockquete>

 - Comando que lista opções de projetos!

  <blockquete>
    dotnet new
  </blockquete>

 - Comando para criar um projeto, com uma pasta!

  <blockquete>
    dotnet new console -n HelloWorld -o helloWorld
  </blockquete>

  -n: nome do projeto console!
  -o: nome da pasta!

 - Comando que Vincula um projeto a uma solução existente

  <blockquete>
    dotnet sln add 'nomeDoProjeto'
  </blockquete>

 - Comando que limpando a aplicação

  <blockquete>
    dotnet clean
  <blockquete>

 - Comando que restalra a aplicação

  <blockquete>
    dotnet restore
  <blockquete>

 - Comando para Buildar a aplicação

  <blockquete>
    dotnet build
  <blockquete>

 - Comando que Executa um projeto

  <blockquete>
    dotnet run
  <blockquete>

 - Comando que Abre o codigo no VS code

  <blockquete>
    code .
  <blockquete>
  
 - Comando que criando uma pasta

  <blockquete>
    md "nome da pagina"
  <blockquete>

# Definindo SDK

### Se define no arquivo Global!

# Projeto MVC, 

### Arquivo csproj, escrito em XML

  - <Project Sdk="Microsoft.NET.Sdk.Web"> : SDK que informa uma versão do .net core !

  - <TargetFramework> : Informa a versão do ASPnet

  - <AspNetCoreHostingModel> : Informa que não está rodando no ISS e sim emulado no visual studio!

  - <DockerDefaultTargetOS> : Informa que o target do Docker é para Linux!

  - <UserSecretsId> : Usa uma chave para guardar dados importante!

  - <ItemGroup>

    - <PackageReference> : Faz referencia aos pacotes


### Connected Serviçes (PESQUISAR MAIS DEPOIS)

  - Adiciona serviços existentes, personalizado ou do Azure!


### Dependências 

  - Analyzes: Para gestão e monitoramento de performace do Visual Studio!

  - NuGet: São pacotes com fixtures do AspNet Core!

  - SDK: Suporte a técnologia do SDK!

# Launch Settings

### A pasta propriedades

 - dentro dela vai ter o arquivo "Launch Settings.json"

 - Objetivo: configurar como a aplicação será iniciada no Visual Studio!

 - Visual studio tem uma emulação do IIS, se chama IIS express

 - Ambientes: desenvolvimento, Staging : de teste, production: produção!

 - CommandName: Project : processo do dotnet core que vai autohospedar a minha aplicação! 

 - applicationUrl: a do IISExpress foi definida no IIS! 

 - MinhaAppVS está rodando em projet

 - Sempre vai forçar a usar o HTTPs

 <blockquete>

  "applicationUrl": "https://localhost:5001;http://localhost:5000"
 
 </blockquete>

 - nesse arquivo configura o Docker também!

 - renomear o nome , acima do commandName: 
 
    - 'IIS Express' para 'Dev IISExpress'

    - 'MinhaAppVS' para 'Prod SelfHosting'

      - Muda o 'ASPNETCORE_ENVIRONMENT: "Development"' 
      para  'ASPNETCORE_ENVIRONMENT: "Production"'

 Essa pagina é o local aonde configura os ambientes!

 ambuente de : teste, produção e desenvolvimento!

# pasta wwwroot

- A função: armazenar os arquivos estatico: 

  css, js, js, icones, fontes etc

- Arquivos que não são compilados!

- Tera um tratamento diferente do Visual studio!

- Pode executar tarefaz de minificação e buumder

- acesso a repositorio de pacotes, npm, gulp, etc 

# App Settings

- appSetting.json é uma configuração global que serve para qualquer ambiente!

- appSetting.development.json: é uma configuração 

- Pode criar o appSetting.Production.json

- é uma extenção do webconfig, só que com formato json!

- É aonde configura o banco de dados!

# Classes de Configuração

- Program.cs

- Tem a função de dizer como o programa vai funcionar

- Método main chama o método, CreateWebHostBuilder()

  - Que tem a interface IWebHostBuilder

  - Usa o método CreateDefaultBuilder(), para chamar o arquivo:

    'Startup'

  - Cria um host para rodar a sua aplicação

  - o nome do comando para rodar um selfHost é Program, o mesmo nome da classe

  - É separado na classe startup, para poder ficar limpo

  - Configura o MVC, injeção de dependencia etc

# Minha primeira App VS Code

- Precisa ter o SDK intalado para os comando funcionar!

- Comando que informa os outros comando!

<blockquete> dotnet -h </blockquete>

<blockquete> dotnet new -h </blockquete>

- Criando um Projeto

<blockquete> dotnet new mvc -n MinhaAppVSCode </blockquete>

- Abre no VS code

<blockquete> code .</blockquete>

- Rodando o projeto, bota o -h para ver as outras opções

<blockquete>  dotnet run </blockquete>

-  No arquivo appsettings.Development.json, vc configura as irformações do terminar, definindo como "information", "warning", "debug"

### Rodando outro ambiente

- Antes foi trocado o nome no arquivo LaunchSetting.json na pata propriedade;

<blockquete> 

 "Prod": {
      "commandName": "Project",
      "dotnetRunMessages": "true",
      "launchBrowser": true,
      "applicationUrl": "https://localhost:5005;http://localhost:5006",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Staging"
      }
</blockquete>

- Comando rodando outro ambiente!

<blockquete> run --launch-profile Prod </blockquete>

# instalando pacote

- Comando que instala pacote

<blockquete> dotnet add package automapper </blockquete>

- Ver todas as referencias

<blockquete> dotnet list package </blockquete>

# OWIN

- DOTNET por de baixo dos panos!

1° conceito , OWIN sigla antiga!

separar o servidor da aplicação!

WEB HOST(IIS) <- asp.net components, estava dentro!

aspnet dependia do IIS

A ideia do OWIN era separar!

### hoje em dia

- CustomHost: possibilidade de criar o proprio Host.

- SelfHost: possibiblidade de hospedar seu component aspnet no seu proprio processo.

- outros host pode rodar Apach, indingks, etc

### Como resolver

- com uma Interface que tem : Enviroment Dictionary e Application Delegate

<blockquete>
  IDictionary<string, object>
  Func<IDictionary<string, object>, Task>
</blockquete>

- Tudo se trata de por em um fluxo de operações

- Se torna independente de sistema operacional


# Middlewares

- component de softwares em uma aplicação ASPnet core!

- Manipula dados entre os request e responses

- Um middleware possui um responsabiblidade unica

- E pode trabalhar lado a lado com outros middlewares.

- Quando falamos do pipeline do ASPNET CORE estamos falando basicamente de Middlewares.

Resquest -> Middleware -> Response

- Pipeline : pilha de Middleware

- Pode ter um processo na entrada(request) e na saida(response)

<blockquete> </blockquete>

- 

<blockquete>

</blockquete>

- 

<blockquete>

</blockquete>

