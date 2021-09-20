#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["BA100/BA100.csproj", "BA100/"]
RUN dotnet restore "BA100/BA100.csproj"
COPY . .
WORKDIR "/src/BA100"
RUN dotnet build "BA100.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BA100.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BA100.dll"]