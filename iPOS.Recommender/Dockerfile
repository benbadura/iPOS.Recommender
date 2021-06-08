#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["iPOS.Recommender/iPOS.Recommender.csproj", "iPOS.Recommender/"]
RUN dotnet restore "iPOS.Recommender/iPOS.Recommender.csproj"
COPY . .
WORKDIR "/src/iPOS.Recommender"
RUN dotnet build "iPOS.Recommender.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "iPOS.Recommender.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "iPOS.Recommender.dll"]