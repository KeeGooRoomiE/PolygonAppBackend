# Stage 1: Build the .NET app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /app

# Копируем файлы проекта
COPY *.csproj ./
RUN dotnet restore

# Копируем весь код проекта и публикуем его
COPY . .
RUN dotnet publish -c Release -o /out

# Stage 2: Run the app
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

WORKDIR /app
COPY --from=build /out .

# Открываем порт 5000 для приложения
EXPOSE 5000

# Запускаем приложение
ENTRYPOINT ["dotnet", "PolygonApp.dll"]