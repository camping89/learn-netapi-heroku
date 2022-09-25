FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["aspnetcore-webapi-6/aspnetcore-webapi-6.csproj", "aspnetcore-webapi-6/"]
RUN dotnet restore "aspnetcore-webapi-6/aspnetcore-webapi-6.csproj"
COPY . .
WORKDIR "/src/aspnetcore-webapi-6"
RUN dotnet build "aspnetcore-webapi-6.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetcore-webapi-6.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetcore-webapi-6.dll"]
