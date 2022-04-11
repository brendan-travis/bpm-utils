FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/BpmUtils.Ui/BpmUtils.Ui.csproj", "BpmUtils.Ui/"]
RUN dotnet restore "src/BpmUtils.Ui/BpmUtils.Ui.csproj"
COPY . .
WORKDIR "/src/BpmUtils.Ui"
RUN dotnet build "BpmUtils.Ui.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BpmUtils.Ui.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BpmUtils.Ui.dll"]
