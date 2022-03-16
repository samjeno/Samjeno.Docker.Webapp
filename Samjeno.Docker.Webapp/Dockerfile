FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["Samjeno.Docker.Webapp/Samjeno.Docker.Webapp.csproj", "Samjeno.Docker.Webapp/"]

RUN dotnet restore "Samjeno.Docker.Webapp/Samjeno.Docker.Webapp.csproj"
COPY . .
WORKDIR "/src/Samjeno.Docker.Webapp"
RUN dotnet build "Samjeno.Docker.Webapp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Samjeno.Docker.Webapp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Samjeno.Docker.Webapp.dll"]