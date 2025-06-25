# Modulo_API
# 📘 Projeto: ModuloAPI - Web API com .NET

### 🧾 Descrição

Este projeto foi desenvolvido durante o Bootcamp **"WEX – End to End Engineering"**, da DIO. O objetivo foi construir uma **Web API RESTful utilizando .NET 6+ com ASP.NET Core**, expondo endpoints personalizados, estruturando controllers e aplicando o Swagger para documentação e testes interativos.

A API contém:

- Um controller de exemplo (`WeatherForecastController`)
- Um controller personalizado (`UsuarioController`)
- Um modelo de previsão (`WeatherForecast.cs`)
- O arquivo de inicialização da aplicação (`Program.cs`)

---

### 💻 Comandos Utilizados no Terminal

```bash
# Criar o projeto Web API
dotnet new webapi

# Executar com hot reload (atualização automática ao salvar)
dotnet watch run

📂 Estrutura do Projeto e Explicações
🔧 Program.cs
Responsável por iniciar o servidor, adicionar os serviços (Controllers e Swagger), configurar HTTPS e o pipeline da aplicação.
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
app.Run();
🌦️ WeatherForecastController.cs
Controller gerado automaticamente. Retorna uma previsão do tempo simulada para os próximos 5 dias:
[HttpGet(Name = "GetWeatherForecast")]
public IEnumerable<WeatherForecast> Get()
{
    return Enumerable.Range(1, 5).Select(index => new WeatherForecast
    {
        Date = DateTime.Now.AddDays(index),
        TemperatureC = Random.Shared.Next(-20, 55),
        Summary = Summaries[Random.Shared.Next(Summaries.Length)]
    }).ToArray();
}
📄 WeatherForecast.cs
Modelo que define os dados de previsão do tempo:
public class WeatherForecast
{
    public DateTime Date { get; set; }
    public int TemperatureC { get; set; }
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
    public string? Summary { get; set; }
}
👤 UsuarioController.cs
Controller personalizado com dois endpoints:
// Exibe a data e hora atual
[HttpGet("obterDataHoraAtua")]
public IActionResult ObterDataHora()
{
    var obj = new
    {
        Data = DateTime.Now.ToLongDateString(),
        Hora = DateTime.Now.ToShortTimeString()
    };
    return Ok(obj);
}

// Apresenta uma mensagem de boas-vindas com o nome recebido
[HttpGet("Apresentar/{nome}")]
public IActionResult Apresentar(string nome)
{
    var mensagem = $"ola {nome}, seja bem vindo!";
    return Ok(new { mensagem });
}
🧪 Testando a API com Swagger
1 Execute a API com:
dotnet watch run
2 Acesse no navegador:
https://localhost:{porta}/swagger
3 Teste os endpoints disponíveis:
GET /Usuario/obterDataHoraAtua

GET /Usuario/Apresentar/{nome}

GET /WeatherForecast
📌 Observações Finais
Necessário ter instalado o .NET SDK 6 ou superior.

O Swagger facilita o teste e documentação dos endpoints.

O comando dotnet watch run é ideal para desenvolvimento com hot reload.

🧠 Objetivo de Aprendizado
Criar Web APIs com ASP.NET Core

Usar Controllers e Rotas REST

Configurar Swagger

Iniciar o uso do terminal para scaffolding e execução de APIs
