FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["AuthAssignment/AuthAssignment.csproj", "AuthAssignment/"]
RUN dotnet restore "AuthAssignment/AuthAssignment.csproj"
COPY . .
WORKDIR "/src/AuthAssignment"
RUN dotnet build "AuthAssignment.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AuthAssignment.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AuthAssignment.dll"]
