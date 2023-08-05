FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["TicketManagementSystem.WorkerService/TicketManagementSystem.WorkerService.csproj", "TicketManagementSystem.WorkerService/"]
RUN dotnet restore "TicketManagementSystem.WorkerService/TicketManagementSystem.WorkerService.csproj"
COPY . .
WORKDIR "/src/TicketManagementSystem.WorkerService"
RUN dotnet build "TicketManagementSystem.WorkerService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TicketManagementSystem.WorkerService.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TicketManagementSystem.WorkerService.dll"]
