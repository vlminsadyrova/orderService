#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["./../OrderService.CustomerService.csproj", "src/OrderService.CustomerService/"]
RUN dotnet restore "src/OrderService.CustomerService/OrderService.CustomerService.csproj"
COPY . .
WORKDIR "/src/OrderService.CustomerService"
RUN dotnet build "OrderService.CustomerService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "OrderService.CustomerService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "OrderService.CustomerService.dll"]