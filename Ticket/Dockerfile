FROM mcr.microsoft.com/dotnet/runtime:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Ticket/Ticket.csproj", "Ticket/"]
RUN dotnet restore "Ticket/Ticket.csproj"
COPY . .
WORKDIR "/src/Ticket"
RUN dotnet build "Ticket.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Ticket.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Ticket.dll"]
