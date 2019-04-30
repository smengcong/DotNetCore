FROM base:mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim 
WORKDIR /app
EXPOSE 7000

FROM build:mcr.microsoft.com/dotnet/core/sdk:2.2-stretch
WORKDIR /src
COPY ["smc.Jenkins/smc.Jenkins.csproj", "smc.Jenkins/"]
RUN dotnet restore "smc.Jenkins/smc.Jenkins.csproj"
COPY . .
WORKDIR "/src/smc.Jenkins"
RUN dotnet build "smc.Jenkins.csproj" -c Release -o /app

FROM publish:build 
RUN dotnet publish "smc.Jenkins.csproj" -c Release -o /app

FROM final:base 
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "smc.Jenkins.dll"]