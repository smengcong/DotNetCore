FROM docker.io/microsoft/dotnet
WORKDIR /app
EXPOSE 80
FROM docker.io/microsoft/dotnet
WORKDIR /src
COPY ["smc.Jenkins/smc.Jenkins.csproj", "smc.Jenkins/"]
RUN dotnet restore "smc.Jenkins/smc.Jenkins.csproj"
COPY . .
WORKDIR "/src/smc.Jenkins"
RUN dotnet build "smc.Jenkins.csproj" -c Release -o /app
RUN dotnet publish "smc.Jenkins.csproj" -c Release -o /app
ENTRYPOINT ["dotnet", "smc.Jenkins.dll"]