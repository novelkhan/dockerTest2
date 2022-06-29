#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["dockerTest2/dockerTest2.csproj", "dockerTest2/"]
RUN dotnet restore "dockerTest2/dockerTest2.csproj"
COPY . .
WORKDIR "/src/dockerTest2"
RUN dotnet build "dockerTest2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dockerTest2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dockerTest2.dll"]