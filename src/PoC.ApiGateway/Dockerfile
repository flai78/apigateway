FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["src/PoC.ApiGateway/PoC.ApiGateway.csproj", "src/PoC.ApiGateway/"]
RUN dotnet restore "src/PoC.ApiGateway/PoC.ApiGateway.csproj"
COPY . .
WORKDIR "/src/src/PoC.ApiGateway"
RUN dotnet build "PoC.ApiGateway.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PoC.ApiGateway.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PoC.ApiGateway.dll"]