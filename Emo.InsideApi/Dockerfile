FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY Emo.InsideApi/Emo.InsideApi.csproj Emo.InsideApi/
RUN dotnet restore Emo.InsideApi/Emo.InsideApi.csproj
COPY . .
WORKDIR /src/Emo.InsideApi
RUN dotnet build Emo.InsideApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Emo.InsideApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Emo.InsideApi.dll"]
