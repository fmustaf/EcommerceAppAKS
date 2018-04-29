FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
#COPY eShopOnWeb.sln ./
#COPY src/Web/Web.csproj src/Web/
#COPY src/ApplicationCore/ApplicationCore.csproj src/ApplicationCore/
#COPY src/Infrastructure/Infrastructure.csproj src/Infrastructure/
COPY . .
RUN dotnet restore -nowarn:msb3202,nu1503
WORKDIR /src/src/Web
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Web.dll"]
