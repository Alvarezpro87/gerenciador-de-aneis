# Usa a imagem do SDK do .NET como base
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Define o diretório de trabalho
WORKDIR /app

# Copia o arquivo .csproj para restaurar as dependências
COPY *.csproj ./

# Restaura as dependências
RUN dotnet restore

# Copia o restante do projeto
COPY . ./

# Publica o projeto em modo Release
RUN dotnet publish -c Release -o out

# Usa a imagem Runtime para executar a aplicação
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Expõe a porta 8080
EXPOSE 8080

# Comando de entrada
ENTRYPOINT ["dotnet", "Backend.dll"]
