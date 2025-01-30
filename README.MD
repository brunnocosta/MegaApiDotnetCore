# MegaApiDotnetCore

Este projeto é uma API feita em .NET Core para listar os dados dos bosses de Megaman. O objetivo principal é ser um backend que fornece JSONs no formato abaixo:

```json
{
  "Id": 1,
  "Code": "DLN/DRN-003",
  "Name": "Cutman",
  "HP": 150,
  "Picture": "https://vignette.wikia.nocookie.net/megaman/images/2/22/Cutman.png"
}
```

## Estrutura do Projeto

```plaintext
.vs/
.vscode/
    launch.json
    tasks.json
bin/
Controllers/
    RobotsController.cs
Database/
    DTOs/
    EntityFramework/
    Repositories/
global.json
MegamanApi.csproj
MegamanApi.sln
middlewares/
    MiddlewareLog.cs
    MiddlewareLogExtensions.cs
Models/
    Robot.cs
obj/
Program.cs
Properties/
Services/
Startup.cs
```

## Endpoints

### `GET /api/v1/robots`

Retorna uma lista de todos os robôs.

### `GET /api/v1/robots/{id}`

Retorna os detalhes de um robô específico pelo ID.

### `POST /api/v1/robots`

Adiciona um novo robô.

## Dependências

| Dependência | Versão | Descrição |
|-------------|--------|-----------|
| [Microsoft.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore) | 3.1.8 | ORM para .NET Core |
| [Microsoft.EntityFrameworkCore.Design](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Design) | 3.1.8 | Ferramentas de design para Entity Framework Core |
| [Microsoft.EntityFrameworkCore.SqlServer](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.SqlServer) | 3.1.8 | Provedor SQL Server para Entity Framework Core |
| [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json) | 12.0.2 | Biblioteca para manipulação de JSON |

## Configuração

### Arquivos de Configuração

- `appsettings.json`: Configurações gerais da aplicação.
- `appsettings.Development.json`: Configurações específicas para o ambiente de desenvolvimento.

### Configuração do Middleware

O middleware de logging é configurado no arquivo [`MiddlewareLog.cs`](src/middlewares/MiddlewareLog.cs).

## Técnicas Utilizadas

### Arquitetura

- **Controllers**: Responsáveis por lidar com as requisições HTTP.
- **Services**: Contêm a lógica de negócios.
- **Database**: Contém os DTOs, EntityFramework e Repositories.
- **Middlewares**: Contêm os middlewares personalizados.
- **Models**: Contêm as definições de modelos de dados.

### Padronização

- Controllers no plural.
- Models no singular.

### Services Lifetimes

- **AddSingleton**: O mesmo para todas as requisições.
- **AddScoped**: Criado um para cada client request.
- **Transient**: Nova instância é criada toda vez.

### Pontos Importantes

- Sempre dependa de contratos, nunca de implementação.

## Adicionando Migrations

Para adicionar uma nova migration, execute o comando:

```sh
dotnet ef migrations add InitialMigration -o Database/Entity/Migrations
```

## Testes

Para criar um projeto de testes, execute:

```sh
dotnet new mstest -o NetCoreTesting.Tests
```

Adicione a referência ao projeto principal:

```sh
dotnet add reference ..\NetCoreTesting.Core\NetCoreTesting.Core.csproj
```

Adicione o pacote de testes:

```sh
dotnet add package Microsoft.VisualStudio.QualityTools.UnitTestFramework --version 11.0.50727.1
```

## Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
