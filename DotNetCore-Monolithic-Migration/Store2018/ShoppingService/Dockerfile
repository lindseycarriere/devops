#microsoft/dotnet:2.1-sdk
#microsoft/dotnet:2.1-aspnetcore-runtime
#microsoft/dotnet:2.1-runtime

FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src/ShoppingService
COPY ./ShoppingService.csproj .

RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
RUN pwd
RUN ls -la
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ShoppingService.dll"]
