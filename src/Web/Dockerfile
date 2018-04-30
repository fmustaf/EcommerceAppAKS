FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
#COPY eShopOnWeb.sln ./
#COPY src/Web/Web.csproj src/Web/
#COPY src/ApplicationCore/ApplicationCore.csproj src/ApplicationCore/
#COPY src/Infrastructure/Infrastructure.csproj src/Infrastructure/
COPY . .
RUN dotnet restore src/Web/Web.csproj -nowarn:msb3202,nu1503
WORKDIR /src/src/Web
RUN dotnet build Web.csproj -c Release -o /app
RUN dotnet publish -c Release -o /app

FROM microsoft/aspnetcore:2.0 AS final
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "Web.dll"]
