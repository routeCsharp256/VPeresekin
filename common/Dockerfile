FROM mcr.microsoft.com/dotnet/sdk:5.0 AS BUILD

WORKDIR /src

COPY ["src/merchandise-service/merchandise-service.csproj","src/merchandise-service/"]
RUN dotnet restore "src/merchandise-service/merchandise-service.csproj"

COPY . .

WORKDIR "/src/src/merchandise-service"

RUN  dotnet build "merchandise-service.csproj" -c Release -o /app/build

FROM  build as publish
RUN dotnet publish "merchandise-service.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS runtime

WORKDIR  /app

EXPOSE 80
EXPOSE 443

FROM runtime as final
WORKDIR /app

COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet","merchandise-service.dll"]