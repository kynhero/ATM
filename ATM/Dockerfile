FROM mcr.microsoft.com/dotnet/core/runtime:3.1 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["ATM/ATM.csproj", "ATM/"]
RUN dotnet restore "ATM/ATM.csproj"
COPY . .
WORKDIR "/src/ATM"
RUN dotnet build "ATM.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ATM.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ATM.dll"]
