FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["TicketProcessor.Microservice/TicketProcessor.Microservice.csproj", "TicketProcessor.Microservice/"]
RUN dotnet restore "TicketProcessor.Microservice/TicketProcessor.Microservice.csproj"
COPY . .
WORKDIR "/src/TicketProcessor.Microservice"
RUN dotnet build "TicketProcessor.Microservice.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TicketProcessor.Microservice.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TicketProcessor.Microservice.dll"]
