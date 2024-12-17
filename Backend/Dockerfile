# Use a imagem base do SDK do .NET
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Define o diretório de trabalho dentro do container
WORKDIR /app

# Copia apenas o arquivo .csproj para restaurar as dependências
COPY *.csproj ./

# Executa o restore para baixar as dependências
RUN dotnet restore

# Copia os arquivos restantes
COPY . ./

# Compila o projeto
RUN dotnet publish -c Release -o out

# Usa a imagem do ASP.NET Runtime para rodar a aplicação
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime

# Define o diretório de trabalho no container
WORKDIR /app

# Copia a saída da compilação para o container
COPY --from=build /app/out ./

# Expõe a porta 8080
EXPOSE 8080

# Comando para rodar a aplicação
ENTRYPOINT ["dotnet", "Backend.dll"]
