#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["EPila.Ph.Web.Kiosk/EPila.Ph.Web.Kiosk.csproj", "EPila.Ph.Web.Kiosk/"]
RUN dotnet restore "EPila.Ph.Web.Kiosk/EPila.Ph.Web.Kiosk.csproj"
COPY . .
WORKDIR "/src/EPila.Ph.Web.Kiosk"
RUN dotnet build "EPila.Ph.Web.Kiosk.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EPila.Ph.Web.Kiosk.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EPila.Ph.Web.Kiosk.dll"]