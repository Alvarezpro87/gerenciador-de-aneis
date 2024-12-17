# Usa a imagem do SDK do .NET como base
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Define o diretório de trabalho
WORKDIR /app

# Copia os arquivos de solução e projeto
COPY Backend.sln ./
COPY Backend/Backend.csproj ./Backend/

# Restaura as dependências
RUN dotnet restore Backend.sln

# Copia todo o restante do projeto
COPY Backend/. ./Backend/

# Publica o projeto em modo Release
RUN dotnet publish Backend.sln -c Release -o /app/out

# Usa a imagem Runtime para executar a aplicação
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Expõe a porta 8080
EXPOSE 8080

# Comando de entrada
ENTRYPOINT ["dotnet", "Backend.dll"]
