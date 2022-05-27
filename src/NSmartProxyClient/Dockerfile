#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/runtime:3.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["NSmartProxyClient/NSmartProxyClient.csproj", "NSmartProxyClient/"]
COPY ["NSmartProxy.ClientRouter/NSmartProxy.ClientRouter.csproj", "NSmartProxy.ClientRouter/"]
COPY ["NSmartProxy.Data/NSmartProxy.Data.csproj", "NSmartProxy.Data/"]
COPY ["NSmartProxy.Infrastructure/NSmartProxy.Infrastructure.csproj", "NSmartProxy.Infrastructure/"]
RUN dotnet restore "NSmartProxyClient/NSmartProxyClient.csproj"
COPY . .
WORKDIR "/src/NSmartProxyClient"
RUN dotnet build "NSmartProxyClient.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NSmartProxyClient.csproj" -c Release -o /app/publish

FROM base AS final
ENV name=""
ENV pwd=""
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["sh","-c","dotnet NSmartProxyClient.dll -u $name -p $pwd"]