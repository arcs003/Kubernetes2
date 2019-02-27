FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Kubernetes2/Kubernetes2.csproj", "Kubernetes2/"]

RUN dotnet restore "Kubernetes2/Kubernetes2.csproj"
COPY . .
WORKDIR "/src/Kubernetes2"
RUN dotnet build "Kubernetes2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Kubernetes2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Kubernetes2.dll"]