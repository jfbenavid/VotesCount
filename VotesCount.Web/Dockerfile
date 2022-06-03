#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["VotesCount.Web/VotesCount.Web.csproj", "VotesCount.Web/"]
RUN dotnet restore "VotesCount.Web/VotesCount.Web.csproj"
COPY . .
WORKDIR "/src/VotesCount.Web"
RUN dotnet build "VotesCount.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "VotesCount.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VotesCount.Web.dll"]