FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["BookShelf/BookShelf.csproj", "BookShelf/"]
RUN dotnet restore "BookShelf/BookShelf.csproj"
COPY . .
WORKDIR "/src/BookShelf"
RUN dotnet build "BookShelf.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BookShelf.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BookShelf.dll"]
