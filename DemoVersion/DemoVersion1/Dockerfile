#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DemoVersion1/DemoVersion1.csproj", "DemoVersion1/"]
RUN dotnet restore "DemoVersion1/DemoVersion1.csproj"
COPY . .
WORKDIR "/src/DemoVersion1"
RUN dotnet build "DemoVersion1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DemoVersion1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DemoVersion1.dll"]