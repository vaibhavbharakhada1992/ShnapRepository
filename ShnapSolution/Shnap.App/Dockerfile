FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Shnap.App/Shnap.App.csproj", "Shnap.App/"]
RUN dotnet restore "Shnap.App/Shnap.App.csproj"
COPY . .
WORKDIR "/src/Shnap.App"
RUN dotnet build "Shnap.App.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Shnap.App.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Shnap.App.dll"]