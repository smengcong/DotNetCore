FROM docker.io/microsoft/dotnet:latest
WORKDIR /app
EXPOSE 7000

FROM docker.io/microsoft/dotnet:latest
WORKDIR /src
COPY ["smc.Jenkins/smc.Jenkins.csproj", "smc.Jenkins/"]
RUN dotnet restore "smc.Jenkins/smc.Jenkins.csproj"
COPY . .
WORKDIR "/src/smc.Jenkins"
RUN dotnet build "smc.Jenkins.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "smc.Jenkins.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "smc.Jenkins.dll"]
