FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["src/Di.Netti.Svc/Di.Netti.Svc.csproj", "src/Di.Netti.Svc/"]
RUN dotnet restore "src/Di.Netti.Svc/Di.Netti.Svc.csproj"
COPY . .
WORKDIR "/src/src/Di.Netti.Svc"
RUN dotnet build "Di.Netti.Svc.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Di.Netti.Svc.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Di.Netti.Svc.dll"]