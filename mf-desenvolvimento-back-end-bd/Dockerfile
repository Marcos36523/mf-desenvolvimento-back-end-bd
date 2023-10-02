#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["mf-desenvolvimento-back-end-bd/mf-desenvolvimento-back-end-bd.csproj", "mf-desenvolvimento-back-end-bd/"]
RUN dotnet restore "mf-desenvolvimento-back-end-bd/mf-desenvolvimento-back-end-bd.csproj"
COPY . .
WORKDIR "/src/mf-desenvolvimento-back-end-bd"
RUN dotnet build "mf-desenvolvimento-back-end-bd.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "mf-desenvolvimento-back-end-bd.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "mf-desenvolvimento-back-end-bd.dll"]