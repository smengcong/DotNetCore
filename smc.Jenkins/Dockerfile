FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim as base
WORKDIR /app
EXPOSE 7000

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch as build
WORKDIR /src
COPY ["smc.Jenkins/smc.Jenkins.csproj", "smc.Jenkins/"]
RUN dotnet restore "smc.Jenkins/smc.Jenkins.csproj"
COPY . .
WORKDIR "/src/smc.Jenkins"
RUN dotnet build "smc.Jenkins.csproj" -c Release -o /app

FROM build as publish
RUN dotnet publish "smc.Jenkins.csproj" -c Release -o /app

FROM base as final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "smc.Jenkins.dll"]