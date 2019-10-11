FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY Emo.Api/Emo.Api.csproj Emo.Api/
RUN dotnet restore Emo.Api/Emo.Api.csproj
COPY . .
WORKDIR /src/Emo.Api
RUN dotnet build Emo.Api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Emo.Api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Emo.Api.dll"]
