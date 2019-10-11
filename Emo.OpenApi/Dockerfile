FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY Emo.OpenApi/Emo.OpenApi.csproj Emo.OpenApi/
RUN dotnet restore Emo.OpenApi/Emo.OpenApi.csproj
COPY . .
WORKDIR /src/Emo.OpenApi
RUN dotnet build Emo.OpenApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Emo.OpenApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Emo.OpenApi.dll"]
